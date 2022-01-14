## Understanding Proof of Stake - (PoS)

## Hey Everyone👋👋

When we talk about blockchains on decentralized systems such as Ethereum and Bitcoin, there is no centralized mechanism or system to believe in for a single source of truth. This is where consensus mechanisms drop in. 

Now, Proof of stake (PoS) is one such consensus mechanism that will be the core Ethereum 2.0. In this article, we will try to understand the working of Proof of Stake (PoS) and Pros-cons for same.

I request you to stake your attention for some time! 😅😅



![JulJulbGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1642161102770/I33HFjnAR.gif)


## ⚒️Proof of Work

To understand Proof of stake, we need to have a look at another consensus mechanism that is Proof of work which is currently being used by Bitcoin and Ethereum.

Let us understand this step-wise : 
- All the nodes in the network have the same blockchain.
- Now transactions are bundled together to form a block.
- In order to add this block to the chain, all the miners compete against each other to solve a puzzle that comes with that block.
- The only way to solve the puzzle is with the trial-error method.
- Whoever solves this puzzle first gets a Reward.
- Once the puzzle is solved it is easy to verify the solution for the same.
- If more than 50% of nodes on the network verify if it is correct then they add it to their blockchain.


Amazing !!🎉🎉 Now that you have understood Proof of work (PoW) let us see the demerits of it and understand Why we need another consensus mechanism ❓🤔
In the end, PoW is just like a  race with no 2nd and 3rd position, only the 1st position will secure the reward.



![ThisIsAWeirdRaceAnthonyAlfredoGIF (2).gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1642144298138/t6NQuOAPVf.gif)


### 📛Demerits of Proof of Work 

- Energy Consumption

Miners need to use special hardware with a huge amount of computing capacity in order to solve the puzzle and get rewards. A huge amount of electricity is required to run these mining nodes continuously.
As you know, all the miners compete against each other to solve the puzzle, but only the miner who solves it first gets the reward. Due to this all power and energy consumed by other miners are since the work is just thrown away if they aren’t the first one to solve it.

> Did you know? 

> Mining a single bitcoin transaction is equivalent to the power consumption of an average U.S. household over 77.87 days. 
You can read more  [here](https://digiconomist.net/bitcoin-energy-consumption/).

- Centralized Mining Pools

As more complex calculation requires more computational power which in turn increases the overall cost, thus increasing the centralization of miners which is beneficial for them. As the cost is increased to solve the puzzle, it does not encourage new miners to join the network.


To address these disadvantages, we need different consensus mechanisms.
Now let us understand Proof of Stake (PoS).


![ShallWeShouldWeGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1642148175769/a2qYU_sI4.gif)

## 📜Proof of Stake - (PoS)

 Now as we know that Proof of Stake is also a consensus mechanism, let us understand the working of it.

#### ⚒️Working of Proof of Stake :

- In Proof of Stake Mining of blocks is known as "Forging".
- In Proof of Stake the specific network chooses one node to validate the block instead of competing against each other. These guys here are known as validators instead of miners. 
- To become a validator the node should commit some amount of funds to the network, which we call here Staking.
- After this the network chooses one validator to validate the block's transactions and add the block to the chain.
- Proof of Stake uses Pseudo-random election to be the validator of the block, based on a various number of factors that includes the staking age, randomization.
- Once this is done, the node receives some transaction fees which are associated with the block.


Great !! Now that you have understood PoS, you might have certain doubts in your mind! Let's look at them below.


#### 🎯What if validator creates fraudulent transactions in the block?

If the validator misbehaves and creates fraudulent transactions in the block, then the network will punish the validator by taking some amount of the funds from the owner's stake. 

Eg :  

In Ethereum the owner needs to deposit 32 ETH in order to become a validator.
Now if this particular node is selected by the network as a validator and if the validator fails to validate in any way then some portion of his stake will be taken away and he would be blacklisted.


#### 🎯How does validator selection work in Proof of Stake?

Node selection to become a validator has various factors depending on the blockchain environment and its eco-system but these are the two general ways it is done :

- Coin-age Selection:

Here the algorithm keeps a track of the time that node stays a validator. 
The chances of getting selected become higher as the node gets older and older.


- Random Block selection:

The method uses a combination of ‘lowest hash value’ and ‘highest stake’ for the selection of a new validator. The node having the best combination of these becomes the new validator. 


#### 🎯What if the Validator wants to stop Forging? 

The validator can opt to withdraw the stakes from the network. If the network detects any mishap by the validator, it can take a part of the deposit or the whole deposit as a  form of penalty.


### ♻️Merits

- Reduced Power consumption (like way too much reduced in comparison with Proof of Work)
- No need for High computational power
- The above two help in reducing  the overall cost
- As the cost is low it encourages more people to set up their own node and get started hence making the network more decentralized.

### 📛Demerits

- Proof-of-stake is still in its building stage, though it has been deployed by several networks, it is  less tested relative to proof-of-work

- Nodes need to stake something at first, it might happen that a node doesn't own anything to stake at all.

## 🎯Final Thoughts

Proof of Stake seems to be a much better consensus measure but still its in process of making its way to the Mainnet of Ethereum.
Proof of Stake will be rolling out with on Ethereum. 2.0 this year. In fact, it is already there on Beacon Chain, you can find more [here](https://launchpad.ethereum.org/en/).

Amazing !! Congrats on making it to the end! 🎉🎉

*That's the end of the article!  Cheers and have a Good Day!*


![CheersPartyGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1642161623719/vKJ12i98N.gif)
