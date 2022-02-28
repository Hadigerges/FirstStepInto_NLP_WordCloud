# FirstStepInto_NLP_WordCloud
First Step Into NLP: basic NLP code in Python that analyses a web page and outputs a WordCloud

Original file is located at
    https://colab.research.google.com/drive/1d-DV5alcPjdLJgdbeJ5wPk45mxaVC_DD
"""

import nltk
import urllib3
import matplotlib.pyplot as plt
import operator
from bs4 import BeautifulSoup

allText = ""
for line in lines:
  allText += " "+line

allText

http = urllib3.PoolManager()
url1 = 'https://www.fges.fr/cursus-universitaire/licence-sts/master-data-intelligence-artificielle/'
url2 = 'https://www.univ-lille.fr/'
url3 = 'https://www.renault.fr/vehicule-hybride/e-tech-hybride.html'
response = http.request('GET', url1) #we can include url2 or ulr3 to change the input

htmlContent = BeautifulSoup(response.data,'html.parser')
htmlContent.contents

#Get text from html
html_content2 = htmlContent.get_text()
html_content2

tokens = html_content2.split()
tokens = htmlContent2.split()
print(tokens[0:100])


for script in htmlContent(["script","style"]):
  script.decompose()

html_content2 = htmlContent.get_text()
tokens = html_content2.split()
tokens

freq_dis = {}

for word in tokens:
  if word in freq_dis:
    freq_dis[word] += 1
  else:
    freq_dis[word] = 1
freq_dis

sorted_freq_dist = sorted(freq_dis.items(), key=operator.itemgetter(1), reverse=True)
sorted_freq_dist

plt.figure(figsize=(20, 8))
Freq_dist_nltk = nltk.FreqDist(tokens)
Freq_dist_nltk.plot(50, cumulative=False)

nltk.download("stopwords")

stopwords = nltk.corpus.stopwords.words("english")
stopwords

print(len(stopwords))

clean_tokens = [tok for tok in tokens if len(tok.lower())>1 and (tok.lower() not in stopwords)]
clean_tokens

plt.figure(figsize=(20, 8))
Freq_dist_nltk1 = nltk.FreqDist(clean_tokens)
Freq_dist_nltk1.plot(50, cumulative=False)

from wordcloud import WordCloud

wc = WordCloud().generate_from_frequencies(Freq_dist_nltk1)

plt.imshow(wc, interpolation='bilinear')
plt.axis("off")
