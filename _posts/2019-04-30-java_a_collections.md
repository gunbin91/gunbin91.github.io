---
layout: post
title: "10. 컬렉션(Collections)"
tags: [ java, collections ]
date: 2019-04-30
categories: [ java ]
---

<p align="center">
    컬렉션이란 많은 데이터를 처리하기 위해 사용하는 특수 객체들로, 배열과 비슷한 성격을 가지고 있지만 많은 유용한 기능들을 가지고 있다.
</p><br/>

# ◆ 컬렉션 ( Collections )
테이터(객체)를 관리(저장, 검색, 조작 등)를 목적으로 설계된 객체들.<br/>
=> 배열의 크기 제한의 단점을 보완
<br/>
#### ▶ 컬렉션객체 생성 
컬렉션 객체는 일반 객체의 생성과 조금 다른 방식으로 <font color="hotpink">제네릭</font>이라는 조건이 더 필요하다.<br/><font color="orange">저장하고자 하는 자료형을 미리 <>안에 명시</font>해 주어야 한다.
{% highlight ruby %}
ArrayList<String> ar = new ArrayList<String>();
{% endhighlight %}

<br/>

# ◆ Collection 계열
Collection은 크게 <font color="hotpink">Set / List / Queue / Map</font> 계열로 나눠진다.
#### ▶ Set 계열 
TreeSet, LinkedHashSet ...

#### ▶ List 계열 
Vector, ArrayList, Stack, LinkedList ...
#### ▶ Queue 계열 
PriorityQueue, LinkedList ...
#### ▶ 그리고 Map 계열 
HashMap, LinkdeHashMap, TreeMap...

<br/><br/>

# ◆ 컬렉션객체의 공통 메서드
객체 저장은 collection 계열에 따라서 성공 또는 실패 할 수 있음.<br/>
(같은 객체를 저장할 때, set타입은 실패 할 수도 있다. - 중복을 허용하지 않기 때문에)
<br/>

> Collection은 기본적으로 객체만 관리하기 때문에 일반데이터는 저장할 수 없지만, 일반 데이터는 Autoboxing되기 때문에 Wrapper객체로 저장이 가능하다.

<br/>

#### ▶ 컬렉션의 공통 메서드 (Map은 일부 제외)
- int size() 
: 컬렉션객체에 저장되어있는 객체의 개수를 반환
- boolean isEmpty() 
: 현재 컬렉션이 비이었는지 여부를 반환
- boolean contains(Object o) 
: 특정 객체를 가지고 있는지 여부를 반환
- boolean add(Object o) 
: 객체 저장 후 성공여부 반환 ( 객체 저장 )
- boolean remove(Object) 
: 특정객체를 삭제 후 성공여부 반환 ( 객체 제거 )
- Iterator iterator() 
: 탐색객체 반환
- boolean containsAll(Collection)
: 매개변수 컬렉션객체가 가지고 있는 객체들을 모두 가지고 있는지 반환
- boolean addAll(Collection) 
: 매개변수 컬렉션객체가 가지고 있는 객체 모두를 저장 (하나라도 저장되면 true)
- boolean removeAll(Collection) 
: 매개변수 컬렉션객체가 가지고 있는 객체들과 중복되는 객체들을 모두 제거.
- boolean retainAll(collection) 
: 매개변수 컬렉션 객체와 중복되는 객체들만 남기고 모두 제거.
- void clear() 
: 컬렉션 초기화
- toArray() 
: Object[] 배열로 반환

> Map계열을 제외한 컬렉션 간에는 변환 캐스팅이 가능하다.
<br/>컬렉션의 toString()은 관리중인 객체들의 toString()을 모아서 출력

<br/><br/>

# ◆ Traversing Collection-컬렉션 순회<br/>( 컬렉션 객체 접근 )
컬렉션 객체를 순회하는 방법으로는 크게 4가지가 있다.

