---
layout: post
title: "android dialog Fragment显示"
date: 2015-01-02 11:37:40 +0800
comments: true
categories: android
---

先上效果图.

##0x01 创建显示框视图 alert_dialog_nick.xml

	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/layout_r"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:background="#FFFFFF"
    android:orientation="vertical" >

    <RelativeLayout
        android:layout_width="250dp"
        android:layout_height="wrap_content"
        android:layout_marginTop="15.0dip"
        android:gravity="center_horizontal" >

        <EditText  
            android:id="@+id/dialog_edit"  
            android:layout_width="230dp"  
            android:layout_height="40dp"  
        	android:background="@drawable/login_input" 
            android:drawablePadding="25dip"
            android:textColorHint="@color/color_hint"  
            android:textSize="14.0dip"
            android:inputType="number"  
            android:paddingLeft="10dp" />  
    </RelativeLayout>

    <ImageView
        android:layout_width="250dp"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_marginTop="15dp"
        android:background="@color/color_gray"
        android:src="@drawable/prefresh_list_cutline" />

    <RelativeLayout
        android:layout_width="250dp"
        android:layout_height="wrap_content"
        android:layout_marginLeft="5dp"
        android:layout_marginRight="5dp"
        android:layout_marginTop="15dp" >

        <LinearLayout
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_centerInParent="true"
            android:paddingBottom="10.0dip"
            android:orientation="horizontal" >

            <Button
                android:id="@+id/yes"
                android:layout_width="90.0dip"
                android:layout_height="40.0dip"
                android:background="@color/color_blue"
                android:text="@string/dialog_yes"
                android:textSize="16sp"
                android:layout_marginRight="20.0dip"
                android:textColor="@color/color_white" />

            <Button
                android:id="@+id/no"
                android:layout_width="90.0dip"
                android:layout_height="40.0dip"
                android:background="@color/color_red"
                android:text="@string/dialog_no"
                android:textSize="16sp"
                android:textColor="@color/color_white" />
        </LinearLayout>
    </RelativeLayout>

	</LinearLayout>


##0x02 创建显示框TianKongDialog.java

	//TianKongDialog 这个注意点在 DialogFragment 要是import android.support.v4.app.DialogFragment的...不要直接app.DialogFragment的
	
	@SuppressLint("NewApi")
	public class TianKongDialog extends DialogFragment{
	private static String CURRENT_TIME = "CURRENT_TIME";
	
	private EditText dialog_edit;
	
	public static TianKongDialog newInstance(){
		//创建一个新的带有参数的Fragment实例
		TianKongDialog fragment = new TianKongDialog();
		Bundle args = new Bundle();
		fragment.setArguments(args);
		return fragment;
	}
	
	@Override
	public Dialog onCreateDialog(Bundle savedInstanceState) {
		LayoutInflater factory = (LayoutInflater)  getActivity().getSystemService( getActivity().LAYOUT_INFLATER_SERVICE);
		final View customViewnick = factory.inflate(R.layout.alert_dialog_nick, null);
		dialog_edit = (EditText)customViewnick.findViewById(R.id.dialog_edit);
		final Dialog ad2 = new Dialog(getActivity(), R.style.Theme_CustomDialog2);
		ad2.setContentView(customViewnick);
		ad2.setCancelable(false);//有可能你调不出这个方法，可以通过ad.setOnKeyListener()方法来实现屏蔽back键
		ad2.setCanceledOnTouchOutside(false);//当点击除对话框外屏幕其他区域时对话框不消失，默认是消失的

		Button buttonnickyes = (Button)customViewnick.findViewById(R.id.yes);
		buttonnickyes.setOnClickListener(new Button.OnClickListener() {
			
			@Override
			public void onClick(View arg0) {
				String cushion_time = dialog_edit.getText().toString();
				ad2.dismiss();
			}
		});
		Button buttonnickno = (Button)customViewnick.findViewById(R.id.no);
		buttonnickno.setOnClickListener(new Button.OnClickListener() {
			
			@Override
			public void onClick(View arg0) {
				ad2.dismiss();
			}
		});
		return ad2;			
	}

	

	}
	
##0x03 调用 显示框

		String tag = "my_dialog";  
        TianKongDialog myFragment = TianKongDialog.newInstance();  
        myFragment.show(getFragmentManager(), tag); 

