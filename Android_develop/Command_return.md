#[안드로이드] 리눅스 커맨드를 실행하고 결과값을 받아오기
##(SELinux 상태 확인하기)
<br>

[Viper4Android Installer](http://http://overimagine.tistory.com/14) 앱을 만들면서 SELinux의 상태를 확인하는 부분을 넣으면서 리눅스 커맨드를 실행, 결과값을 받아와야했다. ProcessBuilder만으로는 실행은 가능하나 결과를 반환할 수 없었기 때문에 BufferReader를 이용하였다.
<br>

```
ProcessBuilder를 이용해 커맨드를 실행하고 BufferReader를 이용해 결과값을 받아올 수 있다.
```

<br>
## 예시
뜬금없지만 아래는 완성된 코드예시이다.
<center>
<div class="colorscripter-code" style="color:#010101; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important; overflow:auto"><table class="colorscripter-code-table" style="margin:0; padding:0; border:none; background-color:#fafafa; border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px; border-right:2px solid #e5e5e5"><div style="margin:0; padding:0; word-break:normal; text-align:right; color:#666; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height:130%"><div style="line-height:130%">1</div><div style="line-height:130%">2</div><div style="line-height:130%">3</div><div style="line-height:130%">4</div><div style="line-height:130%">5</div><div style="line-height:130%">6</div><div style="line-height:130%">7</div><div style="line-height:130%">8</div><div style="line-height:130%">9</div><div style="line-height:130%">10</div><div style="line-height:130%">11</div></div></td><td style="padding:6px 0"><div align="left" style="margin:0; padding:0; color:#010101; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#a71d5d">public</span>&nbsp;<span style="color:#a71d5d">static</span>&nbsp;<span style="color:#066de2">String</span>&nbsp;SelinuxStatus()&nbsp;{</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#066de2">String</span>&nbsp;line&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;<span style="color:#066de2">null</span>;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#a71d5d">try</span>&nbsp;{</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Process&nbsp;p&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;Runtime.getRuntime().exec(<span style="color:#63a35c">"getenforce"</span>);</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;BufferedReader&nbsp;br&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;<span style="color:#a71d5d">new</span>&nbsp;BufferedReader(<span style="color:#a71d5d">new</span>&nbsp;InputStreamReader(p.getInputStream()));</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;line&nbsp;<span style="color:#0086b3"></span><span style="color:#a71d5d">=</span>&nbsp;br.readLine();</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#a71d5d">return</span>&nbsp;line;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span style="color:#a71d5d">catch</span>&nbsp;(Exception&nbsp;e)&nbsp;{</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#a71d5d">return</span>&nbsp;<span style="color:#066de2">null</span>;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;}</div><div style="padding:0 6px; white-space:pre; line-height:130%">}</div></div><div style="text-align:right; margin-top:-13px; margin-right:5px; font-size:9px; font-style:italic"><a href="http://colorscripter.com/info#e" target="_blank" style="color:#e5e5e5; text-decoration:none">Colored by Color Scripter</a></div></td><td style="vertical-align:bottom; padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none; color:white"><span style="font-size:9px; word-break:normal; background-color:#e5e5e5; color:white; border-radius:10px; padding:1px">cs</span></a></td></tr></table></div>
</center>
<br>

**요약하자면,**

SelinuxStatus()를 실행하면 (Process) p가 `"getenforce"` 명령어를 실행하고, (BufferedReader) br이 (String) line에 p를 실행하고나서의 결과값을 입력한다.

내가 썼지만 무슨 말을 하는지 모르겠다. 그냥 한줄한줄 읽어보자.
<br>

## 설명

> line 2 > String line;

문자열 line을 초기화한다. `getenforce` 명령어를 실행하면 결과값이 문자열로 나오기 때문에 문자열로 초기화하였다.
<br>

> line 4 > Process p = Runtime.getRuntime.exec("getenforce");

"getenforce"라는 명령어를 가져와서 실행한다는 뜻이다. 설정 앱의 휴대전화 정보 (또는 태블릿 정보)에서도 SELinux 상태를 확인할 수 있다.

참고로 "setenforce" 명령어는 SELinux 상태를 변경할 수 있다.
ex) setenforce 0 또는 setenforce 1
<br>

> line 5 > BufferedReader br = new BufferedReader(new InputStreamReader(p.getInputStream()));

BufferReader가 프로세스 p의 실행 결과를 받아오도록 초기화, 실행한다.
<br>

> line 6 > line = br.readLine();

br이 읽은 결과 값을 line에 저장한다.
<br>

> line 7 > return line;

문자열 line을 반환한다.
<br>

> line 9 > return null;

try문을 실행도중 에러가 발생시 catch문에서 null을 반환한다.
<br>


## 주요 부분

> line 4 > Process p = Runtime.getRuntime.exec("getenforce");

> line 5 > BufferedReader br = new BufferedReader(new InputStreamReader(p.getInputStream()));

> line 6 > line = br.readLine();
