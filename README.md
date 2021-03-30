# MFC
#include<Windows.h>
#include <iostream>
//窗口处理过程：

LRESULT CALLBACK WindosProc(HWND hwnd, UINT uMsg, WPARAM wParam, LPARAM lParam)
{
	return DefWindowProc(hwnd, uMsg, wParam, lParam);
}

int WINAPI WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, PSTR szCmdLine, int iCmdShow)
{
	WNDCLASS win1;

	//设计窗口
	win1.cbClsExtra = 0;//类额外内存
	win1.cbWndExtra = 0;//窗口额外内存
	win1.hbrBackground =(HBRUSH) GetStockObject( WHITE_BRUSH);//背景
	win1.hCursor = LoadCursor(NULL, IDC_HAND);//光标
	win1.hIcon = LoadIcon(NULL, IDI_ERROR);//图标
	win1.lpfnWndProc = WindosProc;
	win1.hInstance = hInstance;
	win1.lpszClassName = TEXT("i loce you");
	win1.lpszMenuName = NULL;
	win1.style = 0;

	//注册窗口
	RegisterClass(&win1);

	//创建窗口
	/*
		lpClassName
		lpWindowName
	    dwStyle
		 x
		 y
		nWidth,
		nHeight
		hWndParent
		hMenu
		hInstance
		lpParam*/
	HWND hwnd =  CreateWindow(
	win1.lpszClassName,TEXT("hellowordl"),WS_ACTIVECAPTION,CW_USEDEFAULT,CW_USEDEFAULT,CW_USEDEFAULT,CW_USEDEFAULT,NULL,NULL,hInstance,NULL);
	
	//4.显示
	ShowWindow(hwnd, SW_SHOWNORMAL);
	UpdateWindow(hwnd);

	//5.循环读取消息、
	MSG msg;
	while (true)
	{
		if (GetMessage(&msg, hwnd, 0, 0)==false)
		{
			break;
		}

		TranslateMessage(&msg);//翻译消息

		DispatchMessage(&msg);//分发消息
	}
	return 0;
}
