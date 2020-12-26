# Blog-Beiträge automatisch übersetzen
[:de:](https://github.com/joatom/ai_curious/blob/master/_posts/blog_translator.md) <--> [:us:](https://joatom.github.io/ai_curious/markdown/2020/12/26/blog-translator.html)

> Achtung! Dieser Text wurde automatisch übersetzt!

Da ich in meinem ersten [Blog-Beitrag](https://datamuni.com/@joatom/a-handful-of-bricks-from-sql-to-pandas) soviele Fehler auf Englisch gemacht habe, schreibe ich diesen Beitrag auf Deutsch und lasse ihn automatisch übersetzen.

Zur Übersetzung verwende ich das populäre NLP-Framework von [huggingface.co](https://huggingface.co/transformers/index.html). Auf ihrer Webseite ist ein einfaches [Beispiel](https://huggingface.co/transformers/model_doc/marian.html) um eine Übersetzungsanwendung zu implementieren. Und diese werde ich verwenden.

Wie erwartet, hat es nicht auf Anhieb funktioniert die Markdown-Syntax bei der Übersetzung immer korrekt zu übernehmen.
Also habe ich zu Beginn und hinterher noch ein paar Anpassungen vornehmen müssen.

Den Code (inkl. Vor- und Nachbearbeitung), den ich für die Übersetzung der Markdown-Dateien verwendet habe, findet ihr [hier](https://github.com/joatom/blog-resources/tree/main/blog_translator).
Aber da es ja nur ein paar Zeilen Code sind, können wir sie uns auch eben hier anschauen:

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
src_text = [s.replace('\n',' <<eol>>') for s in src_text]

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
tgt_text = [s.replace('<<eol>>', '',) for s in tgt_text]
## remove space between ] ( to get the md link syntax right
tgt_text = [s.replace('] (', '](',) for s in tgt_text]

# write english blog post
with open('2020-12-26-blog-translator.md', 'w') as f_out:
    for line in tgt_text:
        f_out.write("%s\n" % line)
f_out.close()
```

Da das meine erster NLP-Anwendung ist, habe ich es bei diesem *Hello World*-Code belassen. Sicherlich gibt es geschickter Wege, um die Markdown-Syntax in *tokenizer* abzubilden. Vielleicht schreibe ich ein Follow up, wenn ich es rausgefunden habe.

Übrigens, die Übersetzung hat mich ebenfallls dazu gebracht meinen deutschen Schreibstil anzupassen.
Beispielsweise funktioniert Sarkasmus nach der Übersetzung nicht so gut, also hab ich es vermieden.
Außerdem kommt es auch häufig auf die richtige Wortwahl an (z.B. gibt es kein Markdown-Befehl, jedoch gibt es Markdown-Syntax).

Viele Grüße

Johannes & der Roboter