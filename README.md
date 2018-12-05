# gaminganywhere32
This project cloned from https://github.com/chunying/gaminganywhere/ for Window 10 and MSVC 2017(SDK 10.0.17763.0)

First Set path

	set PATH="C:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\bin";%PATH%
	set INCLUDE="C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\Include"

Open command prompt as Administrator

	C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Auxiliary\Build\vcvars32.bat


Need to replace symbolic link with file content like ctlr-sdl, event-driven with event-posix 

Set path 

	MS C++ 2010 and mspdb100.dll
	
	https://stackoverflow.com/questions/2990331/ms-c-2010-and-mspdb100-dll
	
	https://github.com/chunying/gaminganywhere/issues/56
	
	encoder-video.cpp(186): error C2668: 'std::to_string' : ambiguous call to overloaded function	
		https://github.com/chunying/gaminganywhere/issues/51	

Replace these file 
	1) C:\Users\name\Documents\Visual Studio 2010\Projects\gaminganywhere\ga\module\vsource-desktop\vsource-desktop-dfm.cpp vsource-desktop-d3d.cpp
	
	2) C:\Users\name\Documents\Visual Studio 2010\Projects\gaminganywhere\ga\server/NMakefile.def
	
	content with
	
		1)	vsource-desktop.cpp
		
		2)	ga/module/NMakefile.def
	
FFMPEG 4.1
		gaminganywhere\ga\core\ga-avcodec.cpp(113): error C2065: 'CODEC_FLAG_GLOBAL_HEADER' : undeclared identifier
		
		gaminganywhere\ga\module\encoder-audio\encoder-audio.cpp(110): error C2065: 'CODEC_FLAG_GLOBAL_HEADER' : undeclared identifier
		
		gaminganywhere\ga\client\rtspclient.cpp(376): error C2065: 'CODEC_CAP_TRUNCATED' : undeclared identifier
		
		hook-function.cpp(179): error C2065: 'PIX_FMT_BGRA': undeclared identifier
		
		gaminganywhere\ga\client\rtspclient.cpp CODEC_CAP_TRUNCATED CODEC_FLAG_TRUNCATED
		
			just append  AV_ to the CODEC_..._...
			
Code commented
	server-ffmpeg.obj : error LNK2019: unresolved external symbol _ffio_open_dyn_packet_buf referenced in function "int __cdecl ff_server_send_packet_1(char const *,void *,int,struct AVPacket *,__int64,struct timeval *)" (?ff_server_send_packet_1@@YAHPBDPAXHPAUAVPacket@@_JPAUtimeval@@@Z)
	
	rtspserver.obj : error LNK2019: unresolved external symbol _ff_rtsp_parse_line referenced in function "void * __cdecl rtspserver(void *)" (?rtspserver@@YAPAXPAX@Z)
	
	server-ffmpeg.dll : fatal error LNK1120: 1 unresolved externals

Compiler error for liv555
		1600 to 1900 mismatch : This error due to Version 2010 -->2017
		
		cann't open file libliveMedia.d.lib
		
			for above error u need to compile the code in debug mode and rename file 'xxx.d.lib' and goto the 'module/NMakefile.def' and remane 'libliveMedia.lib' as 'liveMedia.lib'
			
		error LNK2019: unresolved external symbol __imp____iob_func referenced in function _ShowError
		
		syntax error : expected ':' or '=' separator: This is due to symbolic link
			copy content from module\NMakefile.def to ga\server\periodic\NMakefile.def	
