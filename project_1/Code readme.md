=============================================================
WORD TOKENIZER
=============================================================



We are going to complete the code for word-level tokenization.

Steps:

Build vocabulary from the corpus.

We'll split each sentence by spaces to get words.

We'll collect all unique words and assign an ID to each.

We'll create two dictionaries: word2id and id2word.

Implement the encode function.

Split the input text by spaces.

For each word, look up its ID in word2id. If the word is not in the vocabulary, we have to handle it.
Since we are building the vocabulary from the corpus, any word not in the corpus will be unknown.
We can use a special token [UNK] for unknown words. But note: our current vocabulary doesn't have [UNK].
We have two options:
Option 1: Add [UNK] to the vocabulary.
Option 2: Let the tokenizer throw an error.

Since the problem says we should try with unseen words, let's add [UNK] to the vocabulary.

Implement the decode function.

For each ID in the input list, look up the word in id2word.

Then join the words with spaces.

Test the tokenizer.

Let's adjust the code accordingly.

We'll do:

Preprocess the corpus: split each sentence into words and collect unique words.

Then, we'll add a special token [UNK] at the beginning or end of the vocabulary.

Then build the mappings.

However, note that the original corpus doesn't have [UNK]. So when building the vocabulary, we can either:

First, build the vocabulary from the corpus, then add [UNK] (so [UNK] is the first token, for example).

Or, we can build the vocabulary without [UNK] and then when encoding, if a word is not found, we use a default ID for [UNK].

But wait, the problem says: "Try a sentence with unseen words and see what happens (and how to fix it)"

So let's first build without [UNK] and see the error, then we can fix by adding [UNK].

We'll do it in two steps for learning:

Step 1: Build vocabulary without [UNK] and see the issue.

Step 2: Then add [UNK] and handle unknown words.

But the instructions say to implement the code in the given placeholders.

Let's follow:

We are going to:

Build the vocabulary from the corpus (without [UNK] initially, but then we'll add it to handle OOV)

However, the problem says: "Try a sentence with unseen words and see what happens (and how to fix it)"

So we'll first build the vocabulary without [UNK] and then when we test with an unseen word, we get a KeyError.

Then we can fix by adding [UNK] to the vocabulary.

Let's do:

vocab = sorted(set(all_words))

Then we'll add [UNK] at the beginning.

Then build word2id and id2word.

But note: the corpus is tiny, so we can get all words by:

all_words = []
for sentence in corpus:
words = sentence.split()
all_words.extend(words)

Then we get the unique words and sort them (to have consistent order) and then add [UNK] at the beginning.

Alternatively, we can do:

vocab = sorted(set(all_words))
vocab = ['[UNK]'] + vocab # now [UNK] has ID 0

Then:

word2id = {word: idx for idx, word in enumerate(vocab)}
id2word = {idx: word for idx, word in enumerate(vocab)}

Now, in encode function, we can use:

tokens = text.split()
ids = [word2id.get(token, word2id['[UNK]']) for token in tokens]

But note: we have added [UNK] so every unknown word will map to 0.

Let's code accordingly.

However, the problem says: "YOUR CODE HERE (~6-15 lines of code)" for building vocabulary.

We can do:

all_words = []
for sentence in corpus:
all_words.extend(sentence.split())
unique_words = sorted(set(all_words))
vocab = ['[UNK]'] + unique_words

Then build the mappings.

But wait, the original corpus might have repeated words? We use set to remove duplicates.

Let's implement.

We'll also note: the original corpus has mixed case. For example, "The" and "the" are different.
We have to decide if we want to be case-sensitive. The example corpus has both "The" and "the".

We'll keep it case-sensitive for now.

Let's code accordingly.



=============================================
Charecter Tokenizer
=============================================

We are going to build a character-level tokenizer. We'll include:

All uppercase and lowercase English letters (so 26*2 = 52 letters)

We'll also add two special tokens: one for unknown (if we encounter any non-alphabet character) and one for padding.

Steps:

Create the vocabulary (vocab) which will include:
[UNK] for unknown characters (non-alphabet)
[PAD] for padding
Then all the uppercase and lowercase letters.

Create mappings: char2id and id2char.

Implement encode function:

We'll convert each character in the text to its ID.

If the character is in the vocabulary (i.e., it's a letter), use its ID.

Otherwise, use the [UNK] token.

Implement decode function:

Convert each ID in the list to the corresponding character.

If the ID is not in id2char, we can return a placeholder (like [UNK]) but in our case we have included all 52 letters and two specials, so we should be safe for the given assumption (only uppercase and lowercase letters). However, we might have non-alphabet in the input, so we used [UNK] in encoding, so we must have [UNK] in the decoding as well.

Test the tokenizer.

Note: The problem says "for simplicity, assume we are only using uppercase and lowercase English letters (a-z, A-Z)" but we are also going to handle non-alphabet by [UNK].

Let's code accordingly.

