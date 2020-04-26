```python
import pandas as pd
import requests 
from bs4 import BeautifulSoup
```

```python

def obtem_aparicoes(url):
  html = requests.get(url)
  bs_obj = BeautifulSoup(html.text, 'lxml')
  h4 = bs_obj.find({'h4': 'Aparições em títulos da série'})
  aparicoes = [i.text for i in h4.find_next().find_all('a')]
  return aparicoes

def obtem_personagem(url):
  aparicoes - obtem_aparicoes(url)
  nome = [url.split("/")[-2] * len(aparicoes)]
  return pd.DataFrame({"mome": nome, "aparicao": aparicoes})


#pegar todos os links
def get_all_links(url):
  html = requests.get(url)
  bs_obj = BeautifulSoup(html.text, 'lxml')
  links = [] 
  h3 = bs_obj.find_all('h3', style='padding.left: 30px;')
  for i in h3:
    links += [ j['href'] for j in i.find_next().find_all('a')]
  return links 
  ```
  
  ```python
  url = "http://www.residentevildatabase.com/personagens/"
links = get_all_links(url)
```

```python
df = pd.DataFrame()
for l in links:
  df = pd.concat([df, obtem_personagem(l) ] )
  
  ```
  
  ```python
  df.to_excel('data_personagem.xlsx')
  ```
  
  
  
  
  
  
