#[안드로이드] Snackbar(스낵바) 사용하기
<br>

## 설명

안드로이드 5.0 롤리팝과 함께 공개된 머터리얼 디자인(Material Design) 가이드에는 Toast와 비슷하지만 뭔가 다른 느낌의 무언가가 있었는데 바로 Snackbar이다.

<center>
[Hi! I'm Snackbar!]
~~그래 안녕?!~~
</center>

<br>
API 버전 20 이하 (킷캣 이하)의 안드로이드 버전에서는 Support Library v4가 필요하며 API도 간단해서 금방 사용할 수 있다. 이번 시간에는 Snackbar의 구현과, Toast와의 차이점을 설명해보겠다.

자세한 API 설명은 안드로이드 레퍼런스에서 확인할 수 있다.
http://developer.android.com/reference/android/support/design/widget/Snackbar.html
<br>

## Toast와의 차이점

아래는 Snackbar와 Toast의 API이다.
<br>

```
Snackbar API
Snackbar.make (View view, CharSquence text, int duration)
Snackbar.make (View view, int resId, int duration)

Snackbar 생성시 View와 문자열(리소스 포함), 지속 시간 (int형)을 매개변수로 받는다.
```

```
Toast API
Toast.makeText (Context context, CharSequence text, int duration)
Toast.makeText (Context context, int resId, int duration)

Toast 생성시 Context (보통 this), 문자열(리소스 포함), 지속 시간(int형)을 매개변수로 받는다.
```
<br>

두가지 모두 사용자에게 알린다는 목적은 같다. 하지만 약간의 기능과 구현 방법에서 차이가 있다.

- Snackbar를 API 21 (롤리팝) 이하에서 구현하기 위해서는 SupportLibrary v4가 필요하다.
- Snackbar은 Action을 통해 OnClick을 설정할 수 있다.
- Toast는 Context를 인자로 받고, Snackbar는 View를 매개변수로 받는다.


~~그래도 show() 써줘야하는건 똑같다. 사랑이 돌아오듯 show()도 돌아온다~~
<br>

## Snackbar 구현하기
<br>

<center><video src="http://material-design.storage.googleapis.com/publish/material_v_3/material_ext_publish/0B6Okdz75tqQsLVVnZlF4UEtKRU0/components_snackbar_specs_fabtablet_002.webm" width="640" height="480"></video></center>

<br>
구현하기에 앞서 잠시 위의 영상을 보자. 구글이 머터리얼 디자인을 공개하면서 같이 공개한 영상이다. 4초밖에 되지 않는 짧은 영상이지만 Snackbar를 표현하기는 충분하다.


<br>

### 기본 구현

영상을 잘 보았다면 아래의 코드를 보도록 하자. 위에서 필자는 Snackbar의 API는 간단하다고 했다. 못봤다면 위에서 다시 보고오자.
<br>

<div class="colorscripter-code" style="color:#010101; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important; overflow:auto"><table class="colorscripter-code-table" style="margin:0; padding:0; border:none; background-color:#fafafa; border-radius:4px; line-height:140%" cellspacing="0" cellpadding="0"><tr><td style="padding:6px; border-right:2px solid #e5e5e5"><div style="margin:0; padding:0; word-break:normal; text-align:right; color:#666; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important"><div>1</div></div></td><td style="padding:6px 0"><div align="left" style="margin:0; padding:0; color:#010101; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important"><div style="padding:0 6px; white-space:pre">Snackbar.make(view,&nbsp;<span style="color:#63a35c">"Hi!&nbsp;I'm&nbsp;Snackbar!"</span>,&nbsp;Snackbar.LENGTH_LONG).setAction(<span style="color:#63a35c">"Action"</span>,&nbsp;<span style="color:#066de2">null</span>).show();</div></div></td><td style="vertical-align:bottom; padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none"><span style="font-size:9px; word-break:normal; background-color:#e5e5e5; color:white; border-radius:10px; padding:1px">cs</span></a></td></tr></table></div>


위의 'Hi! I'm Snackbar!' 이미지를 만들때 썼던 코드다. 간단하다.
<br>

<div class="colorscripter-code" style="color:#010101; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important; overflow:auto"><table class="colorscripter-code-table" style="margin:0; padding:0; border:none; background-color:#fafafa; border-radius:4px; line-height:140%" cellspacing="0" cellpadding="0"><tr><td style="padding:6px; border-right:2px solid #e5e5e5"><div style="margin:0; padding:0; word-break:normal; text-align:right; color:#666; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important"><div>1</div></div></td><td style="padding:6px 0"><div style="margin:0; padding:0; color:#010101; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important"><div style="padding:0 6px; white-space:pre">Snackbar.make(view,&nbsp;<span style="color:#63a35c">"Hi!&nbsp;I'm&nbsp;Snackbar!"</span>,&nbsp;Snackbar.LENGTH_LONG).show();</div></div></td><td style="vertical-align:bottom; padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none"><span style="font-size:9px; word-break:normal; background-color:#e5e5e5; color:white; border-radius:10px; padding:1px">cs</span></a></td></tr></table></div>


가뜩이나 짧은 코드에서 Action 부분을 빼면 더 짧아진다. 역시 Toast와 비슷하다.
하지만 여기서 끝나면 재미가 없다. ~~하지만 이미 이 글은 너무 길다.~~
<br>

### Action 구현하기

Toast와의 차이점에서도 말했었다. Snackbar는 Action을 통해 OnClick을 받을 수 있다.

<div class="colorscripter-code" style="color:#010101; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important; overflow:auto"><table class="colorscripter-code-table" style="margin:0; padding:0; border:none; background-color:#fafafa; border-radius:4px; line-height:140%" cellspacing="0" cellpadding="0"><tr><td style="padding:6px; border-right:2px solid #e5e5e5"><div style="margin:0; padding:0; word-break:normal; text-align:right; color:#666; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important"><div>1</div><div>2</div><div>3</div><div>4</div><div>5</div><div>6</div><div>7</div></div></td><td style="padding:6px 0"><div style="margin:0; padding:0; color:#010101; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important"><div style="padding:0 6px; white-space:pre">Snackbar.make(v,&nbsp;<span style="color:#63a35c">"Hi!&nbsp;I'm&nbsp;Snackbar!"</span>,&nbsp;Snackbar.LENGTH_LONG)</div><div style="padding:0 6px; white-space:pre">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.setAction(<span style="color:#63a35c">"OK"</span>,&nbsp;<span style="color:#a71d5d">new</span>&nbsp;OnClickListener()&nbsp;{</div><div style="padding:0 6px; white-space:pre">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@Override</div><div style="padding:0 6px; white-space:pre">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#a71d5d">public</span>&nbsp;<span style="color:#a71d5d">void</span>&nbsp;onClick(View&nbsp;v)&nbsp;{</div><div style="padding:0 6px; white-space:pre">&nbsp;</div><div style="padding:0 6px; white-space:pre">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</div><div style="padding:0 6px; white-space:pre">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}).show();</div></div><div style="text-align:right; margin-top:-13px; margin-right:5px; font-size:9px; font-style:italic"><a href="http://colorscripter.com/info#e" target="_blank" style="color:#e5e5e5; text-decoration:none">Colored by Color Scripter</a></div></td><td style="vertical-align:bottom; padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none"><span style="font-size:9px; word-break:normal; background-color:#e5e5e5; color:white; border-radius:10px; padding:1px">cs</span></a></td></tr></table></div>


가장 위에 있던 기본 코드와의 차이는 단 하나. setAction이다.
~~달라진 것은 단 하나. 전부입니다.~~
<br>

```
Snackbar setAction API
setAction(CharSequence text, OnClickListener listener)
setAction(int resId, OnClickListener listener)

Action의 버튼이 될 문자열(리소스 포함), OnClickListener를 매개변수로 받는다.
```

OnClickListener의 OnClick에 (5번 라인)에 클릭했을 때의 내용을 작성하면 된다.
