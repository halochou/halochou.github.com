---
layout: post
title: 转载-MFC多线程的界面更新
date: 2014-01-14 09:47:00
tags: [mfc]
---
帮朋友转载

转自[铮铮卡穆的空间](http://hi.baidu.com/edzhu/item/38be47081ac776056c9048be)

界面更新一般只能用在主线程中，在子线程中更新界面通常都会崩溃，这时可以考虑线程间通信，在子线程中发出一个消息，由主线程来接收，主线程收到消息之后，进行界面更新操作。

以下部分为转载：

一.在你的相关头文件中加入自定义消息常量比如一个串口读完成的消息: 

    #define   WM_COMM_READCOMPLETE                   WM_USER+1001 


二.再在你的主线程要负责处理该消息的那个窗口中(比如`CFormView1`)加入这个消息的映射: 

    BEGIN_MESSAGE_MAP(CFormView1,   CFormView) 
        ON_MESSAGE(WM_COMM_READCOMPLETE,OnReadComplete) 
    END_MESSAGE_MAP() 


三.之后在窗口类`CFormView1`中定义`OnReadComplete`这个消息处理函数： 

    class   CPortFormView   :   public   CFormView 
    { 
        public: 
        afx_msg   LONG   OnReadComplete(UINT   ,LONG   buf); 
        ...... 
    } 

然后你在`CFormView1`的实现文件中实现`OnReadComplete`这个函数,完成该消息的处理。


四.这样你在在其它辅助线程里要向`CFormView1`窗口发消息`WM_COMM_READCOMPLETE`并让 
主线程去执行消息处理函数`OnReadComplete`时，你只需要用下面两个函数之一就行：

    ::PostMessage(hWndFormView1,WM_COMM_READCOMPLETE,wParam,lParam); 
    ::SendMessage(hWndFormView1,WM_COMM_READCOMPLETE,wParam,lParam); 

其中`hWndFormView1`为窗口句柄；`wParam`,`lParam`你可以用来传参数 


五.注意使用多线程的方法要正确，避免死锁 
