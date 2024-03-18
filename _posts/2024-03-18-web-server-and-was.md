---
title: Web Server와 WAS
author: imbsh
date: 2024-03-18 09:20:00 +0900
categories: [IT, SERVER]
tags: [apache, jboss, nginx, tomcat, was, web, web application server, web server, server]
pin: true
---

> 백엔드 인프라를 공부하다보면 한 어플리케이션의 트래픽이 Web Server와 WAS로 분산되는 것을 알 수 있습니다. Web Server, WAS가 무엇인지 그리고 어떤 이유로 구분돼있는지 알아보겠습니다.

## Web Server란?
> - **개념**
> <br/>웹 브라우저(Client)로부터 HTTP 기반 요청을 받아 정적인 컨텐츠(html, js, css, jpg 등)를 제공하는 프로그램
> - **기능**
> <br/>HTTP 기반의 클라이언트(웹 브라우저, 웹 크롤러) 요청에 대해 서비스를 제공하는 기능(2가지 방식)
>   - **방식 1**
>     - 정적 컨텐츠 제공
>     - WAS를 거치지 않고 직접 제공
>   - **방식 2**
>     - 동적 컨텐츠 제공을 위한 요청 전달
>     - 클라이언트의 요청(Request)을 WAS에 보내고, WAS에서 처리된 결과를 클라이언트에게 응답(Response)
> - **종류**
> <br/> Apache Server, Nginx, IIS 등

## WAS란?
> - **개념**
> <br/>DB 조회 등의 동적 컨텐츠 제공을 위한 Application Server로 HTTP를 통해 Application을 실행해주는 미들웨어입니다. 웹 컨테이너 또는 서블릿 컨테이너 라고 불립니다. 
> - **기능**
>   - 프로그램 실행 환경과 DB 접속 기능 제공
>   - 여러 개의 트랜잭션 관리 기능 제공
>   - 업무 처리 비즈니스 로직 수행
> - **종류**
> <br/> Tomcat, JBoss, Jeus, Web Shpere 등

## 정적 컨텐츠와 Web Server / 동적 컨텐츠와 WAS
> ![web-server-and-was][web-server-and-was]
> <br/>(출처:<a href="https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html">https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html<a/>)

## Web Server와 WAS를 구분하는 이유
> - 기능 분리로 서버 부하 방지
> - 물리적 분리로 보안 강화
> - 여러 대의 WAS 연결로 서버 장애시 안정성 확보
> - 여러 종류의 Web Application 서비스 가동





[web-server-and-was]: posts/2024-03-18-web-server-and-was/web-server-and-was.webp "web-server-and-was"
