## OS 모듈
---
OS 모듈은 Operating System의 약자로서 운영체제에서 제공되는 여러 기능을 파이썬에서 수행할 수 있게 해준다.

1. os.getcwd(): 현재 경로를 얻을 수 있다.
2. os.listdir()
- 현재 경로에 존재하는 파일과 디렉토리 목록이 **리스트**로 구성된 후 반환된다.
- os.listdir()함수의 인자로 경로를 전달하는 경우, **해당 경로**에 존재하는 파일과 디렉토리 목록을 구할 수 있다.
```
files=os.listdir('경로')
len(files) # 해당 경로에 몇개의 파일 또는 디렉토리가 존재하는지 확인할 수 있다.

for x in os.listdir('경로')
  if x.endswith('exe'):
    print(x) # 해당 경로에 있는 파일 목록 중, 문자열이 'exe'로 끝나는 경우의 파일을 출력해준다.
```
3. os.chdir('디렉토리경로'): 디렉토리 변경
4. os.path.dir(path): 경로 중, 디렉토리명만 얻기
```
print(os.path.dirname("/Users/evan/dev/python/web-crawler-py/parsed_data")) # Users/evan/dev/python/web-crawler-py
```
5. os.path.basename(path): 경로 중, 파일명만 얻기
```
print(os.path.basename("/Users/evan/dev/python/web-crawler-py/parsed_data")) # parsed_data
```
6. os.path.split(path): 경로 중, 디렉토리명과 파일명 나누어 얻기, 디렉토리명과 파일명이 리스트 형태로 나온다.
```
dir,file=os.path.split("/Users/evan/dev/python/web-crawler-py/parsed_data")
print(dir, file, spe="\n) 
```
7. os.path.join(path, path1, path2,...)): 경로를 병합하여 새 경로 생성
```
print(os.path.join('cassava/train/train','name')) # 'cassava/train/train/name'
```



