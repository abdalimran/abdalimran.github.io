---
layout: post
title: Fuzzy word replace from string in Python
category: 
    - "Miscellaneous"
---

Have you ever faced problems like the following?

You are given a string, for example `"Apple MacBook Pro appl"`. Now you have to remove the word `"Apple"` from the string.
You can easily use python's default `replace()` function to do that. It'll only match and replace the words that exactly matches to `Apple`. But it is required that you also remove the words that might be misspelled, like `appl`. How can we do that?

Fuzzy string matching techniques come into play here. We can solve this problem in 2 ways. One is through using Python's default `difflib` library, and the other one is through using `rapidfuzz`, a fuzzy string matching library.

Below I've given codes for both of the approaches.

**Using difflib:**
{% highlight python %}
import difflib

def fuzzy_replace(word, string):
    '''
    Returns the cleaned string.

            Parameters:
                    word (str): word to be replaced
                    string (str): given string from where we should remove the word

            Returns:
                    string (str): the cleaned string.
    '''
    tokens = string.split()
    matches = difflib.get_close_matches(word=word, possibilities=tokens, n=len(tokens), cutoff=0.6)
    return ' '.join(filter(lambda x: x not in matches, tokens))
{% endhighlight %}

**Using rapidfuzz:**

To use rapidfuzz, we need to install it using the following command
{% highlight python %}
pip install rapidfuzz
{% endhighlight %}

Now, let's implement the function using rapidfuzz.

{% highlight python %}
from rapidfuzz import process, fuzz

def fuzzy_replace(word, string):
    '''
    Returns the cleaned product name as string.

            Parameters:
                    word (str): brand name as string
                    string (str): product name as string

            Returns:
                    product name (str): the cleaned product name as string.
    '''
    tokens = string.split()
    matches = process.extract(query=word, choices=tokens, scorer=fuzz.WRatio, score_cutoff=60.0, limit=len(tokens))
    idx_matches = [m[2] for m in matches]
    return ' '.join(filter(lambda token_idx: tokens.index(token_idx) not in idx_matches, tokens))
{% endhighlight %}

To learn more about rapidfuzz's functions please visit [here](https://maxbachmann.github.io/RapidFuzz/process.html) 

Now, if we use the function we can see the output as follows:

{% highlight python %}
word = "Apple"
string = "Apple MacBook Pro appl"

print(fuzzy_replace(word, string))
{% endhighlight %}

```
Output: MacBook Pro
```
