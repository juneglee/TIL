# regularExpression

## Regular Expression

## 정규 표현식 \(Regular Expression\)

| 특수문자 | 설명 |
| :--- | :--- |
| . | 한 개의 임의의 문자 |
| ? | 앞의 문자가 존재할 수도 있고, 존재하지 않을 수도 있다 |
| \* | 앞의 문자가 무한개로 존재할 수도 있고, 존재하지 않을 수도 있습니다. |
| + | 앞의 문자가 최소 한 개 이상 존재 \(문자가 1개 이상\) |
| ^ | 뒤의 문자로 문자열이 시작됩니다. |
| $ | 앞의 문자로 문자열이 끝납니다. |
| {숫자} | 숫자만큼 반복 |
| {숫자1, 숫자2} | 숫자1 이상 숫자2 이하만큼 반복 |
| {숫자,} | 숫자 이상만큼 반복 |
| \[문자\] | 문자들 중 한개의 문자와 매치 |
|  | 해당 문자를 제외한 문자를 매치 |

### . 한 개의 임의의 문자

```python
r = re.compile("a.c")
print(r.search("abd")) # None
print(r.search("abc")) # <re.Match object; span=(0, 3), match='abc'>
```

### ? 앞의 문자가 존재 or 미존재

```python
r = re.compile("abc?") # c는 없어도 되고, 있더도 되지만, a와 b는 반드시 있어야 한다. 이때 abc는 하나만 존재해야 한다
print(r.search("abc")) # <re.Match object; span=(0, 3), match='abc'>
print(r.search("ab")) # <re.Match object; span=(0, 2), match='ab'>
```

### \* 앞의 문자가 0개 이상

```python
r = re.compile("ab*c") # b 는 0개 이상이라서 있어도 되고 없어도 되며, 마찬가지로 b를 제외한 a c는 하나만 존재 
print(r.search("ac")) # <re.Match object; span=(0, 2), match='ac'>
print(r.search("abc")) # <re.Match object; span=(0, 3), match='abc'>
print(r.search("abbbc")) # <re.Match object; span=(0, 5), match='abbbc'>
```

### + 앞의 문자가 1개 이상

```python
r = re.compile("ab+c")
print(r.search("ac")) # None
print(r.search("abc")) # <re.Match object; span=(0, 3), match='abc'>
print(r.search("abbbc")) # <re.Match object; span=(0, 5), match='abbbc'>
```

### ^ 시작되는 글자를 지정

```python
r = re.compile("^bc")
print(r.search("abc")) # None
print(r.search("bc")) # <re.Match object; span=(0, 2), match='bc'>
```

### {숫자} 해당 문자를 숫자만큼 반복

```python
r = re.compile("ab{2}c")
print(r.search("abc")) # None
print(r.search("abbc")) # <re.Match object; span=(0, 4), match='abbc'>
print(r.search("abbbc")) # None
```

### {숫자1, 숫자2} 해당 문자를 숫자1 이상, 숫자2 이하만큼 반복

```python
r = re.compile("ab{2,4}c")
print(r.search("abc")) # None
print(r.search("abbc")) # <re.Match object; span=(0, 4), match='abbc'>
print(r.search("abbbc")) # <re.Match object; span=(0, 5), match='abbbc'>
print(r.search("abbbbc")) # <re.Match object; span=(0, 6), match='abbbbc'>
print(r.search("abbbbbc")) # None
```

### {숫자,} 해당 문자를 숫자 이상 만큼 반복

```python
r = re.compile("ab{2,}c")
print(r.search("abc")) # None
print(r.search("abbc")) # <re.Match object; span=(0, 4), match='abbc'>
print(r.search("abbbc")) # <re.Match object; span=(0, 5), match='abbbc'>
print(r.search("abbbbc")) # <re.Match object; span=(0, 6), match='abbbbc'>
print(r.search("abbbbbc")) # <re.Match object; span=(0, 7), match='abbbbbc'>
```

### \[문자\] 문자들 중 한개의 문자와 매치

* \[a-zA-Z\]는 알파벳 전부를 의미, \[0-9\]는 숫자 전부를 의미

```python
r = re.compile("[abc]")
print(r.search("a")) # <re.Match object; span=(0, 1), match='a'>
print(r.search("d")) # None
```

###  제외한 모든 문자를 매치

```python
r = re.compile("[^abc]")
print(r.search("a")) # None
print(r.search("d")) # <re.Match object; span=(0, 1), match='d'>
```

### 정규 표현식 문자 규칙

| 문자규칙 | 설명 |
| :--- | :--- |
| \ | 역 슬래쉬 문자 자체를 의미 |
| \d | 모든 숫자를 의미, \[0-9\]와 동일한 의미 |
| \D | 숫자를 제외한 모든 문자를 의미, 와 동일한 의미 |
| \s | 공백을 의미, \[\t\n\r\f\v\]와 동일한 의미 |
| \S | 공백을 제외한 문자를 의미, 와 동일한 의미 |
| \w | 문자 또는 숫자를 의미, \[a-zA-Z0-9\]와 동일한 의미 |
| \W | 문자 또는 숫자가 아닌 문자를 의미, 와 동일한 의미 |

