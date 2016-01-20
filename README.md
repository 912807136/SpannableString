# SpannableString
TextView通常通过SpannableString来修改TextView某一部分文字的字体颜色，大小，点击事件等等。

```java
package com.gavin.demospanablestring;

import android.app.Activity;
import android.graphics.Color;
import android.graphics.Typeface;
import android.graphics.drawable.Drawable;
import android.os.Bundle;
import android.text.SpannableString;
import android.text.TextPaint;
import android.text.method.LinkMovementMethod;
import android.text.style.AbsoluteSizeSpan;
import android.text.style.BackgroundColorSpan;
import android.text.style.ClickableSpan;
import android.text.style.ForegroundColorSpan;
import android.text.style.ImageSpan;
import android.text.style.StrikethroughSpan;
import android.text.style.StyleSpan;
import android.text.style.URLSpan;
import android.util.TypedValue;
import android.view.View;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends Activity {

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);

		initView();
	}

	private void initView() {
		TextView text1 = (TextView) findViewById(R.id.text1);
		String text = "你知不知道我等到花儿都谢了.点我";
		SpannableString ss = new SpannableString(text);
		// 设置字体
		ss.setSpan(new ForegroundColorSpan(Color.GREEN), 0, 2, SpannableString.SPAN_INCLUSIVE_EXCLUSIVE);
		// 设置字体大小
		int textSize = (int) TypedValue.applyDimension(TypedValue.COMPLEX_UNIT_SP, 14,
				getResources().getDisplayMetrics());
		ss.setSpan(new AbsoluteSizeSpan(textSize), 2, 4, SpannableString.SPAN_INCLUSIVE_EXCLUSIVE);
		// 设置背景
		ss.setSpan(new BackgroundColorSpan(Color.YELLOW), 4, 6, SpannableString.SPAN_INCLUSIVE_EXCLUSIVE);
		// 粗体
		ss.setSpan(new StyleSpan(Typeface.BOLD_ITALIC), 6, 8, SpannableString.SPAN_INCLUSIVE_EXCLUSIVE);
		// 设置删除线
		ss.setSpan(new StrikethroughSpan(), 8, 10, SpannableString.SPAN_INCLUSIVE_EXCLUSIVE);
		// 文本超链接
		ss.setSpan(new URLSpan("http://baidu.com"), 10, 12, SpannableString.SPAN_INCLUSIVE_EXCLUSIVE);
		text1.setMovementMethod(new LinkMovementMethod());
		// 图片
		Drawable d = getResources().getDrawable(R.drawable.ic_launcher);
		d.setBounds(0, 0, d.getIntrinsicWidth(), d.getIntrinsicHeight());  
		ss.setSpan(new ImageSpan(d), 13, 14, SpannableString.SPAN_INCLUSIVE_EXCLUSIVE);
		//点击事件
		ss.setSpan(new ClickableSpan() {
			@Override
			public void updateDrawState(TextPaint ds) {
				super.updateDrawState(ds);
				//设置没有下划线
				ds.setUnderlineText(false);
				//设置颜色高亮
				ds.setARGB(255, 0, 71, 112);
			}
			@Override
			public void onClick(View widget) {
				Toast.makeText(MainActivity.this, "我知道了", Toast.LENGTH_LONG).show();
			}
		}, 14, 16, SpannableString.SPAN_INCLUSIVE_EXCLUSIVE);
		text1.setMovementMethod(LinkMovementMethod.getInstance());
		text1.setText(ss);

	}
}

```java
