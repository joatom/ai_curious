---
toc: true
layout: post
description: How to translate a German blog post to English.
categories: [NLP]
title: Automatically translate blog posts
---

# Automatically translate blog posts 
[:de:](https://github.com/joatom/ai_curious/blob/master/_posts/blog_translator.md) <-> [:us:](https://joatom.github.io/ai_curious/markdown/2020/12/26/blog-translator.html) 

> Attention! This text has been automatically translated! 

Since I made so many mistakes in my first [Blog post](https://datamuni.com/@joatom/a-handful-of-bricks-from-sql-to-pandas), I write this post in German and have it automatically translated. 

For translation I use the popular NLP framework of [huggingface.co](https://huggingface.co/transformers/index.html). On their website is a simple [example](https://huggingface.co/transformers/model_doc/marian.html) to implement a translation application and I will use it. 

As expected, the Markdown syntax does not immediately work correctly when translating. 
So I had to make some adjustments at the beginning and afterwards. 

The code (including pre- and post-processing) I used for the translation of the markdown files can be found [here](https://github.com/joatom/blog-resources/tree/main/blog_translator). 
But since it's just a few lines of code, we can also look at it here: 

```python 
from transformers import MarianMTModel, MarianTokenizer 
 
# load pretrained model and tokenizer 
model_name = 'Helsinki-NLP/opus-mt-de-en' 
tokenizer = MarianTokenizer.from_pretrained(model_name) 
model = MarianMTModel.from_pretrained(model_name) 
 
# load german block post 
f_in = open("blog_translator_de.md", "r") 
src_text = f_in.readlines() 
f_in.close() 
 
# preprocessing 
## line break (\n) results to "I don't know."  We make it more specific: 
src_text = [s.replace('\n',' ') for s in src_text] 
 
## remove code block 
code = [] 
inside_code_block = False 
for i, line in enumerate(src_text): 
    if line.startswith('```') and not inside_code_block: 
        # entering codeblock 
        inside_code_block = True 
        code += [line] 
        src_text[i] = '<<code_block>>' 
    elif inside_code_block and not line.startswith('```'): 
        code += [line] 
        src_text[i] = '<<code_block>>' 
    elif inside_code_block and line.startswith('```'): 
        # leaving code block 
        code += [line] 
        src_text[i] = '<<code_block>>' 
        inside_code_block = False 
 
# translate 
translated = model.generate(**tokenizer.prepare_seq2seq_batch(src_text, return_tensors="pt")) 
tgt_text = [tokenizer.decode(t, skip_special_tokens=True) for t in translated] 
 
# postprocessing 
## replace code_blog tags with code 
for i, line in enumerate(tgt_text): 
    if line == '<<code_block>>': 
        tgt_text[i] = code.pop(0) 
 
## remove the eol (but keep empty list entries / lines) 
tgt_text = [s.replace('', '',) for s in tgt_text] 
## remove space between ]( to get the md link syntax right 
tgt_text = [s.replace('](', '](',) for s in tgt_text] 
 
# write english blog post 
with open('2020-12-26-blog-translator.md', 'w') as f_out: 
    for line in tgt_text: 
        f_out.write("%s\n" % line) 
f_out.close() 
``` 

Since this is my first NLP application, I left it with this *Hello World* code. Surely there are clever ways to map the markdown syntax in *tokenizer*. Maybe I'll write a follow up when I find out. 

By the way, the translation just made me adapt my German writing style. 
For example, sarcasm doesn't work so well after translation, so I avoided it. 
Also, it often depends on the correct choice of words (e.g. there is no markdown command, but there is markdown syntax). <<eol>

Best regards 

Johannes & the Robot
