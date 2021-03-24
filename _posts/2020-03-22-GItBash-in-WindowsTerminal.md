---
layout: post
title: "Windows Terminal에서 Git Bash 사용하기"
subtitle : "Git Bash in Windows Terminal"
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
cover-img: /assets/img/path.jpg
tags: [Windows_Terminal, Git_Bash]]
comments: true
---

# Windows Terminal 설정 추가

~~~
{
    "guid": "{########-####-####-####-########}",
    "commandline": "%PROGRAMFILES%/git/usr/bin/bash.exe -i -l",
    "icon": "%PROGRAMFILES%/Git/mingw64/share/git/git-for-windows.ico",
    "name" : "Bash",
    "startingDirectory" : "%USERPROFILE%",
    "tabColor" : "#E84D31"  
}
~~~
GUID는 powershell에 다음과 같이 입력하면 얻을 수 있다.
~~~
[guid]::NewGuid()
~~~

Terminal 설정에 대한 더 많은 정보는 아래의 사이트에 있다.
[Windows 터미널이란?](https://docs.microsoft.com/ko-kr/windows/terminal/)
# Context Menu 수정하기
바탕화면 또는 폴더 왼쪽 클릭하면 나타나는 Context Menu 내부의 Git Bash도 Windows Terminal을 이용하여 열 수 있다. 
### Warning

{: .box-warning}
**주의:** 편집하기 전 미리 백업을 해두는 것이 좋다.


Registry 편집기에 들어간후 다음 주소로 들어간다.
~~~
컴퓨터\HKEY_CLASSES_ROOT\Directory
~~~

내부에 Background와 shell폴더가 있다. Background 폴더는 바탕화면 또는 탐색기 내부를 마우스 오른쪽 클릭할 때 뜨는 Context Menu이고 shell은 폴더 아이콘을 마우스 오른쪽 클릭할 때 뜨는 Context Menu이다.

먼저 Directory\Background\shell\git_shell로 들어간다. 안에 command 폴더가 있다. 폴더를 클리하면 REG_SZ인 (기본값)이 있다. 데이터를 다음과 같이 수정한다.

~~~
"C:\Users\{사용자 컴퓨터 이름}\Appdata\Local\Microsoft\WindowsApps\wt.exe" "-p" "Bash"" "-d" "%v."
~~~

-p와 Bash는 프로필에 대한 Parameter이다. -d와 %v.는 현재 디렉터리에 대한 Parameter이다.
Parameter에 대한 더 많은 정보를 원하면 아래의 사이트가 도움이 된다.
[Shortcut Menu Verbs](https://docs.microsoft.com/en-us/windows/win32/shell/context#shortcut-menu-verbs)

수정을 했다면 Directory\shell\git_shell로 들어간다. command로 들어간 후 (기본값)의 데이터를 위와 동일하게 바꾼다.
이제 Context Menu에서도 Windows Terminal을 이용하여 Git Bash를 이용할 수 있게 되었다.