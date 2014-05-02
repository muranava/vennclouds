Dynamic Wordclouds and Vennclouds
Developed at the Human Language Technology Center of Excellence, Johns Hopkins University
Author: Glen Coppersmith (coppersmith@jhu.edu)
Author: Erin Kelly (elkelly8@gmail.com)
Author: Aleksander Yelskiy (ayelskiy@gmail.com)

If you use this, please cite the following paper:
Glen Coppersmith and Erin Kelly (2014). Dynamic Wordclouds and Vennclouds for Exploratory Data Analysis.
Association for Computational Linguistics Workshop on Interactive Language Learning and Visualization.



[[This README is currently out of data, for usage instructions run:
python dynamic_wordclouds.py --help ]]


This is _RESEARCH_ code, there are likely still bugs and gotchas hiding in the nooks and crannys. If you find one, please do let us know.

NB: this generates (potentially large) encapsulated HTML files, that can be used when disconnected from the internet. Please be certain that you place the generated HTML files in a directory that contains the `offline_source' directory, so the HTML files can find the jQuery libraries used.

---
dynamic_wordclouds.py
---
This houses all of the functions (importable as python function calls) required to make both single and delta dynamic wordclouds.
For usage instructions:
python dynamic_wordclouds.py -h

usage: dynamic_wordclouds.py [-h] [--blue BLUE] [--red RED] [--black BLACK]
                             [--output OUTPUT] [--idf IDF]

Create a delta wordcloud html file.

optional arguments:
  -h, --help       show this help message and exit
  --blue BLUE      Location of the documents for the blue side of a delta
                   wordcloud -- plain text, 1 document per line.
  --red RED        Location of the documents for the red side of a delta
                   wordcloud -- plain text, 1 document per line.
  --black BLACK    Location of the documents for a single wordcloud -- plain
                   text, 1 document per line.
  --output OUTPUT  Where the output html file should be written.
  --idf IDF        Location of an idf vector to be used, as a JSON file of a
                   python dictionary -- see `create_idf_vector.py` to make
                   one. If this argument is omitted, we will generate the idf
                   vector from the red and blue documents.


---
create_idf_vector.py
---
This will create and store an IDF vector from an arbitrary number of text files (one document per line). This is best run on a large number of documents, so as to get a good estimate of the true IDF value of each token. The resulting JSON file can then be passed into dynamic_wordclouds.py to create the wordclouds.
For usage instructions:
python create_idf_vector.py -h

usage: create_idf_vector.py [-h] [--output OUTPUT] --docs [DOCS [DOCS ...]]

Create a JSON idf vector for use with the dynamic wordclouds.

optional arguments:
  -h, --help            show this help message and exit
  --output OUTPUT       Where the output JSON file should be written.
  --docs [DOCS [DOCS ...]]
                        List of text files used to generate the idf vector --
                        one document per line, multiple text files allowed




##############
Example Usage:
##############

1) Single wordcloud:
python dynamic_wordclouds.py --black some_text_file.txt
where `some_text_file.txt' has one document per line. This will calculate IDF and the wordcloud from the same set of documents (this is only advised if there are a large number of documents in this text file).

2) Delta wordcloud ("Venn Cloud"):
python dynamic_wordclouds.py --blue blue.txt --red red.txt
where `blue.txt' and `red.txt' are plain text documents with one document per line. This will calculate IDF and the wordcloud from the same set of documents (this is only advised if there are a large number of documents in these text files).

3) Create an idf vector for use later:
python create_idf_vector  --output this_idf_vector.json blue.txt red.txt some_text_file.txt
where `blue.txt', `red.txt' and `some_text_file.txt' are plain text documents with one document per line. 

4) Use the idf vector previously created to make a wordcloud and store it at venn_cloud.html
python dynamic_wordclouds.py --blue blue.txt --red red.txt --idf this_idf_vector.json --output venn_cloud.html
where `blue.txt', `red.txt' are plain text documents with one document per line, `this_idf_vector.json' was generated by `create_idf_vector.py' as above. 

