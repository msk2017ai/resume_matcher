# RESUME MATCHER
##  THIS APPLICATION IDENTIFIES TO HOW CLOSE THE RESUME IS MATCHING WITH THE JOB DESCRIPTION. 
##  WE CAN USE THIS METHODOLOGY TO IDENTIFY AND MATCH HOW EXTENT THE CANDIDATE PROFILES ARE MATCHING WITH THE JOB DESCRIPTIONS.

```
from docx import Document
from docx.shared import Inches
import nltk
#nltk.download('punkt')
import nltk
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize
```

## READING JOB DESCRIPTION (SAMPLE USED FOR THIS EXPERIMENT)

```
jd = Document('job_description/job_description.docx')
lis = []
job_description =[]
for para in jd.paragraphs:
    lis.append(para.text)
import nltk
nltk.download('punkt')
print(len(lis))
for i in range(len(lis)):
    tokens = nltk.word_tokenize(lis[i])
    job_description.append((tokens))
job_description_list = ' '.join([ls for x in job_description for ls in x])
print(job_description_list)
```

## READING SAMPLE RESUME - A

```
document_a = Document('sample_resumes/Resume_A.docx')
lis = []
textual_a =[]
for para in document_a.paragraphs:
    lis.append(para.text)

print(len(lis))
for i in range(len(lis)):
    tokens = nltk.word_tokenize(lis[i])
    textual_a.append((tokens))
textual_a_list = ' '.join([ls for x in textual_a for ls in x])
print(textual_a_list)
```

```
from docx import Document
from docx.shared import Inches
document_b = Document('sample_resumes/Resume_B.docx')
lis = []
textual_b =[]
for para in document_b.paragraphs:
    lis.append(para.text)
print(len(lis))
for i in range(len(lis)):
    tokens = nltk.word_tokenize(lis[i])
    textual_b.append((tokens))
textual_b_list = ' '.join([ls for x in textual_b for ls in x])
print(textual_b_list)
```

## IDENTIFY AND MATCH RESUME A TO HOW EXTENT THIS MATCHES WITH CURRENT SAMPLE JOB DESCRIPTION

```
# tokenization
X_list = word_tokenize(textual_a_list) 
Y_list = word_tokenize(job_description_list)
  
# sw contains the list of stopwords
sw = stopwords.words('english') 
l1 =[];l2 =[]
X_set = {w for w in X_list if not w in sw} 
Y_set = {w for w in Y_list if not w in sw}
  
# form a set containing keywords of both strings 
rvector = X_set.union(Y_set) 
for w in rvector:
    if w in X_set: l1.append(1) # create a vector
    else: l1.append(0)
    if w in Y_set: l2.append(1)
    else: l2.append(0)
c = 0
  
# cosine formula 
for i in range(len(rvector)):
        c+= l1[i]*l2[i]
cosine = c / float((sum(l1)*sum(l2))**0.5)
print("similarity: ", cosine)
if cosine > 0.1:
    print("THIS RESUME MATCHES WTH JOB REQUIREMENT WITH A SCORE OF = ", cosine)
else:
    print("THIS RESUME DOES NOT MATCH WTH JOB REQUIREMENT, LOW SCORE OF = ", cosine)
```

## IDENTIFY AND MATCH RESUME B TO HOW EXTENT THIS MATCHES WITH CURRENT SAMPLE JOB DESCRIPTION

```
# tokenization
X_list = word_tokenize(textual_b_list) 
Y_list = word_tokenize(job_description_list)
  
# sw contains the list of stopwords
sw = stopwords.words('english') 
l1 =[];l2 =[]
X_set = {w for w in X_list if not w in sw} 
Y_set = {w for w in Y_list if not w in sw}
  
# form a set containing keywords of both strings 
rvector = X_set.union(Y_set) 
for w in rvector:
    if w in X_set: l1.append(1) # create a vector
    else: l1.append(0)
    if w in Y_set: l2.append(1)
    else: l2.append(0)
c = 0
  
# cosine formula 
for i in range(len(rvector)):
        c+= l1[i]*l2[i]
cosine = c / float((sum(l1)*sum(l2))**0.5)
print("similarity: ", cosine)
if cosine > 0.1:
    print("THIS RESUME MATCHES WTH JOB REQUIREMENT WITH A SCORE OF = ", cosine)
else:
    print("THIS RESUME DOES NOT MATCH WTH JOB REQUIREMENT, LOW SCORE OF = ", cosine)