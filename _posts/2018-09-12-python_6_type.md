---
layout: post
title: "5. 자료구조(자료형)"
tags: [ python, python data type ]
date: 2018-09-12
categories: [ python ]
---

<p align="center">
    파이썬은 변수를 선언할 때 자료형과 같이 선언하지 않지만, 파이썬에도 여러가지 자료형들이 있다.
    <br> Navi : [ <a href="#list">리스트</a> ], [ <a href="#tuple">튜플</a> ], [ <a href="#dic">사전</a> ], [ <a href="#slice">슬라이스연산</a> ], [ <a href="#str">문자열</a> ], [ <a href="#col">집합</a> ]
</p><br/>

<a id="list"></a>
# 리스트( List )
리스트는 열거형 자료구조이며,  <font color="orange">대괄호( [ ] )를 이용</font>해 만들고 추가 및 삭제가 가능하다.<br/>

- <font color="deeppink">리스트선언</font>
{% highlight ruby %}
mylist = [ 'apple', 'mango', 'carrot', 'banana' ]
{% endhighlight %}
<br/>

- <font color="orange">len(리스트)</font> <br/>
열거형 데이터의 길이를 int형으로 반환<br/>
{% highlight ruby %}
print(len(mylist))

실행결과
=> 4
{% endhighlight %}
<br/>

- <font color="orange">리스트.append(데이터)</font> <br/>
리스트의 마지막인덱스에 해당 데이터추가<br/>
{% highlight ruby %}
mylist.append('rice')
print(mylist)

실행결과
=> [ 'apple', 'mango', 'carrot', 'banana', 'rice' ]
{% endhighlight %}
<br/>

- <font color="orange">리스트.insert(인덱스, 데이터)</font> <br/>
해당 인덱스에 데이터 삽입<br/>
{% highlight ruby %}
mylist.insert(1,'tomato')
print(mylist)

실행결과
=> [ 'apple', 'tomato', 'mango', 'carrot', 'banana', 'rice' ]
{% endhighlight %}


- <font color="orange">리스트.remove(인덱스)</font> <br/>
해당 인덱스 삭제
{% highlight ruby %}
mylist.remove(0)
print(mylist)

실행결과
=> [ 'tomato', 'mango', 'carrot', 'banana', 'rice' ]
{% endhighlight %}

- <font color="orange">리스트.index(데이터)</font> <br/>
해당 데이터가 있는 인덱스 반환
{% highlight ruby%}
print(mylist.index('banana'))

실행결과
=> 3
{% endhighlight %}

- <font color="orange">리스트.sort()</font> <br/>
리스트를 파이썬이 알아서 순서에 맞게 정렬해준다.
{% highlight ruby %}
mylist.sort()
print(mylist)

실행결과
=> ['banana', 'carrot', 'mango', 'rice', 'tomato']
{% endhighlight %}

- <font color="orange">리스트.pop() </font><br/>
가장 끝에 있는 데이터를 삭제 후 반환 ( 인덱스 입력도 가능 )
{% highlight ruby %}
p = mylist.pop()
print(mylist)
print(p)

실행결과
=> 
['tomato', 'aaa', 'mango', 'carrot', 'banana']
rice
{% endhighlight %}

>리스트 또한 더하거나 곱하여(문자열과 같은 방식) 새로운 리스트를 만들어 낼 수 있다.

<a id="tuple"></a>
# 튜플( Tuple )
튜플 또한 열거형 데이터로, 선언은 <font color="orange">소괄호( () )를 사용</font>한다. 또는 <font color="orange">괄호 없이 선언도 가능</font> <br/>
리스트와의 차이점은 <font color="deeppink">튜플은 수정이 불가</font>하다는 점이다. ( 추가는 가능 )<br/>

- <font color="deeppink">튜플 선언</font> 
{% highlight ruby %}
zoo = ('python', 'elephant', 'penguin')
또는
zoo = 'python', 'elephant', 'penguin'
{% endhighlight %}
<br/>

- <font color="orange">len(튜플)</font><br/> 
튜플 또한 열거형 데이터이므로 len함수 호출이 가능하다.
{% highlight ruby %}
print(len(zoo))

실행결과
=> 3
{% endhighlight %}
<br/>