#### 1. toArray를 이용해 배열로 접근.
<font color="orange">컬렉션객체.toArray()</font>를 호출하게 되면 <font color="orange">Object[]형태의 배열이 반환</font>되기 때문에 for문을 이용하여 인덱스로 접근이 가능하다.
{% highlight ruby %}
public static void main(String[] args) {
	ArrayList<String> arlist = new ArrayList<String>(); // ArrayList객체 생성
	arlist.add("하나"); 
	arlist.add("둘");
	arlist.add("셋");
	Object[] ar = arlist.toArray(); // 배열객체로 반환
	for(int i=0; i<ar.length; i++) {
		System.out.println(ar[i]);
	}
}
{% endhighlight %}

<br/>

#### 2. Iterator 객체를 이용해 접근
컬렉션 변수.iterator()를 이용하면 객체의 순회를 도와주는 객체인 <font color="orange">Iterator객체</font>를 반환해준다. 해당 객체의 메서드로 순차적 접근이 가능하다. 

- 생성 
: Iterator it = (컬렉션변수).iterator();
- it.hasNext() 
: 다음 접근 할 수 있는 (뽑을) 객체가 있는지 여부를 boolean반환
- it.next() 
: 저장 객체를 Object형으로 반환
<br/>
( hasNext()를 해 주어야 컬렉션 접근이 가능하기 때문에, 데이터가 하나만 있더라도 next()로 객체를 뽑아내기 전 hasNext()를 먼저 호출해야 한다. )
{% highlight ruby %}
HashSet set = new HashSet();
Iterator it = set.iterator(); // Iterator객체 반환
while(it.hashNext()){ // 다음 객체로 이동
    Object o = it.next(); // 객체반환
    System.out.println(o);
}
{% endhighlight %}

<br/>

#### 3. for-each 를 이용해 접근
{% highlight ruby %}
ArrayList<String> array = new ArrayList();
    for( String s : array ){
        System.out.println(s);
    }
{% endhighlight %}

<br/>

#### 4. stream().forEach
컬렉션변수.stream().forEach(a)
자주 쓰이지 않는 듯..

<br/><br/>

# ◆ Set계열 컬렉션
다른 컬렉션과 다르게 Set은 <font color="orange">중복되는 Elements(객체)를 저장하지 않는 컬렉션</font>이다.<br/>
동일객체 ?<br/>
(혹은 동일 된다고 판단되는 객체 - String및 Wrapper객체는 데이터가 같으면 같다고 판단.)
<br/>

#### ▶ 자주 쓰이는 Set계열의 객체
- HashSet 
: 속도는 제일 빠름, 순서는 보장받지 못함 ( 순서 예측 불가 )
- LinkedHashSet 
: HashSet다음으로 빠름, 순서 보장을 받음 ( 저장된 순서 )
- TreeSet 
: 객체가 가지고 있는 value기반의 정렬된 형태로 저장할 수 있음. ( 정렬 )

<br/><br/>


#### ▶ Set계열 컬렉션의 동일객체 판단.
- HashSet과 LinkedHashSet
: 저장할 객체의 hashCode()를 호출하여 비교한 후 같은 값일 때 
다시 equals()를 호출하여 비교하여 동일객체를 판단한다.<br/>
( hashCode()는 int값을 리턴 하기 때문에 보통 매개변수들을 이용한 공식을 이용 )

- TreeSet
: compareTo()의 값이 0을 리턴 할 때 동일 객체로 판단한다. (크면 양수, 작으면 음수)
<br/>
=> 따라서, 직접 만든 커스텀 객체를 TreeSet에 저장하여 쓰려면, <br/>
implements Comparable<>을 구현하고, compareTo()메서드를 오버라이드 해야 한다. <br/>
( TreeSet은 데이터를 정렬하기 때문에 <font color="orange">implements Comparable<>가 구현되어 있지 않은 객체는 사용자체를 할 수 없다</font>.)<br/>
<br/>

> <b>HashSet, LinkedHashSet</b> -> hashCode(), equals()<br/>
<b>TreeSet</b> -> implements Comparable<해당클래스>, compareTo()

<br/><br/>

# ◆ List계열
List 계열은 index가 있는 컬렉션으로,
Set계열과 달리 중복 객체를 저장하고, <font color="orange">인덱스를 통한 접근이 가능</font>하다. <br/> 
또한 List계열 전용의 Iterator객체가 추가적으로 있고, List의 일부분 추출이 가능하다.

<br/><br/>

