---
title: Java - 가비지 컬렉션 (Garbage Collection)
author: imbsh
date: 2024-03-14 15:48:00 +0900
categories: [IT, JAVA]
tags: [heap, minor, major, garbage, collection, young, old, generation, 가비지, 컬렉션, gc]
pin: true
---

## 가비지 컬렉션이란?
> 가비지 컬렉션(Garbage Collection, 이하 GC)을 해석해보면 쓰레기 수집입니다. Java에서 메모리 관리 방법 중 하나이며 쓰레기 수집이란 말처럼 주기적으로 **JVM의 Heap Memory 영역을 점검해 스택에서 참조되지 않는(버려진) 객체를 메모리에서 해제하는 방법**입니다. Java 뿐만이 아닌 Python, JavaScript 등의 언어에서도 제공되고 있습니다.

## 가비지 컬렉션은 어떻게 등장했을까요?
> 가비지 컬렉션은 존 매카시라는 사람이 1959년에 LISP라는 언어의 메모리 관리를 위해 처음 만들었다고 알려져 있습니다. C와 같은 언어들에서는 할당했던 메모리를 수동으로 해제해줘야 합니다. 하지만 항상 사람이 하는 일이 100% 완벽할 수는 없어 할당 후 해제를 하지 않거나, 해제한 메모리를 다시 해제 시도하는 등의 실수로 버그가 생기기 마련이었습니다. 그러니 자동으로 처리해주는 기능이 필요하지 않았을까요?

## 가비지 컬렉션에 의해 정리되는 대상은 누구일까요?
> 가비지 컬렉션을 실행하는 녀석을 가비지 컬렉터(Garbage Collector)라고 합니다. 가비지 컬렉터에게 쓰레기는 어떤 것일까요? 바로 **누구에게도 참조되고 있지 않은 객체**입니다. 참조되지 않는 객체는 앞으로도 쓰일 일이 없고 불필요하게 메모리만 점유하고 있기 때문입니다.

## JVM의 Heap Memory
> JVM의 Heap Memory 영역은 크게 Young Generation, Old Generation 두 영역으로 나눠져있습니다. 각 영역이 어떤 역할을 하는지 알아볼까요?
> 우선 Age라는 개념을 알고 가면 좋을 것 같습니다. 여기서 Age란 GC가 실행될 때마다 해제되지 않고 살아남은 횟수를 카운트 하는 것입니다. 예를 들어 총 5번의 GC에서 살아남았다면 Age가 5라고 할 수 있습니다.
> 1. **Young Generation**
> <br/>비교적 생성되지 오래되지 않은 객체들이 할당돼있으며 1개의 **Eden 영역과 2개의 Survivor 영역**으로 다시 분류됩니다.
> - **Eden 영역**
> <br/>객체가 생성되면 Heap 내에 최초로 할당되는 영역입니다. Eden 영역이 꽉 차면 GC(Minor GC)가 실행되고 Age가 증가한 객체는 Survivor 영역으로 이동됩니다.
> - **Survivor 영역**
> <br/>Eden 영역의 GC에서 살아남은 객체가 할당되는 영역입니다.
>
> 2. **Old Generation**
> <br/>비교적 오래된 객체들이 할당돼있으며 **Promotion(Young Generation 영역에서 특정 횟수 이상의 Age를 가진 객체가 Old Generation 영역으로 옮겨지는 것)** 과정을 거쳐 할당되는 영역입니다.

## 가비지 컬렉션 종류
> GC는 Minor GC, Major GC로 나눠지며 아래와 같은 특징이 있습니다.
> - **Minor GC**
>   - 대상 영역 : Young Generation
>   - 실행 시점 : Eden 영역이 꽉 찬 경우
>   - 실행 속도 : 빠름
> - **Major GC**
>   - 대상 영역 : Old Generation
>   - 실행 시점 : Old 영역이 꽉 찬 경우
>   - 실행 속도 : 느림

## 가비지 컬렉션 과정
> GC는 공통적으로 **Mark-Sweep-Compaction** 과정을 진행합니다.
> <br/>![mark-sweep-compaction][m-s-c]
> 1. **Mark** : 대상(참조되지 않는 버려진 객체)을 식별합니다.
> 2. **Sweep** : 식별된 대상을 제거합니다.
> 3. **Compaction** : 유효한 객체들을 Heap 영역의 시작 주소 앞쪽부터 다시 채워 나갑니다.
>
> <br/>위 과정을 보면 제거 대상을 찾아 제거하고, 할당 공간을 압축한다고 정리가 되는데요. 그렇다면 GC가 자주 실행되게 하면 좋은 것일까요?
>
> 우선 정답은 “No”입니다.
>
> GC가 Mark and Sweep 과정을 진행하는 동안 일시적으로 어플리케이션을 멈춥니다. 이를 Stop the World 라고 합니다. 이것은 필수적인 과정인데요. 어플리케이션을 멈추지 않고 객체를 정리한다면 어디선가 참조중인 객체의 주소가 바뀌는 등의 이유로 오류가 발생할 수 있기 때문입니다. GC가 빈번히 실행된다면 당연히 어플리케이션의 일시 정지 빈도가 증가할 것이고, 사용 중에 버벅이는 현상이 느껴질 것입니다.
>
> 그러므로 필요한 경우 개발하는 시스템의 특성에 맞게 GC에 대한 설정을 변경해 효율적으로 사용할 필요가 있습니다. 가비지 컬렉션 튜닝이라고 하는 그 과정은 차후 별도로 포스팅 하겠습니다. 
> <br/>감사합니다.

[m-s-c]: assets/img/posts/2024-03-14-garbage-collection/mark-sweep-compaction.webp "mark-sweep-compaction"
