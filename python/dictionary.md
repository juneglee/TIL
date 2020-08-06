# dictionary

# 리스트와 딕셔너리 비교
|   | 리스트 | 딕셔너리 |
| --- | --- | --- |
| 정의 | 인덱스를 기반으로 값을 저장하는 것 | 키를 기반으로 값을 저장하는 것 |
| 선언 형식 | list_a = [] | dict_a = {} |
| 사용 예 | list_a[1] | dict_a["name"] |

```
변수 = {
 키 : 값,
 키 : 값,
 ...
 키 : 값
}
```
```python
dict_a = {
    "name1" : "user1",
    "name2" : "user2"
}
print(dict_a["name1"]) # user1
print(dict_a["name2"]) # user2
```

### 리스트와 딕셔너리를 값으로 넣기 
```python
dict_b = {
    "dirctor" : ["안소니","조"],
    "cast" : ["아이언맨","타노스","헐크","토르"]
}
print(dict_b) # {'dirctor': ['안소니', '조'], 'cast': ['아이언맨', '타노스', '헐크', '토르']}
print(dict_b["dirctor"]) # ['안소니', '조']
```

### 딕셔너리의 요소에 접근하기 
```python
dictionary = {
    "name": "7D 건조 망고",
    "type": "당절임",
    "ingredient": ["망고", "설탕", "메타중아황산나트륨", "치자황색소"],
    "origin": "필리핀"
}

print("name:", dictionary["name"]) # name: 7D 건조 망고
print("type:", dictionary["type"]) # type: 당절임
print("ingredient:", dictionary["ingredient"]) # ingredient: ['망고', '설탕', '메타중아황산나트륨', '치자황색소']
print("origin:", dictionary["origin"]) # origin: 필리핀
print("--------------------------------------------")
```

### 값 변경
```python
dictionary["name"] = "8D 건조 망고"
print("name:", dictionary["name"]) #  name: 8D 건조 망고
```

### 딕셔너리 요소에 추가 : 딕셔너리[새로운 키] = 새로운 값
```python
dictionary = {}
print("요소 추가 이전:", dictionary)
dictionary["name"] = "새로운 이름"
dictionary["head"] = "새로운 정신"
dictionary["body"] = "새로운 몸"
print("요소 추가 이후:", dictionary)
```

### 딕셔너리 요소에 제거 : del
```python
dictionary2 = {
    "name": "7D 건조 망고",
    "type": "당절임"
    }

print("요소 제거 이전:", dictionary2) # 요소 제거 이전: {'name': '7D 건조 망고', 'type': '당절임'}
del dictionary2["name"]
del dictionary2["type"]
print("요소 제거 이후:", dictionary2) # 요소 제거 이후: {}
```

### 딕셔너리 내부에 키가 있는지 확인
: in 키워드를 사용하여 내부에 키가 있는지 없는지 확인
```python
dictionary = {
    "name": "7D 건조 망고",
    "type": "당절임",
    "ingredient": ["망고", "설탕", "메타중아황산나트륨", "치자황색소"],
    "origin": "필리핀"
}
key = input("> 접근하고자 하는 키: ")
if key in dictionary:
    print(dictionary[key])
else:
    print("존재하지 않는 키에 접근하고 있습니다.")
```

### 딕셔너리 만들 때 주의할 사항
1. Key는 고유한 값이므로 중복되는 Key 값을 설정해 놓으면 하나를 제외한 나머지 것들이 모두 무시
```python
a = {1:'a', 1:'b'}
print(a) # {1: 'b'} 
```
2. Key에 리스트는 쓸 수 없다
```python
a = {[1,2] : 'hi'}
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

### 딕셔너리 관련 함수들
- Key 리스트 만들기 : keys
```python
a = {'name': 'pey', 'phone': '0119993323', 'birth': '1118'}
print(a.keys()) # dict_keys(['name', 'phone', 'birth'])
# 리스트로 반환하는 방법 : list 
list(a.keys()) # ['name', 'phone', 'birth']
```

- Value 리스트 만들기 : values
```python
a.values() # dict_values(['pey', '0119993323', '1118'])
```

- Key, Value 쌍 얻기 : items
```python
a.items() # dict_items([('name', 'pey'), ('phone', '0119993323'), ('birth', '1118')])
```

- Key: Value 쌍 모두 지우기 : clear
```python
a.clear()
print(a) # {}
```

- Key로 Value얻기 : get
```python
a = {'name':'pey', 'phone':'0119993323', 'birth': '1118'}
print(a.get('name')) # 'pey'
# 존재하지 않는 키에 접근하는 상황에서 두번째 대처 방법으로는 딕셔너리의 get()
value = dictionary.get("none")
print("값:", value)
if value == None:
    print("존재하지 않는 키에 접근했었습니다.")
```

- 해당 Key가 딕셔너리 안에 있는지 조사하기 : in
```python
a = {'name':'pey', 'phone':'0119993323', 'birth': '1118'}
'name' in a
# True
```