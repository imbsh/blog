---
title: Java - 수동 Transaction Rollback
author: imbsh
date: 2025-01-09 21:16:00 +0900
categories: [IT, JAVA]
tags: [자바, java, transaction, rollback, 트랜잭션, 롤백, 수동, setrollbackonly]
pin: true
---

> 개발을 하다보면 이런저런 이유로 트랜잭션을 수동으로 조작해줘야 하는 경우가 있습니다.
> 예를 들어 쿼리 실행에 문제가 없었지만 특정 값을 받으면 예외 발생없이 정상적으로 진행하면서도 롤백은 해야하는 경우들입니다.
> 이럴 땐 어떻게 할까요?

## TransactionAspectSupport 클래스?
> TransactionAspectSupport는 Spring 프레임워크에서 트랜잭션 관리를 지원하는 클래스입니다. 
> <br/>주로 AOP(Aspect-Oriented Programming)를 사용하여 **트랜잭션 경계를 설정**하고, 트랜잭션의 **시작, 커밋, 롤백**을 처리합니다. 
> 또한 트랜잭션 어드바이스(advice)와 트랜잭션 매니저(transaction manager)를 결합하여 트랜잭션의 일관성과 원자성을 보장합니다.

## setRollbackOnly() 호출하기
```java
@Transactional
public void myMethod() {
  insertMethod();
  updateMethod();
  deleteMethod();
  
  boolean result = verifyMethod();

  if(!result) {
    TransactionAspectSupport.currentTransactionStatus().setRollbackOnly();
  }
}

/*
* currentTransactionStatus()로 현재 트랜잭션을 TransactionStatus 클래스로 가져온 후
* 해당 클래스의 setRollbackOnly()를 호출합니다.
* 이는 현재 트랜잭션이 종료될 때 무조건 Rollback하도록 설정합니다.
*/

```
> 위와 같이 사용할 수 있습니다.
> <br/>감사합니다.