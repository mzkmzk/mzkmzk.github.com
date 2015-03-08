---
layout: post
title: "android adapter"
date: 2014-12-16 11:37:40 +0800
comments: true
categories: android
---

android adapter主要分为SimpleAdapter、ArrayList、BaseAdapter

这里主要介绍BaseAdapter
###0x01 .xml 布局文件的 单一行的样式设置 
	
	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal" 
    android:id="@+id/book_access"
    >
     <TextView
             android:id="@+id/book_name"
             android:layout_width="wrap_content"
             android:layout_height="wrap_content"
             android:layout_weight="1"
             android:background="#ffffffff"
             android:gravity="center"
             android:text="@string/str_navi_home_navi_left" />
          <TextView
              android:id="@+id/book_accessTime"
              android:layout_width="wrap_content"
              android:layout_height="wrap_content"
              android:layout_weight="1"
              android:background="#ffffffff"
              android:gravity="center"
              android:text="@string/str_navi_home_navi_right" />
	</LinearLayout> 
	
###0x02 .java 继承BaseAdapter

	package gabriel.luoyer.promonkey.main;

	import java.util.ArrayList;
	import java.util.List;
	import java.util.Map;

	import org.apache.http.NameValuePair;
	import org.apache.http.message.BasicNameValuePair;

	import com.charon.pulltorefreshlistview.PullToRefreshListView;
	import com.charon.pulltorefreshlistview.PullToRefreshListView.OnRefreshListener;

	import android.os.AsyncTask;
	import android.os.Bundle;
	import android.os.Handler;
	import android.os.Message;
	import android.os.SystemClock;
	import android.util.Log;
	import android.view.LayoutInflater;
	import android.view.View;
	import android.view.ViewGroup;
	import android.widget.AdapterView;
	import android.widget.BaseAdapter;
	import android.widget.TextView;
	import android.widget.Toast;
	import android.widget.AdapterView.OnItemClickListener;
	import gabriel.luoyer.promonkey.R;
	import gabriel.luoyer.promonkey.base.BaseFragment;
	import gabriel.luoyer.promonkey.bean.book;
	import gabriel.luoyer.promonkey.utils.ModelServer;

	public class HomeFragment extends BaseFragment {
	
	private PullToRefreshListView mPullToRefreshListView;
	private MyAdapter adapter;
	private ArrayList<book> data;
	public LayoutInflater mInflater;
	
	@Override
	public View onCreateView(LayoutInflater inflater, ViewGroup container,
			Bundle savedInstanceState) {
		mInflater=inflater;
		View view = inflater.inflate(R.layout.main_frg_home, container, false);
		findView(view);
		initView(view);
		return view;
	}
	
	private void findView(View view) {
		mPullToRefreshListView = (PullToRefreshListView)view.findViewById(R.id.mfh_s);
	}

	private void initView(View view) {
		
		data = new ArrayList<book>();
		
		book b =new book();
		
		b.setB_name("书籍名称");
		b.setB_accessTime("借书时间");
		
		data.add(b);

		adapter = new MyAdapter();

		mPullToRefreshListView.setAdapter(adapter);

		mPullToRefreshListView.setOnRefreshListener(new OnRefreshListener() {

			@Override
			public void onRefresh() {
				new AsyncTask<Void, Void, Void>() {

					@Override
					protected Void doInBackground(Void... params) {
						SystemClock.sleep(1000);
						book b =new book();
						b.setB_name("书籍名称");
						b.setB_accessTime("借书时间");
						data.add(b);
						return null;
					}

					@Override
					protected void onPostExecute(Void result) {
						super.onPostExecute(result);
						adapter.notifyDataSetChanged();
						mPullToRefreshListView.onRefreshComplete();
					}
				}.execute();
			}
		});

		mPullToRefreshListView
				.setOnItemClickListener(new OnItemClickListener() {

					@Override
					public void onItemClick(AdapterView<?> parent, View view,
							int position, long id) {
						// If you call addHeaderView, the position will contains
						// the count of header view.
						// int realPosition = position
						// - mPullToRefreshListView.getHeaderViewsCount();
						// Toast.makeText(PullToRefreshActivity.this,
						// data.get(realPosition), Toast.LENGTH_SHORT).show();

						Toast.makeText(
								getActivity().getApplicationContext(),
								(String) mPullToRefreshListView.getAdapter()
										.getItem(position), Toast.LENGTH_SHORT)
								.show();

					}

				});

	}


	private class MyAdapter extends BaseAdapter {

		@Override
		public int getCount() {
			return data.size();
		}

		@Override
		public Object getItem(int position) {
			return data.get(position);
		}

		@Override
		public long getItemId(int position) {
			return position;
		}

		@Override
		public View getView(int position, View convertView, ViewGroup parent) {
			 ViewHolder holder = null;
             if (convertView == null) {                    
                 holder=new ViewHolder();                   
                 convertView = mInflater.inflate(R.layout.main_frg_home_lv, null);
                 holder.book_name = (TextView)convertView.findViewById(R.id.book_name);
                 holder.book_accessTime = (TextView)convertView.findViewById(R.id.book_accessTime);
                 convertView.setTag(holder);                    
             }else {                   
                 holder = (ViewHolder)convertView.getTag();
             }                           
             holder.book_name.setText(data.get(position).getB_name());
             holder.book_accessTime.setText(data.get(position).getB_accessTime());                
             return convertView;
		}
	}
	
	public final class ViewHolder{
        public TextView book_name;
        public TextView book_accessTime;
    }
	}


参考链接<http://www.xue5.com/Mobile/Mobile/735287.html>






