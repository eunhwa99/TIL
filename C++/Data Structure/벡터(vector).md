## Vector
---
vector는 C++ STL(표준라이브러리)에 있는 컨테이너로, 사용자가 사용하기 편하게 정의된 class 이다. vector를 생성하면, 메모리 heap에 생성되며 동적할당된다.

### Vector의 초기화
1. vector<자료형>변수명: 벡터 생성
2. vector<자료형>변수명(숫자): 숫자만큼 백터 생성 후, 0으로 초기화
3. vector 변수명(n,x): x값으로 초기화된 n개의 원소를 갖는 벡터 생성
4. vector<자료형>변수명={변수1,변수2,변수3,...}: 벡터 생성 후 오른쪽 변수 값으로 초기화
5. vector<자료형>변수명[]={{변수1, 변수2},{변수3, 변수4}}: 벡터 배열(2차원 벡터)선언 및 초기화 (열은 고정, 행은 가변)
6. vector<vector<자료형>>변수명: 2차원 벡터 생성 (열과 행 모두 가변)
7. vector<자료형>변수명.assign(범위, 초기화 값): 벡터의 범위 내에서 해당 값으로 초기화
```
vector<int> v;        //int형 백터 생성
vector<int>v(4);    //int형 백터 생성 후 크기를 4로 할당(모든 백터요소 0으로 초기화), 가변 가능(push_back으로)

vector<bool>visited;
visted=vector<bool>(adj.size(),false); // adj.size()만큼 false로 visited 벡터를 초기화한다.

vector<int>v = { 1, 2, 3};        //int형 백터 생성 후 1, 2, 3 으로 초기화
vector<int>v[] = {{ 1, 2}, {3, 4}};        //int형 백터 배열 생성(행은 가변이지만 열은 고정)
vector<vector<int>> v;        //2차원 백터 생성(행과 열 모두 가변)
vector<int> v = { 1, 2, 3, 4, 5};        //백터 범위를 5로 지정하고 정수 10으로 초기화
v.assign(5, 10);    //output : 10 10 10 10 10
```

### Vector의 Iterators
1. v.begin(): 벡터 시작점의 주소 값 반환
2. v.end(): 벡터 (끝부분+1) 주소값 반환
3. v.rbegin(): reverse begin, 벡터의 끝 지점을 시작점으로 반환
4. v.rend(): reverse end, 벡터의 (시작+1) 지점을 끝 부분으로 반환
```
vector<int> v = { 1, 2, 3, 4 };
for_each(v.begin(), v.end(), [&](int& n){
    cout << n << endl;        //output : 1 2 3 4
});
 
for_each(v.rbegin(), v.rend(), [&](int& n) {
     cout << n << endl;        //output : 4 3 2 1
});

vector<int>::iterator itor = v.begin();
for (; itor != v.end(); itor++)
    cout << *itor << endl;        //output : 1 2 3 4
vector<int>::reverse_iterator itor2 = v.rbegin();
for (; itor2 != v.rend(); itor2++)
    cout << *itor2 << endl;    
```

### Vector의 요소 접근
1. v.at(i): 벡터의 i번째 요소 접근
2. v[i]: 벡터의 번째 요소 접근
3. v.front(): 벡터의 첫번째 요소 접근
4. v.back(): 벡터의 마지막 요소 접근

### Vector에 요소 삽입
1. v.push_back(): 벡터의 마지막 부분에 새로운 요소 추가
2. v.pop_back(): 벡터의 마지막 부분 제거
3. v.insert(삽입할 위치의 주소값, 변수값): 사용자가 원하는 위치에 요소 삽입
4. v.emplace(삽입할 위치의 주소값, 변수값): tkdydwkrk dnjsgksms dnlcldp dyth tkqdlq
5. v.emplace_back(): 벡터의 마지막 부분에 새로운 요소 추가
6. v.erase(삭제할 위치) or v.erase(시작위치, 끝위치): 사용자가 원하는 index 값의 요소를 지운다.
7. v.clear(): 벡터의 모든 요소를 지운다. (return size=0)
8. v.resize(수정 값): 벡터의 사이즈를 조정한다. (범위 초과시 0으로 초기화)
9. v.swap(벡터 변수): 벡터와 벡터를 스왑한다.
```
vector<int> v;
 
v.push_back(10);
v.push_back(20);        //v = { 10, 20 }
 
v.inset(v.begin() + 1, 100);     // v = { 10, 100, 20 } 
v.pop_back();        // v = { 10, 100 }
 
v.emplace_back(1);    //v = { 10, 100, 1 }
v.emplace_back(2);    //v = { 10, 100, 1, 2 }
v.emplace(v.begin() + 2, -50);    //v = { 1, 100, -50, 1, 2 }
 
v.erase(v.begin() + 1); // v = { 1, -50, 1, 2 }
v.resize(6);    // v = { 1, -50, 1, 2, 0, 0 }
v.clear();    // v = empty()  
```

### Vector Capacity(용량)
1. v.empty(): 벡터가 빈공간이면 true, 값이 있다면 false
2. v.size(): 벡터의 크기 반환
3. v.capacity(): heap에 할당된 벡터의 실제크기(최대크기) 반환
4. v.max_size(): 벡터가 system에서 만들어 질 수 있는 최대 크기 반환
5. v.reserve(숫자): 벡터 크기 설정
6. v.shrink_to_fit(): capacity의 크기를 벡터의 실제 크기에 맞춤
```
vector<int>v = { 1, 2, 3, 4 };
 
cout << v.size() << endl;    //output : 4
cout << v.capacity() << endl; //output : 10 (컴파일 환경에 따라 달라질 수 있음)
 
v.reserve(6);
cout << v.capacity() << endl; //output : 6
cout << v.max_size() << endl; //output : 1073741823(시스템 성능에 따라 달라질 수 있음)
 
v.shrink_to_fit();
cout << v.capacity() << endl; //output : 4
 
cout << v.empty() << endl; //output : false
v.clear();
cout << v.empty() << endl; //output : true
```