#### ▶ List계열 컬렉션 객체 
- Vector 
: (오브젝트)배열기반 동기화 처리가 되어있기 때문에 느림– ArrayList의 구 버전 
- ArrayList 
: (오브젝트)배열기반 - 보통의 경우 가장 성능이 좋음.
<br/>=> 인덱스 수정이 자주 일어나는 경우 느림
- LinkedList 
: 객체 간 연결을 통해 배열처럼 구현 - 특정 상황에서 성능이 가장 좋음.
<br/>=> 인덱스 수정이 자주 일어나는 경우에는 ArrayList보다 빠를 수 있음
<br/>=> 동기화 처리는 Vector만 되어있고, 동기화 처리가 되어있는 객체는 무겁다.
<br/>=> 동기화(synchronized)는 멀티 쓰레드 상황에서만 볼 수 있음.

<br/>

#### ▶ List계열의 인덱스를 이용한 메서드
- add(int idx, E e) 
: 특정 인덱스에 객체 삽입
- set(int idx, E e) 
: 특정 인덱스에 있는 객체 수정
- remove(int idx) 
: 특정 인덱스의 객체 제거 
<br/>=> 제거된 인덱스 위치는 다른 객체들로 채워지기 때문에 객체들의 인덱스가 바뀔 수 있다
- get(int idx) 
: 특정 인덱스에 있는 객체 반환 ( 리스트를 변경하지 않음 )
- addAll(int idx,E e) 
: 특정 인덱스에 객체 모두 삽입
- indexOf(E e) 
: 매개변수로 들어온 객체가 있는 인덱스 반환 ( 없으면 –1 )
- lastIndexOf(E e) 
: List는 중복 값을 허용하기 때문에 뒤에서부터 찾기도 가능.
- subList(int idx, int idx) 
: 서브 리스트 컬렉션으로 반환 ( idx <=   <idx )
<br/>

> ※ subList와 원본 List는 연결되어 있기 때문에 서브리스트를 변경할 시 원본 또한 변경된다. 또한 원본의 인덱스를 삭제할 시 서브리스트가 꼬이기 때문에 사용할 수 없다.<br/>
( 단, 서브리스트에서의 삭제는 가능하다. => 원본데이터도 삭제됨 )<br/>
=> 즉, 서브리스트는 원본데이터의 일부분을 잠시 빌려 쓰는 것.

<br/>

#### ▶ ListIterator (List용 Iterator)
Iterator객체의 메서드도 사용 가능하고, 추가된 메서드도 있다.
<br/>( 자주 사용하지는 않는다. )
- 생성 
: ListIterator<> it = 컬렉션변수.listIterator()  
- hasPrevious() 
: 이전 객체가 있는지 반환
- previous() 
: 이전 객체 반환
- nextIndex() 
: 다음 인덱스 반환
- previousIndex() 
: 이전 인덱스 반환

<br/>

#### ▶ List계열은 인덱스가 있기 때문에 for문으로 접근이 가능하다.
{% highlight ruby %}
for(int idx=0; idx<컬렉션변수.size(); idx++) 
{ 컬렉션변수.get(idx); }
{% endhighlight %}

#### ▶ List계열은 동일 객체도 저장하지만, indexOf()등의 객체를 반환하기 위해서 HashCode(), equals()로 동일 객체 판단하여 반환한다.

<br/><br/>

# ◆ Queue계열
큐는 기본적으로 선입선출(FIFO : First In First Out)이기 때문에 기본 컬렉션 기능 외에, 넣은 순서대로 차례대로 데이터를 뽑아다 쓸 수 있는 기능이 구현되어 있음. <br/>
(중복 저장은 허용, Queue계열은 자주 사용되지 않는다.)

- 생성 
: Queue<String> q1 = new ArrayDeque<>();  
- E element() / E peek()
 : 가장 오래된 객체 뽑기 
- boolean offer(E e) / boolean add(E e)
 : 큐에 객체 추가 
- E poll() / E remove()  
: 가장 오래된 객체 제거, 제거할 객체가 없을 때 null을 반환하고, remove는 오류발생!

<br/>