- 튜플도 마찬가지로 zoo[0] 등을 통해 접근 가능
<br/><br/>
- <b>빈 튜플과 한 개짜리 튜플</b><br/>
빈 튜플은 zoo=() 와 같이 생성할 수 있으며,<br/>
한 개 짜리 튜플을 선언할 때는 zoo( "monkey", ) 와 같이 끝에 콤마(,)를 찍어야 한다.<br/>
> 한개의 데이터를 가지고 있는 튜플을 선언할 때 마지막 콤마를 찍어야 하는 이유는 형변환 문법과 동일하기 때문에 이를 구분하기 위하여 <font color="deeppink">한개짜리 튜플은 마지막 콤마를 하나 더 찍어 주어야 한다.</font>

<br/><br/>

<a id="dic"></a>
# 사전( dictionary )
자바의 Map객체와 비슷하게 <font color="deeppink">'키'와 '값'을 동시에 가질 수 있는 자료구조</font>로 dict 클래스의 인스턴스/객체이다. 사전의 <font color="orange">선언은 중괄호( {} )를 사용</font>하며, <font color="orange">키와 값의 구분은 콜론(:)을 사용</font>한다.<br/>

- <font color="deeppink">사전 선언 </font><br/>
{% highlight ruby %}
dic = {'one' : 3, 'two' : 5, 'three' : 8 }
{% endhighlight %}
<br/>

- <font color="deeppink">데이터 추출</font><br/> 
리스트와 마찬가지로 대괄호([])를 이용하여 추출하지만, 사전은 <font color="orange">인덱스 대신 키값을 넣어 해당 데이터를 추출</font>해 낼 수 있다.
{% highlight ruby %}
dic["one"] 

실행결과
=> 3
{% endhighlight %}
<br/>

- <font color="deeppink">데이터 삽입 </font><br/>
{% highlight ruby %}
dic["four"] = 15
print(dic)

실행결과
=> {'one': 3, 'two': 5, 'three': 8, 'four': 15}
{% endhighlight %}
<br/>

- <font color="deeppink">데이터 삭제</font><br/>
식별자의 삭제와 동일하다
{% highlight ruby %}
del dic['four']
print(dic)

실행결과
=> { 'one' : 3, 'two': 5, 'three': 8 }
{% endhighlight %}
<br/>

- <font color="deeppink">사전 순회</font><br/>
사전을 for문에서 순회할 때 사전의 키값을 반환해준다. <br/>
따라서 해당 키값을 통해 사전의 데이터를 뽑아낼 수 있다.<br/>
{% highlight ruby %}
for k in dic :
    print("key = ", k, ", value =", dic[k])
    
실행결과
=> 
key =  one , value = 3
key =  two , value = 5
key =  three , value = 8
{% endhighlight %}
<br/>

- 또 다른 방법으로 <font color="orange">.items()</font>라는 dict_items데이터를 뽑아내 주는 함수를 사용하여 <font color="orange">키와 값을 동시에 뽑아내며 순회</font>할 수도 있다.
{% highlight ruby %}
print("items = ", dic.items())
for k, v in dic.items() :
    print("key = ", k, ",value = ", v)
    
실행결과
=>
items =  dict_items([('one', 3), ('two', 5), ('three', 8)])
key =  one ,value =  3
key =  two ,value =  5
key =  three ,value =  8
{% endhighlight %}
<br/><br/>

### ▶ 사전 관련 함수
- <font color="orange">.keys()</font> <br/>
dict_keys라는 객체를 반환하는 함수로 <font color="orange">사전의 키를 모두 반환</font>, 파이썬 2버전에서는 리스트를 반환하지만, 3버전 이후부터는 dict_keys객체로 반환되며, 이는 for문등에서 쓰일 수 있다.
( dict_keys객체를 list로 받고 싶을 경우 <font color="orange">'list( 변수.keys() )'로 반환</font>하면 된다. )
<br/><br/>

- <font color="orange">.values()</font><br/>
dict_values라는 객체를 반환하는 함수, 사전의 value값을 모두 반환, 동작 구조는 keys()와 같다.
<br/><br/>

- <font color="orange">.items()</font><br/>
dict_items라는 객체를 반환하는 함수, 사전의 key와 value를 모두 반환
리스트 안에 튜플 형식, 동작 구조는 keys()와 같다.
<br/><br/>

- <font color="orange">.clear()</font><br/>
사전 초기화
<br/><br/>

- <font color="orange">.get(key)</font><br/>
사전에서 키에 대응하는 value값을 가져오는 함수로, [key]를 이용하여 뽑아낼 수 있지만 없는 데이터의 경우 에러가 발생한다.<br/>
하지만 <font color="orange">.get(key)함수를 사용해서 불러올 시 해당 키가 없으면 None를 반환</font>하여 에러를 막을 수 있다.<br/>

<br/>

<a id="col"></a>
# 집합
정렬되지 않은 단순 객체의 묶음. 교집합과 합 집합을 얻어낼 수 있다.<br/>

