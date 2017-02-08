#working rough draft (very rough, lol)
#so far we find key words and create a file of the url's, where it was found.
#necessary imports.  You may need to download these modules. pip install
#Using python 2.7
import requests
import re
import validators
import csv

url = 'http://www.finviz.com/news.ashx'

#First we pull the url request using the requests module, then use regular expression to pull all urls from the website
response = requests.get(url)
html = response.content
urls2 = re.findall('http[s]?://(?:[a-zA-Z]|[0-9]|[$-_@.&+{}]|[!*\(\),]|(?:%[0-9a-fA-F][0-9a-fA-F]))+', html)
#This creates a list of all urls found
#We can then search each list for one of the keywords
#in our list

newList = []
newList = urls2

#for item in newList:
    #print(item)

key_list = ['single-session', 'immigration' 'research', 'deadlock', 'national security', 'Trump', 'Skeptical', 'decline']#This is for testing, our list is much larger obviously

k = int(0)

for item in newList:
    if not validators.url(item):
        print("invalid url")
    else:
	for key in key_list:
    	    m = re.search(key, item)
    	    if m:
        	print ("found!")
		print (key)
		print(item)
		k = k + 1
		with open('scrapedata.csv', 'w')as f:#use csv module to write to a spreadsheet.  Need work on this
                    writer = csv.writer(f)
		    writer.writerows(item)


print (k)#number of keyword hits
print(len(newList))#number of urls searched.
print(newList)











