---
title: Java - VM의 Linux에 JDK 설치하기
author: imbsh
date: 2024-03-18 16:35:00 +0900
categories: [IT, JAVA]
tags: [centos, java, jdk, linux, 리눅스, 설정, 설치, 자바, 환경 변수]
pin: true
---

> 오늘은 리눅스 환경에서 jdk 설치 후 환경 변수 설정까지 해보겠습니다.
> - **환경**
>   - **Host OS** : Windows 10
>   - **VM Version / OS** : VirtualBox 6.1 / CentOS 7

## 진행 순서
> 1. 오라클의 자바 페이지([https://www.oracle.com/java/](https://www.oracle.com/java/))로 접속합니다.
> <br/>상단 [Resources] – [Downloads] – [Java Downloads] 순서로 클릭해 페이지를 이동합니다.
> ![01][01]
>
> 2. 페이지 이동 후 하단으로 스크롤 후 Java 8 버전의 jdk를 다운로드합니다.
> <br/>32bit 환경은 x86 RPM Package, 64bit 환경은 x64 RPM Package 파일을 다운로드해줍니다.
> ![02][02]
>
> 3. 파일 다운로드 시 [파일 저장]을 선택하고 원하는 경로에 저장합니다.
>
> 4. root 계정으로 다운로드 받은 rpm 파일을 설치합니다.
> <br/>터미널에서 rpm 파일위치로 이동 후 아래 명령어로 설치를 실행합니다.
> ```shell
> // x86의 경우
> rpm -ivh jdk-8u401-linux-i586.rpm
> // x64의 경우
> rpm -ivh jdk-8u401-linux-x64.rpm
> ```
> 
> 5. 일반 계정으로 사용자 전환 후 .bash_profile을 수정합니다.
> ```shell
> cd ~
> vi .bash_prpofile
> ```
> 6. JAVA_HOME, PATH를 설정해줍니다.
> ```shell
> JAVA_HOME=(경로)/jdk1.8.0.401-amd64
> PATH=$JAVA_HOME/bin:$PATH
> ```
> 7. Java 버전 확인까지되면 jdk 설치 및 환경 변수 설정 완료!
> ```shell
> java -version
> ```





[01]: posts/2024-03-18-install-jdk-on-linux/01.webp "01"
[02]: posts/2024-03-18-install-jdk-on-linux/02.webp "02"