#### ▶ 데큐(Deque) 
양방향으로 접근할 수 있음.
- 생성 
: Deque<Integer> dq = new ArrayDeque<>();
- insert 
 : addFirst(), offerFirst(), addLast(), offerLast()
- examine 
 : getFirst(), peekFirst(), getLast(), peekLast()
- remove 
: removeFirst(), pollFirst(), removeLast(), pollLast()

<br/><br/>

# ◆ Map 계열
Map은 <font color="orange">키와 벨류 값을 같이 저장하는 형태</font>로, List, Set, Queue와는 사용하는 방법 자체가 다름<br/>
( 저장할 밸류에 킷값을 설정해 넘겨야 함( value값을 키를 통해 제어 할 수 있음.) )

<br/><br/>

#### ▶ Map 종류 
- HashMap / LinkedHashMap / TreeMap 
: 키의 값은 Set으로 관리되기 때문에, <font color="orange">킷값은 중복을 허용하지 않는다.</font> 중복 저장을 시도할 경우 덮어씌우기가 된다.<br/>
( HashMap일 경우 킷값은 HashSet으로 관리 됨 – 비슷한 형태끼리.. ) 

<br/><br/>

#### ▶ 특수 Map으로 Properties라는 객체도 있다.
Properties는 Map<String,String> 형태로 되어있는 Map계열의 객체이지만,<br/>
setProperty(String, String),getProperty(String, String)메서드를 사용하기 위해 쓰인다.<br/>
<b style="color:orange;">getProperty(키,디폴트) - 키가 없을 경우 디폴트 값이 출력되도록 하는 메서드</b>

<br/>

#### ▶ Map 계열 기본 메서드
- put(Key k, Value v) 
: 객체에 키를 물려서 저장<br/>
=> 중복 value값은 허용되지만, 중복 키는 허용되지 않는다. <br/>
( 중복 키를 저장하게 되면 밸류 값이 수정된다. 따라서 수정용으로도 사용 )
- get(Key k) 
: 키에 물려있는 객체를 반환 ( 없으면 null 반환 )
- remove(Key k) 
: 키에 물려있는 객체와 키를 제거<br/>
=> 지워지는 객체가 있으면 객체 반환, 아니면 null반환
- containsKey(Key k) 
: 해당 키가 존재하는지 boolean리턴
- containsValue 
: 해당 value값이 존재하는지 boolean리턴
- size() 
: Map에 저장되어있는 객체 개수
- isEmpty() 
: Map이 비어있는지 boolean리턴
- putAll(Map m) 
: 다른 맵에 있는 값들을 전부 옮김 ( 맵 끼리만 가능 )
- clear() 
:  전부삭제<br/>
=> Map은 제너릭을 설정할 때, 형태 <K, V>를 모두 다 설정해야 함<br/>
=> putAll()도 중복키가 있을 시에는 value값이 수정될 수 있다.

<br/>

#### ▶ Map컬렉션 반환
- Set<Character> key = Map변수.keySet();
: 해당 Map의 키를 Set컬렉션 형태로 반환
- Collection<Integer> value = Map변수.values();
: 해당 Map의 value값들을 Collection객체로 반환<br/>
( Collection은 최상위 오브젝트기 때문에 아무 Map계열을 제외한 컬렉션으로 변환 가능 )
- Set<Entry<Character, Integer>> entry = Map변수.entrySet(); 
: 키와 벨류를 한 쌍의 Entry<K,V>객체를 제네릭으로 하는 Set객체로 반환

<br/>
<br/>

#### ▶ Map 순회
: ketSet()메서드를 이용하여 키를 뽑아내어 for-each문으로 getValue() 나 getKey()를 사용할 수 있음
{% highlight ruby %}
HashMap<String, Integer> hash = new HashMap<String, Integer>();
hash.put("하나", 1);
hash.put("둘", 2);
hash.put("셋", 3);
for(String s : hash.keySet()) {
	System.out.println("키: " + s);
	System.out.println("벨류: " + hash.get(s));
}
{% endhighlight %}

> 특정한 키로 밸류들을 여러 개 저장하고 싶을 때는 제너릭에 컬렉션을 셋팅 하면 된다.<br/>
ex) <String, List<String>>







<br/>