---
layout: post
title:  "Detoxify user prompts"
date:   2023-03-22 00:00:00 +0000
categories: detoxify python pip package user prompt input
---
With the emergence of so many text based ai generative models, there is a initial layer of input prompt validator / filter which detects bias, racist and other inappropriate comments. Building this model, takes time and resources. Should the team focus on the core model or also spend effort on checking for valid inputs?

In this context, there is a helpful open source python package called `detoxify` which helps with detecting bias and other aspects along same lines in an input text. Quoting from [the github page](https://github.com/unitaryai/detoxify){:target="_blank"}:

`Trained models & code to predict toxic comments on 3 Jigsaw challenges: Toxic comment classification, Unintended Bias in Toxic comments, Multilingual toxic comment classification.`

Installation command:
```bash
pip install detoxify
```

Sample code:
```python

from detoxify import Detoxify

# each model takes in either a string or a list of strings

results = Detoxify('original').predict('example text')

results = Detoxify('unbiased').predict(['example text 1','example text 2'])

results = Detoxify('multilingual').predict(['example text','exemple de texte','texto de ejemplo','testo di esempio','texto de exemplo','örnek metin','пример текста'])

# to specify the device the model will be allocated on (defaults to cpu), accepts any torch.device input

model = Detoxify('original', device='cuda')

# optional to display results nicely (will need to pip install pandas)

import pandas as pd

print(pd.DataFrame(results, index=input_text).round(5))
```

Do feel free to go through the limitations shared in the github page. Hope it helps!