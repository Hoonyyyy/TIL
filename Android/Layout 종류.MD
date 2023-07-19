# Layout
```
위젯은 레이아웃 안에 존재해야 한다.
레이아웃은 위젯을 배치해서 안드로이드 화면을 목적에 맞게 배열한다.
```



## LinearLayout
- 박스모델, 한방향으로 배치
- 놓여지는 순서대로 배치 - orientation
- weight, baseline

## 상대(Relative)레이아웃
- 다른 위젯을 상대로 배치_ 상대 id를 기준으로 지정한다.
```
부모에 배치시키기
layout_alignParentLeft = "true"
layout_alignParentTop = "true"
```

## TableLayout
- 테이블로 구성해서 구현
- 표와 같은 형태를 구성할 때 유용하게 사용
- GridLayout
- TableRow ( <Buuton> ~ )
- layout_column : 0부터 시작, 배치될 시작위치
- stretchColumn : 자동확장해서 행을 맞춘다.
- shrinkColumn : 자동축소해서 행을 맞춘다.
- layout_span : 열을 합침
- 속성
```
    layout_column="1" 놓여질 위치
    layout_span="2" column span
-----------------------------------------------------------
stretchColumns = "*" 모두 같은 크기로 확장 전체에 채움
```

## GridLayout
```
    GridLayout
        . rowCOunt : 행의 갯수
        . columnCount : 열의 갯수
        . layout_row : 행의 배치위치
        . layout_column : 열의 배치위치

        . layout_rowSpan:
        . layout_columnSpan
        . layout_gravity = "fill_vertical" / "fill_horizontal"
```




#### LinearLayout
- weight 하면 1:1
```xml
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:background="#4358CD"
        android:layout_weight="1">


    </LinearLayout>
```


### LinearLayout view 동적 생성
```kotlin
package com.example.myapp25k

import android.graphics.Color
import android.graphics.Color.rgb
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.Gravity
import android.widget.Button
import android.widget.LinearLayout
import android.widget.TextView

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val linearLayout = LinearLayout (this)
        linearLayout.orientation = LinearLayout.VERTICAL
        linearLayout.gravity = Gravity.CENTER
        linearLayout.setBackgroundColor(Color.GREEN)

        val params1 = LinearLayout.LayoutParams(
            LinearLayout.LayoutParams.WRAP_CONTENT,
            LinearLayout.LayoutParams.WRAP_CONTENT
        )

        val params2 = LinearLayout.LayoutParams(
            LinearLayout.LayoutParams.MATCH_PARENT,
            LinearLayout.LayoutParams.WRAP_CONTENT
        )

        val btn = Button(this)
        btn.text = "버튼"
        btn.gravity = Gravity.CENTER
        btn.setBackgroundColor(Color.rgb(100,150,200))
        btn.layoutParams = params1
        params1.bottomMargin = 100

        val tv = TextView(this)
        tv.text = "텍스트 뷰입니다. 보이나요?"
        tv.gravity = Gravity.CENTER
        tv.layoutParams = params2

        linearLayout.addView(btn)
        linearLayout.addView(tv)


        setContentView(linearLayout)

    }
}
```


### RelativeLayout 연습
- android:layout_alignParentTop="true"
- android:layout_alignParentLeft="true"
- android:layout_above="@id/tv2"
- android:layout_below="@id/tv1"
- 등 연습
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/tv1"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:gravity="center"
        android:background="#F44336"
        android:text="기준1"
        android:layout_alignParentTop="true"
        android:layout_alignParentLeft="true"
        />

    <TextView
        android:id="@+id/tv2"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:gravity="center"
        android:background="#F44336"
        android:text="기준2"
        android:layout_alignParentRight="true"
        android:layout_centerVertical="true"
        />

    <TextView
        android:id="@+id/tv3"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:gravity="center"
        android:background="#57A2DD"
        android:text="텍스트1"
        android:layout_toRightOf="@id/tv1"
        android:layout_above="@id/tv2"
        />

    <TextView
        android:id="@+id/tv4"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:gravity="center"
        android:background="#57A2DD"
        android:text="텍스트2"
        android:layout_below="@id/tv1"
        android:layout_alignParentRight="true"
        />

    <TextView
        android:id="@+id/tv5"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:gravity="center"
        android:background="#57A2DD"
        android:text="텍스트3"
        android:layout_alignParentBottom="true"
        />

    <TextView
        android:id="@+id/tv6"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:gravity="center"
        android:background="#57A2DD"
        android:text="텍스트4"
        android:layout_toLeftOf="@id/tv2"
        android:layout_alignParentBottom="true"
        
        />
</RelativeLayout>
```

### RelativeLinear 연습2
```xml
package com.example.myapp27k

import android.graphics.Color.rgb
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.Button
import android.widget.RelativeLayout

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        //setContentView(R.layout.activity_main)

        val params = RelativeLayout.LayoutParams(
            RelativeLayout.LayoutParams.MATCH_PARENT,
            RelativeLayout.LayoutParams.MATCH_PARENT
        )

        val layout = RelativeLayout(this)
        val btn = Button(this)
        btn.text = "버튼"
        btn.setBackgroundColor(rgb(55,120,50))
        btn.layoutParams = params
        layout.addView(btn)

        setContentView(layout)


    }
}
```

### TableLayout 연습
- android:stretchColumns="*"
- 칸 비워져 있으면 꽉 채우기
```
<?xml version="1.0" encoding="utf-8"?>
<TableLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:stretchColumns="*">

    <TableRow
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:backgroundTint="#91C0E6"
            android:text="1번"
            />
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:backgroundTint="#95EA98"
            android:layout_span="2"
            android:text="2번"
            />
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:backgroundTint="#F4EA8F"
            android:text="3번"
            />



    </TableRow>

    <TableRow
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:backgroundTint="#91C0E6"
            android:layout_column="1"
            android:text="1번"
            />
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:backgroundTint="#95EA98"
            android:layout_column="1"
            android:text="2번"
            />
        <Button
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:backgroundTint="#F4EA8F"
            android:layout_column="2"
            android:text="3번"
            />
    </TableRow>

</TableLayout>
```
