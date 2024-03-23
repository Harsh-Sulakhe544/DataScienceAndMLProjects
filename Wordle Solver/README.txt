# 🧩 wordle-solver
Welcome!

This repo has a couple of files of interest:
- **answers.txt:** Taken from [here](https://www.powerlanguage.co.uk/wordle/main.e65ce0a5.js), 
  the first ~2,300 word array (starting with the word "cigar") is [assumed to be the set of possible 
  answers for Wordle](https://puzzling.stackexchange.com/a/114518)
- **Wordle solver - exploration.ipynb:** My notebook with all the relevant code 

I'm looking to build this out into a streamlit app, but leaving the above files untouched. Watch this space...

why re.sub() => syntax ==>  re.sub(pattern, repl, string, count=0, flags=0)


why calculate_freq_score() ==> 
Suppose you have a dataset of 5-letter words related to animals:

LIONE
BEARS
HORSE
SNAKE
TIGER
EAGLE
SHEEP
MOUSE
DOGIE
SEALY
Now, let's say you are analyzing the frequency of the letter 'S' appearing as the first letter in these words:

'S' appears as the first letter in 3 out of 10 words (SNAKE, SHEEP, SEALY).
So, in this real-world example, the score for 'S' at position 1 would be 3.

This scoring system helps the game prioritize letters that are frequently occurring in specific positions, 
aiding in making more informed guesses. If you have any further questions or need more clarification, feel 
free to ask!

letters = "ABCDE"

# Assume dict_letter_counts for illustration
dict_letter_counts = {
    1: Counter({'A': 3, 'B': 2, 'C': 1, 'D': 0, 'E': 1}),
    2: Counter({'A': 0, 'B': 1, 'C': 2, 'D': 1, 'E': 1}),
    3: Counter({'A': 1, 'B': 1, 'C': 0, 'D': 2, 'E': 0}),
    4: Counter({'A': 2, 'B': 0, 'C': 1, 'D': 0, 'E': 2}),
    5: Counter({'A': 0, 'B': 1, 'C': 0, 'D': 2, 'E': 1}),
}

explaination : In this example, the calculated score is based on the counts of each letter at its respective 
position in the word "ABCDE" using the provided dict_letter_counts. The enumerate function helps iterate over 
the letters with their indices, and list makes the string iterable for enumeration. The score += ... 
operation accumulates the counts to calculate the final score.

# START ANALYZING FROM HERE 
    def guess(self):

query(str) => filter based on a str => returns a dataframe    
The iterrows() method is used to iterate over the rows of a DataFrame, providing both the index and the data 
of each row as a Series. 

assert => to raise Assertion IO error 

The sample() method returns a list with a specified number of randomly selected items from a sequence. Note: 
This method does not change the original sequence.