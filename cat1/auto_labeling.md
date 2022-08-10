---
jupyter:
  kernelspec:
    display_name: Python 3.8.0 64-bit
    language: python
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.8.0
  nbformat: 4
  nbformat_minor: 2
  orig_nbformat: 4
  vscode:
    interpreter:
      hash: 52cec8aaadfad774486218c8a56524f5464b2e7c2989816453def1b1836c7aed
---

::: {.cell .markdown}
## Half Labelling
:::

::: {.cell .code execution_count="58"}
``` {.python}
import pandas as pd
import os

# masukkan dulu direktori dataset yang ingin di label
path = 'G:\My Drive\.project_file\dataset/2022-07-25'

if not os.path.exists(path+'/all_zero'):
    os.mkdir(path+'/all_zero')
if not os.path.exists(path+'/give_edit'):
    os.mkdir(path+'/give_edit')

list_dir = os.listdir(path)

for x in ['terminal_msg.txt','give_edit','all_zero']:
    list_dir.remove(x)
```
:::

::: {.cell .code execution_count="59"}
``` {.python}
for filename in list_dir:
    df = pd.read_csv(path+'/'+filename, sep=',')

    if len(df['bid[1]'].unique()) > 3:
        df['label'] = ''
        df.to_csv(path+'/give_edit/'+filename, sep=';', index=False)
        
    else:
        df['label'] = 0
        df.to_csv(path+'/all_zero/'+filename, sep=';', index=False)
        
    if os.path.exists(path+'/'+filename):
        os.remove(path+'/'+filename)
```
:::

::: {.cell .markdown}
## Full Labelling
:::

::: {.cell .code execution_count="1"}
``` {.python}
import pandas as pd
import os

# masukkan dulu direktori dataset yang ingin di label
path = 'G:\My Drive\.project_file\dataset/2022-07-22 - Copy'

if not os.path.exists(path+'/all_zero'):
    os.mkdir(path+'/all_zero')
if not os.path.exists(path+'/give_edit'):
    os.mkdir(path+'/give_edit')

list_dir = os.listdir(path)

for x in ['terminal_msg.txt','give_edit','all_zero']:
    list_dir.remove(x)
```
:::

::: {.cell .code}
``` {.python}
for filename in list_dir:
    df = pd.read_csv(path+'/'+filename, sep=',')

    if len(df['bid[1]'].unique()) > 3:
        df['label'] = ''
        for index, rows in df.iterrows():
            print(rows['column'])
        df.to_csv(path+'/give_edit/'+filename, sep=';', index=False)
        
    else:
        df['label'] = 0
        df.to_csv(path+'/all_zero/'+filename, sep=';', index=False)
```
:::