- 집합 선언 : 
{% highlight ruby %}
bri = set(['brazil', 'russia', 'india'])
{% endhighlight %}

- 교집합
: bri & bri2

<a id="str"></a>
# 문자열
파이썬의 모든 문자열은 str클래스의 객체이다.<br/>

- 문자열 선언
: {% highlight ruby %}
name = "hong gil dong'
{% endhighlight %}
<br/><br/>

- <font color="orange">문자열.startswith("문자열")</font><br/>
문자열변수의 문자열이 해당 문자열로 시작되는지 여부를 True/False로 반환
{% highlight ruby %}
print(name.startswith('ho'))

실행결과
=> True
{% endhighlight %}
<br/><br/>

- <font color="orange">'문자열' in 문자열변수 </font><br/>
해당 문자열이 문자열변수 문자열 안에 포함되는지 여부를 True/False로 반환
{% highlight ruby %}
print("gil" in name)

실행결과
=> True
{% endhighlight %}
<br/><br/>

- <font color="orange">'문자열'.find("문자열")</font><br/>
해당 문자열에서 매개 문자열이 시작되는 인덱스 위치를 반환, 만약 찾지 못한 경우 -1을 반환<br/>
{% highlight ruby %}
name.find('war')

실행결과
=> -1
{% endhighlight %}
<br/><br/>

- <font color="orange">문자열변수.join(문자열리스트)</font><br/>
해당 문자열 변수를 구분자로 문자열리스트를 결합하여 큰 문자열을 만들어 냄
{% highlight ruby %}
mylist = [ 'apple', 'mango', 'carrot', 'banana' ]
name ="--good--"
print(name.join(mylist))

실행결과
=> apple--good--mango--good--carrot--good--banana
{% endhighlight %}
<br/><br/>

<a id="slice"></a>
# 슬라이스 연산 (서브스크립션 연산)
열거형( 리스트, 튜플, 문자열)에서만 사용 가능한 인덱싱 연산으로 일부분을 잘라내 부분 집합을 반환해주는 연산이다.<br/>

#### ▶ 음수 인덱스
파이썬에서는 인덱스에 음수 또한 허용되는데, 인덱스가 음수인 경우 <font color="deeppink">뒤에서부터 몇 번째 인지</font>를 판단하여
만약 <font color="orange">-1일 경우 (길이-1)의 인덱스와 동일</font>한 역할을 한다.<br/>
ex ) list[-1] = list[len(list)-1]<br/>
=> 즉 list[-1]은 제일 마지막 인덱스
<br/><br/>

#### ▶ 슬라이스 연산 사용법
열거형의 부분 집합을 추출하여 반환해준다. <font color="orange">'열거형데이터[ index1 : index2 ]'</font>의 문법으로 사용하며,<br/> <font color="deeppink">데이터[index1] ~ 데이터[index2-1]까지의 데이터를 반환</font>해준다.<br/>
이는 복사본이 아니기 때문에 수정시 원본또한 수정되지만, 변수에 대입하여 사용하면 복사본이 된다.<br/>
 
- list[1:3] 
: list[1] ~ list[2]

- list[[2: ] 
: list[2] ~ 

- list[1:-1] 
: list[1] ~ list[len(list)-2]

- list[ : ] 
: list[0] ~ 
<br/><br/>

#### ▶ 슬라이스 연산 세번째 인수
인덱스를 몇 칸씩 건너 띄며 반환할 것인지를 결정<br/>

- list[ : : 1] 
: 디폴트가 1이므로, 한칸씩 반환하여 결국 모두 반환

- list[ : : 2] 
: 한 칸을 건너뛰고 두 칸마다 한 칸씩 반환

- list[ : : -1] 
: 마지막 인덱스부터 거꾸로 반환
<br/><br/>


#### ▶ 참조값
파이썬에도 자바에서의 참조의 개념이 있기 때문에 객체변수를 단순히 ‘=’기호를 이용하여 대입하는 것은 같은 참조값을 가질 수 있기 때문에, 복사본이 필요할 경우 슬라이스 연산 등을 이용하도록 한다.
<br/> 일반변수의 경우는 =를 이용하여 참조되지 않는다.

# in / not in 연산자
열거형 데이터에서 데이터 포함여부를 확인할 수 있는 키워드로, 흐름제어문인 if, for문 등에서 자주 쓰인다.<br/>

ex ) "apple" in list<br/>
=> "apple" 라는 문자열이 list에 포함되어 있는지 True/False 반환
<br/><br/>




<br/>