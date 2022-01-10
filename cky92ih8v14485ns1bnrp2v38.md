## Minting your Custom ERC-20 Tokens on Ethereum from Scratch

## 👋👋Hey Everyone!

As we all know WEB 3.0 is here to stay, having said that all new developers should at least get their hands dirty and see how they feel about it.

<hr />
Today we will be making your custom ERC-20 tokens which we can use as a form of payment or rewards. Now you can either follow along with the blog or if you are too excited you can go [here](https://gist.github.com/devdattakhoche/47982124a1b88c049d8b905351c1c224) and get the complete code .

**What are ERC-20 tokens? 🪙🪙**

ERC-20 is the technical standard on the Ethereum blockchain for token implementation and provides an Interface that every token contract should follow.

In simple ERC-20 is a set of rules which you adhere to while implementing your own custom Tokens on the Ethereum blockchain. Here token is a smart contract that will perform operations when certain conditions are met.

Now ERC-20 is somewhat similar to Bitcoin but the only major difference here is that you don't need to make your blockchain to deploy it, instead you will be deploying it on Ethereum.

We will be making smart Contracts with solidity on Remix IDE as it reduces your time for development setup.
If you are not familiar with Solidity or smart contracts you can check this out  [here](https://devsblog.hashnode.dev/getting-started-with-ethereum-and-solidity)  so that you would be able to follow along.

Now enough of the theoretical part, let's dive in.

![DiveGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641810140208/6XXnO46w1.gif)


## 🔥 Let's get Started

Step 1: To implement our Token to adhere to ERC-20 standards defined by Ethereum.
What does the standard interface look like? Here it is:


```
interface ERC20{
    function balanceOf(address _owner) external view returns (uint256 balance);
    function transfer(address _to, uint256 _value)  external returns (bool success);
    function transferFrom(address _from, address _to, uint256 _value) external returns (bool success);
    function approve(address _spender  , uint256 _value) external returns (bool success);
    function allowance(address _owner, address _spender) external view returns (uint256 remaining);

    event Transfer(address indexed _from, address indexed _to, uint256 _value);
    event Approval(address indexed _owner, address indexed _spender, uint256 _value);
}
``` 
 
Now this in an Interface, Interface has all the empty methods defined which we need to implement. For more info on ERC-20 Standard Interface, you can visit  [here](https://github.com/ethereum/EIPs/blob/f98a60e1b1590c9cfa0bfe66c4e6a674e54cd386/EIPS/eip-20.md). 
We will create a `.sol`  file and add this interface to it in  [Remix IDE](https://remix.ethereum.org/).

Step 2: Once we have done this let us create our custom token contract.
In Solidity, we create a contract with the keyword `contract`.
We will inherit the interface which we added to our file.

Declaring all functions in an interface is just a good programming practice, as it allows you to use that interface instead of the actual contract elsewhere in your code.

Let us also define all the necessary variables which we will be needing to implement the function defined in the interface.

```
contract YourCustomToken is ERC20{

    uint256 public totalSupply;          //Total coins in circulation
    string public name;                   //fancy name: eg Dev's Bucks
    uint8 public decimals;               //How many decimals to show.
    string public symbol;                // Symbol : DBK (for Dev's Bucks)
}

```

The name here represents the name of the token similarly symbol represents the Symbol.
The `totalSupply` is the amount of the tokens which will be circulation on the blockchain. We cannot mint more tokens than the totalSupply.

```
Eg:  
Name: Bitcoin
Symbol: BTC
TotalSupply: 21,000,000 // not more bitcoins can be generated than this number
```

Now coming to decimals, neither the Ethereum Virtual Machine nor Solidity offer support for decimal numbers—they only support various types of integers.
You might think why do we need decimals? 

Consider you have 3 tokens and you want to divide it into 2 equal parts, then it comes out to be 1.5 each, which we cannot do due to decimal constraint.

Here is where the decimals variable drops in.
If I want 1 token with the ability to further divide it with a precision of 2 decimal places then we represent decimals as 100.
Similarly, if I want  9 subdivisions of then we represent it 10^9.

So far our solidity files look like this :

```
// SPDX-License-Identifier: MIT
pragma solidity >=0.5.0 <0.8.0;


interface ERC20{
    function balanceOf(address _owner) external view returns (uint256 balance);
    function transfer(address _to, uint256 _value)  external returns (bool success);
    function transferFrom(address _from, address _to, uint256 _value) external returns (bool success);
    function approve(address _spender  , uint256 _value) external returns (bool success);
    function allowance(address _owner, address _spender) external view returns (uint256 remaining);

    event Transfer(address indexed _from, address indexed _to, uint256 _value);
    event Approval(address indexed _owner, address indexed _spender, uint256 _value);
}

contract YourCustomToken is ERC20{

    uint256 public totalSupply;          //Total coins in circulation
    string public name;                   //fancy name: eg Dev's Bucks
    uint8 public decimals;               //How many decimals to show.
    string public symbol;                // Symbol : DBK (for Dev's Bucks)
}

```

Step 3: Let us now implement all the functions in the interface.

**balanceOf**
```
 mapping (address => uint256) public balances;

function balanceOf(address _owner) public override view returns (uint256 balance) {
        return balances[_owner];
    }
```
`balanceOf` function is a static function that allows the user to view the account balance. Here it `_owner` is the address. The underscore here before the parameter signifies that it is a variable which only used in this function. Putting this underscore is a good programming practice in solidity. To store the balances we create a mapping that will map the corresponding address to the balance that address has.


**transfer**
```
function transfer(address _to, uint256 _value) public override returns (bool success) {
        require(balances[msg.sender] >= _value, "token balance is lower than the value requested");
        balances[msg.sender] =  balances[msg.sender] -  _value;
        balances[_to] =  balances[_tp] +  _value;
        emit Transfer(msg.sender, _to, _value); 
        return true;
    }
```

`transfer` function is a dynamic function that modifies the state of the contract.
This function is responsible to transfer the `_value` of tokens to address `_to`.
Firstly we check if the account that is transferring tokens has a sufficient balance with `require`. If the above condition satisfies we deduct the amount from the owner's address and add it to address `_to`.

After this function triggers the `Transfer` Event which is declared in the interface, which transfer's the amount.


**approve**


```
mapping (address => mapping (address => uint256)) public allowed;
function approve(address _spender, uint256 _value) public override returns (bool success) {
        allowed[msg.sender][_spender] = _value;
        emit Approval(msg.sender, _spender, _value); //solhint-disable-line indent, no-unused-vars
        return true;
    }
```

`approve` function approves someone else to transact on behalf of your own.
Now you might wonder why would you do that?
Consider this eg: You have a 1kg gold(token), and you are the owner.
Now you want to sell it but you don't have potential buyers. You will give this to a gold dealer (Dapps) who will charge you a small fee.  This way, a lot more potential buyers will be able to buy the gold and you will also benefit.

Here gold is the token, you are the owner who is approving, gold dealer in the Dapp on blockchain who will use it on your behalf.

So we create a mapping of mapping where map all the addresses corresponding to the owner address who is authorizing them and the value which they can spend.
You can look at it this way : 
```
[Owner] -> [Gold dealer 1] -> 1 kg Gold // Allowing to transact 1 Kg gold
           [Gold dealer 2] -> 2 kg Gold // Allowing to transact 2 Kg gold 
```
After the mapping is created we trigger the Approve event that is defined in the Interface.


**allowance**

```
function allowance(address _owner, address _spender) public override view returns (uint256 remaining) {
        return allowed[_owner][_spender];
    }

```
`allowance` is a static function that returns the amount which the spender on behalf of the owner is allowed to spend.


**transferFrom**


```
function transferFrom(address _from, address _to, uint256 _value) public override returns (bool success) {
        uint256 allowance = allowed[_from][msg.sender];
        require(balances[_from] >= _value && allowance >= _value, "token balance or allowance is lower than amount requested");
        balances[_to] = balances[_to] + _value;
        balances[_from] = balances[_to] - _value;
        allowed[_from][msg.sender] = allowed[_from][msg.sender] - _value;
        emit Transfer(_from, _to, _value); //solhint-disable-line indent, no-unused-vars
        return true;
    }

```

`transferFrom` function is a dynamic function which transfers `_value` from `_from`
address to `_to` address. This function is used when somebody does a transaction on behalf of someone. Now to this transfer we first check the following conditions : 

1. `_from` address must have balance more than or equal to `_value`
2.  As this is an `on behalf` transaction, we need to check if the spender is allowed to spend an amount that is more than or equal to `_value`.

Once these two conditions are met, we do the mentioned operations :

1. Add `_value` amount to `_to` address
2. Deduct `_value` amount from `_from` address
3. Deduct the allocated value of `on behalf` transfer from `allowed` mapping.

Now we trigger the Transfer event that is defined in the Interface.

Congrats on making it this far!🥳🥳 

Now as we have declared all the functions in the interface, let us allocate all the coins to the deployer's account and the rest of the variables which we declared earlier.

**constructor (Initial Call)**

```

constructor(uint256 _initialAmount, string memory _tokenName, uint8 _decimalUnits, string  memory _tokenSymbol) {
        balances[msg.sender] = _initialAmount;               // Give the creator all initial tokens
        totalSupply = _initialAmount;                        // Update total supply
        name = _tokenName;                                   // Set the name for display purposes
        decimals = _decimalUnits;                            // Amount of decimals for display purposes
        symbol = _tokenSymbol;                               // Set the symbol for display purposes
    }

```
A Constructor is a special method declared using the `constructor` keyword. It is an optional function and is used to initialize the state variables of a contract. It is always executed once when a contract is created and it is used to initialize the contract state. Here we take `_initalAmont` which is the total coins in circulation and give them to ourselves. Similarly, we assign `name`, `decimals`, `totalSupply` and `symbol`.

To sum up all the code : 

```
// SPDX-License-Identifier: MIT
pragma solidity >=0.5.0 <0.8.0;


interface ERC20{
    function balanceOf(address _owner) external view returns (uint256 balance);
    function transfer(address _to, uint256 _value)  external returns (bool success);
    function transferFrom(address _from, address _to, uint256 _value) external returns (bool success);
    function approve(address _spender  , uint256 _value) external returns (bool success);
    function allowance(address _owner, address _spender) external view returns (uint256 remaining);

    event Transfer(address indexed _from, address indexed _to, uint256 _value);
    event Approval(address indexed _owner, address indexed _spender, uint256 _value);
}

contract YourCustomToken is ERC20{

    uint256 public totalSupply;          //Total coins in circulation
    string public name;                   //fancy name: eg Dev's Bucks
    uint8 public decimals;               //How many decimals to show.
    string public symbol;                // Symbol : DBK (for Dev's Bucks)
    mapping (address => uint256) public balances;    
    mapping (address => mapping (address => uint256)) public allowed;
    
    constructor(uint256 _initialAmount, string memory _tokenName, uint8 _decimalUnits, string  memory _tokenSymbol) {
        balances[msg.sender] = _initialAmount;               // Give the creator all initial tokens
        totalSupply = _initialAmount;                        // Update total supply
        name = _tokenName;                                   // Set the name for display purposes
        decimals = _decimalUnits;                            // Amount of decimals for display purposes
        symbol = _tokenSymbol;                               // Set the symbol for display purposes
    }



    function balanceOf(address _owner) public override view returns (uint256 balance) {
        return balances[_owner];
    }
    
    function transfer(address _to, uint256 _value) public override returns (bool success) {
        require(balances[msg.sender] >= _value, "token balance is lower than the value requested");
        balances[msg.sender] =  balances[msg.sender] -  _value;
        balances[_to] =  balances[_to] +  _value;
        emit Transfer(msg.sender, _to, _value); 
        return true;
    }

    function approve(address _spender, uint256 _value) public override returns (bool success) {
        allowed[msg.sender][_spender] = _value;
        emit Approval(msg.sender, _spender, _value); //solhint-disable-line indent, no-unused-vars
        return true;
    }

    function allowance(address _owner, address _spender) public override view returns (uint256 remaining) {
        return allowed[_owner][_spender];
    }

    function transferFrom(address _from, address _to, uint256 _value) public override returns (bool success) {
        uint256 allowance = allowed[_from][msg.sender];
        require(balances[_from] >= _value && allowance >= _value, "token balance or allowance is lower than amount requested");
        balances[_to] = balances[_to] + _value;
        balances[_from] = balances[_to] - _value;
        allowed[_from][msg.sender] = allowed[_from][msg.sender] - _value;
        emit Transfer(_from, _to, _value); //solhint-disable-line indent, no-unused-vars
        return true;
    }
}

```

 [Here](https://gist.github.com/devdattakhoche/47982124a1b88c049d8b905351c1c224)  is the gist of the contract and  [here](https://remix.ethereum.org/#version=soljson-v0.8.4+commit.c7e474f2.js&optimize=false&runs=200&gist=47982124a1b88c049d8b905351c1c224)  is the direct remix IDE link where you can get this code completely.

Amazing 🎉🎉!! This was a good amount of work, but finally, we are done with the coding part.


![TomAndJerryTomTheCatGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641824332143/MLeQnzk1M.gif)

Now once you are in Remix IDE, go to compile tab and select your contract which has all the functions in this case it will be `YourCustomToken`.


![Screenshot 2022-01-10 195359.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641824703027/6yFpZdv62.png)


Compile your contract and make sure you have no errors.
After this hop over to the deploy tab and expand the Deploy tab, you will see that it will ask initial values for the token which are `name`, `Symbol`, `_initialamount`, `decimal`.

Input these values and deploy the contract.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641824883877/FFzuTOncI.png)

After deploying, expand your deployed contracts and you will notice all the functions which you have written.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641824991215/MKlMc8fJB.png)

You can notice that you will have all the minted coins of your own. You can do this by passing your address in the `balanceOf` function;


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641832191816/9WsAkl9sY.png)


Step 4: Let us now deploy our token on the Rinkbey test network. For this, you will be needing all a wallet. 
You can get your wallet  [here](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn?hl=en).

After you have the wallet, go get some test Ethers in your wallet from  [here](https://faucets.chain.link/rinkeby).
Once this is done, go back to your Remix IDE and instead of Javascript VM, deploy your contract on Injected Web3. **Remember to compile and deploy your custom contract, not the interface.**


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641833138283/CLzsQAktE.png)

Once you have deployed your smart contract, you can see the transaction details in the console. Pick your transaction hash and paste it on Rinkbey etherscan.


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641840203842/RBfoK2vML.png)

The 'To' address here is the address of your contract.
Now after you have done this, go to Metamask and have look under the assets tab. 


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641840309263/dpkLZcW7D.png)

Click on the import token and paste the contract address which we got from etherscan and hit the blue button.

Voila, you have your own custom tokens on your wallet.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641840451317/HM8a3s7H-S.png)

Amazing✌️✌️, Good work !! Congrats for making it to the end.
You have created your won ERC20 tokens on Ethereum.


![IAin'TSorryGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1641841271591/_hLmeREOc.gif)


## 🎯Final Thoughts

You can further go and list this token on  [uniswap](https://app.uniswap.org/#/swap)  or  [quickswap ](https://quickswap.exchange/#/swap) and also add liquidity for the same. Let me know in the comments if you want that too.

ERC20 Tokens are a great way to step in Ethereum and solidity development.
You get to know a lot of things. You can use these tokens to incentivize or give rewards. I hope you liked the article and got something to take out of it.
Note that to make production-ready tokens on Mainnet you need to test your contracts first, else it might cost you a lot every time you redeploy the changes.

Feel free to reach out to me.
If you liked the article do share it and give me a follow on hashnode and @devdattakhoche on twitter.✌️✌️