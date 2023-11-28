# Basics

## Subword tokenizers

word split 방식으로 단어들을 구분해서 encoding하는 기존의 방식에서는 oov(out of vocabulary) 문제가 발생하였습니다. 이를 해결하기 위해 subword segmentation방식이 도입되었습니다.

subword 방식은 하나의 단어를 여러 subword로 분리해서 단어를 인코딩 및 임베딩하겠다는 의도를 가진 preprocess 작업입니다.

- birthday = birth + day

서브워드 토크나이저의 주요 알고리즘은 다음과 같습니다.

1. Byte Pair Encoding
2. SentencePiece
3. Huggingface의 Tokenizers

### BPE
> Byte pair encoding

- **char -> vocabulary하는 bottom up방식의 subword segmentation 알고리즘**

BPE알고리즘은 단어들을 1글자씩 쪼갠뒤, iteration을 돌며, 새로운 Byte pair들을 만들어가는 bottom-up방식의 알고리즘입니다. 

- Byte는 문자, Byte pair는 (문자1, 문자2)입니다.
- iteration 마다 가장 많이 사용된 byte pair를 새로운 문자로 등록합니다.

```
# initial 
aaabdaaabac

# 1st iteration
ZabdZabac
Z=aa

# 2nd iteration
ZYdZYac
Y=ab
Z=aa

# 3rd iteration
XdXac
X=ZY
Y=ab
Z=aa
```

위의 예시에서는 X,Y,Z,d,a,c를 얻었습니다.
