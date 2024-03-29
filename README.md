# Page Rank implementation and visualisation

A Simple Python web crawler, Page Ranker, and Visualisation tool.

[![license](https://img.shields.io/github/license/nhnent/tui.editor.svg)]()
[![made-with-python](https://img.shields.io/badge/Made%20with-Python-1f425f.svg)](https://www.python.org/)

This is a set of programs that emulate some of the functions of a 
search engine.  They store their data in a SQLITE3 database named
'spider.sqlite'.  This file can be removed at any time to restart the
process.   

You should install the SQLite browser to view and modify 
the databases from:

http://sqlitebrowser.org/

This program crawls a web site and pulls a series of pages into the
database, recording the links between pages.

Ubuntu: python3 spider.py
Win: spider.py

Enter web url or enter: http://www.dr-chuck.com/
['http://www.dr-chuck.com']
How many pages:2
1 http://www.dr-chuck.com/ 12
2 http://www.dr-chuck.com/csev-blog/ 57
How many pages:

In this sample run, we told to crawl the entered website and retrieve two 
pages from it.  If you restart the program again and tell it to crawl more
pages, it will not re-crawl any pages already in the database.  Upon 
restart it goes to a random non-crawled page and starts there.  So 
each successive run of spider.py is additive.Also if it fails to
retrieve a particular page it moves forth till the requested no. of 
pages are not crawled 

Ubuntu: python3 spider.py 
Win: spider.py

Note: Windows has difficulty in displaying UTF-8 characters
in the console so for each console window you open, you may need
to type the following command before running this code:

    chcp 65001

http://stackoverflow.com/questions/388490/unicode-characters-in-windows-command-line-how



Enter web url or enter: http://www.dr-chuck.com/
['http://www.dr-chuck.com']
How many pages:3
3 http://www.dr-chuck.com/csev-blog 57
4 http://www.dr-chuck.com/dr-chuck/resume/speaking.htm 1
5 http://www.dr-chuck.com/dr-chuck/resume/index.htm 13
How many pages:

You can have multiple starting points in the same database - 
within the program these are called "webs".   The spider
chooses randomly amongst all non-visited links across all
the webs.

If you want to dump the contents of the spider.sqlite file, you can 
run spdump.py as follows:

Ubuntu: python3 spdump.py 
Win: spdump.py

(1, None, 1.0, 3, 'http://www.dr-chuck.com')
(1, None, 1.0, 6, 'http://www.dr-chuck.com/sakai-book')
(1, None, 1.0, 7, 'http://www.dr-chuck.com/obi-sample')
3 rows.

This shows the number of incoming links, the old page rank, the new page
rank, the id of the page, and the url of the page.  The spdump.py program
only shows pages that have at least one incoming link to them.

Once you have a few pages in the database, you can run Page Rank on the
pages using the sprank.py program.  You simply tell it how many Page
Rank iterations to run.

Ubuntu: python3 sprank.py 
Win: sprank.py 

How many iterations:2
1 0.22222222222222224
2 0.14814814814814814
[(3, 1.1111111111111112), (6, 0.9444444444444444), (7, 0.9444444444444444)]

You can dump the database again to see that page rank has been updated:

Ubuntu: python3 spdump.py 
Win: spdump.py 

(1, 1.0, 1.1111111111111112, 3, 'http://www.dr-chuck.com')
(1, 1.0, 0.9444444444444444, 6, 'http://www.dr-chuck.com/sakai-book')
(1, 1.0, 0.9444444444444444, 7, 'http://www.dr-chuck.com/obi-sample')
3 rows.


You can run sprank.py as many times as you like and it will simply refine
the page rank the more times you run it.  You can even run sprank.py a few times
and then go spider a few more pages with spider.py and then run sprank.py
to converge the page ranks for the recently extracted pages as well.

If you re-run the Page Ranking calculations but without re-crawling the Web
pages ,you can use the spreset.py Program

Ubuntu: python3 spreset.py 
Win: spreset.py 

All pages set to a rank of 1.0

Ubuntu: python3 sprank.py 
Win: sprank.py 

How many iterations:70
How many iterations:69 
1 0.04389574759945125
2 0.0292638317329675
3 0.01950922115531169
4 0.013006147436874485
.
.
.
.
66 1.5728159515523052e-13
67 1.0495308326123147e-13
68 7.009208028800155e-14
69 4.677739677087326e-14
70 4.029295415837926e-12
[(3, 1.2000000000000277), (6, 0.8999999999999857), (7, 0.8999999999999857)]

For each iteration of the page rank algorithm it prints the average
change per page of the page rank.   The network initially is quite 
unbalanced and so the individual page ranks are changing wildly.
But in a few short iterations, the page rank converges.  You 
should run prank.py long enough that the page ranks converge.

To visualize the current top pages in terms of page rank,you can run 
spjson.py to write the pages out in JSON format to be viewed in a
web browser.

Ubuntu: python3 spjson.py 
Win: spjson.py 

Creating JSON output on spider.js...
How many nodes? 30
Open force.html in a browser to view the visualization

You can view this data by opening the file force.html in your web browser.  
This shows an automatic layout of the nodes and links.  You can click and 
drag any node and you can also double click on a node to find the URL
that is represented by the node.

This visualization is provided using the force layout from:

http://mbostock.github.com/d3/

If you rerun the other utilities and then re-run spjson.py - you merely
have to press refresh in the browser to get the new data from spider.js.

## Terminal

- `spider.py` running for dr-chuck.com.
<p align="center">
  <a href="" rel="noopener">
 <img width=500px src="./assets/spider.png"></a>
</p>
- `spdump.py` running for dr-chuck.com.
<p align="center">
  <a href="" rel="noopener">
 <img width=500px src="./assets/spdump_demo.png"></a>
</p>
- `sprank.py` running for dr-chuck.com.
<p align="center">
  <a href="" rel="noopener">
 <img width=500px src="./assets/spdump_reset_rank.png"></a>
</p>
- `spdump.py` `spreset.py` `sprank.py`  running for dr-chuck.com.
<p align="center">
  <a href="" rel="noopener">
 <img width=500px src="./assets/multiplefile_demo.png"></a>
</p>


Similarily we can rank pages of various websites and visualise them using D3.js 


## Visualization of website using D3.js

- Wikipedia
<p align="center">
  <a href="" rel="noopener">
 <img width=500px src="./assets/wiki.png"></a>
</p>
<p align="center">
  <a href="" rel="noopener">
 <img width=500px src="./assets/wiki-italy.png"></a>
</p>

- Coursera
<p align="center">
  <a href="" rel="noopener">
 <img width=500px src="./assets/coursera.png"></a>
</p>

- dr-chuck.com
<p align="center">
  <a href="" rel="noopener">
 <img width=500px src="./assets/dr-chuck.jpg"></a>
</p>
<p align="center">
  <a href="" rel="noopener">
 <img width=500px src="./assets/python-chuck.jpg"></a>
</p>
