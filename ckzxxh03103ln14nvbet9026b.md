## Building a Wordle Bot with Python and Selenium

## Hey Everyone👋👋

Wordle Wordle Wordle !!!! 🌟🌟

Worlde has become fairly popular. The best part of wordle is, it takes only a few minutes and is really really easy to share.😁😁

Recently I ran across a tweet by my friend which had some green boxes and a grid, to be precise this was the tweet.✌️

%[https://twitter.com/khadapkar20/status/1494768354569064449]

I was a bit confused about this tweet because I didn't know wordle then.
I did some digging and played the game for a day or two and now surely I am also addicted to it.😂😂

To be honest I liked it when I was able to solve it but now I love it when my bot is able to solve it. In this article, we will build a wordle bot and also discuss the algorithm and strategies to get and optimise the solution.

![BotsHobotsGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1645449190268/fbzV1r16l.gif)


Here is what we will have at the end. Now, this is the bot that is solving the wordle.

![Wordle - The New York Times - Google Chrome 2022-02-20 10-22-21.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1645448512566/5JyVWDtOA.gif)

For those who are really excited and can't wait to see the code directly, here is the link for the same.

%[https://github.com/devdattakhoche/Wordle-Selenium-Bot]


## 🔰Before we begin

To solve the wordle let us first understand the wordle.

Now wordle is a game in which you are supposed to guess a 5 letter word in six attempts.

In each attempt, you will give a valid 5 letter word and in return, you will get some information. Based on this information you guess the next word until you reach 6 attempts or you guess the word.
The below image defines it all.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645448829826/-cro9rfu0.png)


The best way to understand it is by playing the wordle.✌️
Here is the [link](https://www.nytimes.com/games/wordle/index.html) for the same.
If you have solved it, congratulations🎉🎉😎.

If you haven't don't worry, we will build a bot to solve our wordle.😂😂
Now that you understood how it works lets us get started with the solution.



## ✅ Building a Strategy

We will discuss two strategies for solving the wordle and also the accuracy for the same. Some part of both the strategies is kind of the same. We will see how we arrive at the final goal that guessing the correct word.

Now each wordle has 5 letters, our final goal is to find out these 5 letters in the correct order. As the number of letters is fixed we basically have a limited set of words from which 1 word is our answer. 

#### 📃General steps in both Strategies

Every guess gives us some information about each letter:


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1645450394554/TrFNbsGe6.png)

Let us take an example here : 

`H` and `O` are coloured yellow:
- Our final answer consists of the letters `H` and `O`. So we shrink the total words which have the letters `H` and `O`.
-  As they are coloured yellow, it means they are in the answer but are incorrectly placed. So we remove the words which have their 1st letter is `H`  or second letter is `O`.

`N` and `Y` are coloured grey :
- This tells us that these two letters are not their in the final answer. So we remove the words which consist of letters `N` and `Y` from the total set.

`E` is coloured green :
- It means that our answer has the letter `E` in the same position as here, so we only keep those words that have `E` in the 4th position.

As you see here, we update the list for every letter and do this until we get our correct answer.
 
Another thing to note is that at least the first guess should have all the characters unique as it will help you to get more information.

There are many first words to start with, such as :

1. `adieu`
2. `slate`
3. `arise`

And many more.


#### 📜 Randomized Greedy Approach

1. In this approach we start with a random word from the total word list which has all characters unique.
2. We shrink the word list based on information we get from the 1st guess.
3. After this if we get a green letter, say `x` on `ith` position (fixed letter in the answer), we choose another random word that has the letter `x` on the `ith` position.
4. We carry out steps 2 and 3 until we reach the 6th attempt or we find the word.

Now, this approach is quite random 😂😂 and it sometimes works and sometimes it does not. 

Now as this is random it has an accuracy of 55 - 70 %, which is not that good. I did test it 

#### 📜Letter frequency approach

In this approach, I fixed the first three words of the guess with all unique characters.
Now the reason here is that in these first 3 guesses I get more than 50% information 
about my answer, after which I start to use letter frequency to guess the next word.

Here are the first 3 words which work best for me:
1. `adieu`
2. `glops`
3. `crwth`

Now many of you might be like "do these words even exist in the first place" 😂😂.
I had the same reaction at the beginning but yea they exist.

1. We try out all these 3 words first and shrink the word list from the collected information.
2. We have left only limited words as all the first 3 words give most of the information required. To explain to you how I guess the next word let us take a look at an example.


Consider that we are left with these 3 words :

- objet
- other
- oxter

I count the frequency of each character 
with respect to the position and add 
all 5 letters to get a value of that word. 
I choose the word with the maximum value which will be our next guess.

How does this help?
If the frequency of any character is more, 
it means the probability of that character is in 
the answer at that position is greater than the rest of the characters.

```
objet = 3 Os + 1 b + 1 j + 3 Es + 1 t = 9
other = 3 Os + 1 t + 1 h + 3 Es + 2 r = 10
oxter = 3 Os + 1 x + 1 t + 3 Es + 2 r = 10

Hence our next word will be `other`  or `oxter`.
```
We do this until we get the answer or we reach the last attempt.

This method fails when you have any 4 letters fixed and you are looking for the 5th one.
Eg :

```
wodge
bodge
modge
lodge
dodge
podge

```


Here you can see the letters `odge` are fixed but only the first letter changes.

Enough of the theoretical part, let's do some coding.🧑‍💻

##🧑‍💻Coding


![GimmeCodeCatGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1645519113867/pKsbyecBQ.gif)


We will use selenium to automate the wordle and python for implementing the logic.
To use selenium you will need to have a selenium web driver which you can get here.

The original website has a shadow root element, Shadow DOM serves for encapsulation. It allows a component to having its very own “shadow” DOM tree, that can’t be accidentally accessed from the main document, may have local style rules, and more.

So we need to access the shadow root element first and then access the components inside it.

Here is the code related to the selenium driver :

```
import io
import time

import pandas as pd
import requests
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
from webdriver_manager.chrome import ChromeDriverManager
from webdriver_manager.utils import ChromeType



CONSTANTS = {
    "wordle_url": "https://www.nytimes.com/games/wordle/index.html",
    "words_csv": "https://raw.githubusercontent.com/tabatkins/wordle-list/main/words",
    "word_list": ["adieu", "golps", "crwth"]
}


incorrect_letters = set()
correct_letters = set()
counts = {}
previous_correct_letter = set()
ans_list = ["." for i in range(5)]


#####################Driver Functions#############################


def get_letter_data_state(driver_instance, grid, _):
    state = driver_instance.execute_script(
        "return arguments[0].shadowRoot.querySelector('div > game-tile:nth-child({})')".format(
            _ + 1
        ),
        grid,
    )
    data_state = state.get_attribute("evaluation")
    letter = state.get_attribute("letter")
    return letter, data_state


def get_keys(driver_instance):
    game = get_game(driver_instance)
    keyboard = game.find_element(By.TAG_NAME, "game-keyboard")
    keys = driver_instance.execute_script(
        "return arguments[0].shadowRoot.getElementById('keyboard')", keyboard
    )
    return keys


def get_board_grid(driver_instance, word):
    game = get_game(driver_instance)
    grid_row = game.find_element(By.CSS_SELECTOR, f"game-row[letters='{word}']")
    return grid_row


def get_game(driver_instance):
    game_app = driver_instance.find_element(By.TAG_NAME, "game-app")
    game = driver_instance.execute_script(
        "return arguments[0].shadowRoot.getElementById('game')", game_app
    )
    return game


def goaway_popup(driver_instance):
    driver_instance.find_element(By.TAG_NAME, "body").click()


def init_driver():
    s = Service(ChromeDriverManager().install())
    option = webdriver.ChromeOptions()
    option.add_argument("--incognito")
    # option.add_argument("-headless")
    option.add_experimental_option("excludeSwitches", ["enable-logging"])
    driver = webdriver.Chrome(service=s, options=option)
    driver.get(CONSTANTS["wordle_url"])
    time.sleep(1)
    return driver


def press_key(keys, letter):
    keys.find_element(By.CSS_SELECTOR, f'button[data-key="{letter}"]').click()

```

We will also need the word list, which we will access from [here](https://github.com/tabatkins/wordle-list/blob/main/words).

Also, you can find the code for the same on GitHub, I don't want to spam this article with lots of code.😂😂 

%[https://github.com/devdattakhoche/Wordle-Selenium-Bot]

There are many better algorithms out there that you can try out and get better accuracy. Also, I have made a wordle game just for the sake of testing my algorithm which is in the repository with the filename as `wordle_test.py`.

## 🎯Final Thoughts

Congratulations on making it to the end of the article.🎉🎉

Though I have made a bot to solve it automatically, I  still solve it on my own.😂
When I get the answer it feels amazing but when I don't that is when I use my bot 😈😈.

Wordle is a cool game, easy to play and easy to share, automating it makes no point but yea it feels good when my bot solves it😎.

I hope you enjoyed the article, do let me know if you have any suggestions for the article. Also, let me know if you have a better strategy, I will definitely try it out.

*Thank you for reading, Have a good day! Bye Bye! 👋🙋‍♂️* 


![OogwayMyTimeHasComeGIF.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1645520185939/AHc2dfO5W.gif)
