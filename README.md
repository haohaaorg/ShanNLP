# ShanNLP: Shan Natural Language Processing
**experimental project inspired by [PythaiNLP](https://github.com/PyThaiNLP/pythainlp)**

## Current State
- [ ] corpus dict word: 19904 words (60% corvered and need more to collected)

## Word Tokenization method
- [x] maximal_matching
- [x] pythainlp (newmm)

## TODO
- [ ] mining more shan words, poem
- [ ] experiment more method to tokenize
  - [ ] word tokenize
  - [ ] sentent tokenize
  - [ ] subword_tokenize
  - [ ] tokenize with deep learning
- [ ] spelling check
- [ ] pos tagging
- [ ] translation
- [ ] word_vector

## USAGE
### Install
```python
# this project using pythainlp dependecy
# - Trie data structure
# - newmm (experimental)

pip install -r requirements.txt
# or pip install pythainlp
```

### Tokenization

#### maximal_matching bruce-force
```python
from shannlp import word_tokenize

# start measure execute time
# start = time.time()

# # Example usage
input_text = "တိူၵ်ႈသွၼ်လိၵ်ႈသင်ၶၸဝ်ႈ တီႈဝဵင်းမိူင်းၶၢၵ်ႇ တႄႇပိုတ်ႇသွၼ်ႁဵၼ်းလိၵ်ႈ ပဵၼ်ပွၵ်ႈၵမ်းႁႅၵ်း မီးသင်ၶၸဝ်ႈ မႃးႁဵၼ်း 56 တူၼ်။"

# default tokenizer engine="mm" (maximal_matching)
print(word_tokenize(input_text))

# end measure execute time
# end = time.time()
# print(end - start)

# output
# ['တိူၵ်ႈ', 'သွၼ်လိၵ်ႈ', 'သင်ၶ', 'ၸဝ်ႈ', ' ', 'တီႈ', 'ဝဵင်း', 'မိူင်းၶၢၵ်ႇ', ' ', 'တႄႇ', 'ပိုတ်ႇ', 'သွၼ်', 'ႁဵၼ်းလိၵ်ႈ', ' ', 'ပဵၼ်', 'ပွၵ်ႈ', 'ၵမ်း', 'ႁႅၵ်း', ' ', 'မီး', 'သင်ၶ', 'ၸဝ်ႈ', ' ', 'မႃး', 'ႁဵၼ်း', ' ', '56', ' ', 'တူၼ်', '။']
# 0.7220799922943115
```

#### pythainlp newmm
```python
from shannlp.corpus import shan_words
from pythainlp import Tokenizer

_word = Tokenizer(shan_words())

input_text = "တိူၵ်ႈသွၼ်လိၵ်ႈသင်ၶၸဝ်ႈ တီႈဝဵင်းမိူင်းၶၢၵ်ႇ တႄႇပိုတ်ႇသွၼ်ႁဵၼ်းလိၵ်ႈ ပဵၼ်ပွၵ်ႈၵမ်းႁႅၵ်း မီးသင်ၶၸဝ်ႈ မႃးႁဵၼ်း 56 တူၼ်။"

print(_word.word_tokenize(input_text))

# output
# ['တိူၵ်ႈ', 'သွၼ်လိၵ်ႈ', 'သင်ၶ', 'ၸဝ်ႈ', ' ', 'တီႈ', 'ဝဵင်း', 'မိူင်းၶၢၵ်ႇ', ' ', 'တႄႇ', 'ပိုတ်ႇ', 'သွၼ်', 'ႁဵၼ်းလိၵ်ႈ', ' ', 'ပဵၼ်', 'ပွၵ်ႈ', 'ၵမ်း', 'ႁႅၵ်း', ' ', 'မီး', 'သင်ၶ', 'ၸဝ်ႈ', ' ', 'မႃး', 'ႁဵၼ်း', ' ', '56', ' ', 'တူၼ်', '။']
```

### Digit convert
```python
from shannlp.util import digit_to_text

print(digit_to_text("မႂ်ႇသုင်ပီမႂ်ႇတႆး ႒႑႑႗ ၼီႈ"))

# output
# မႂ်ႇသုင်ပီမႂ်ႇတႆး သွင်ၼိုင်ႈၼိုင်ႈၸဵတ်း ၼီႈ
```

### Date converter
```python
from shannlp.util import shanword_to_date
import datetime

print(f"မိူဝ်ႈၼႆႉ: {datetime.date.today()}")
print(f"မိူဝ်ႈဝၼ်းသိုၼ်း {shanword_to_date('မိူဝ်ႈဝၼ်းသိုၼ်း')}")

# output
# မိူဝ်ႈၼႆႉ: 2023-06-15
# မိူဝ်ႈဝၼ်းသိုၼ်း 2023-06-13 00:51:14.597118
```

#### years convert
```python
from shannlp.util import convert_years

# ပီ AD -> ပီတႆး
print(convert_years(2023, "ad", "mo"))
# output 2117

# ပီတႆး -> ပီပုတ်ႉထ
print(convert_years(2117, "mo", "be"))
# output 2566

# ပီပုတ်ႉထ -> ပီၵေႃးၸႃႇ
print(convert_years(2566, "be", "ga"))
# output 1385
```

### Keyboard
```python
from shannlp.util import eng_to_shn, shn_to_eng

print(eng_to_shn("rgfbokifcMj"))
# output မႂ်ႇသုင်ၶႃႈ

print(shn_to_eng("ေၺၺူၼ"))
# output apple
```