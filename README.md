# crash
crash 堆栈定位






##crash 日志定位crash 位置
```
首先是获取线上版本的dSYM文件, 并在dSYM文件找到app文件 ,拷贝dSYM文件和app文件到同一目录, 然后执行命令:

先cd到改目录执行
运行脚本   xcrun atos --arch arm64 -o OutdoorAssistantApplication  -l 0x0000000101844a6c 0x00000001028814D8

注意  0x0000000101844a6c 是起始地址  , 0x00000001028814D8 是结束地址 与下面的+ 17025644相关(0x0000000101844a6c + 17025644 得到的)
```

如:
```
stack:(
"0   OutdoorAssistantApplication         0x0000000101844a6c OutdoorAssistantApplication + 17025644",    0x00000001028814D8

"1   OutdoorAssistantApplication         0x00000001018437f0 OutdoorAssistantApplication + 17020912", 0x000000010287EFE0

"2   OutdoorAssistantApplication         0x0000000101843418 OutdoorAssistantApplication + 17019928", 0x000000010287E830

"3   OutdoorAssistantApplication         0x0000000100c339c4 OutdoorAssistantApplication + 4372932",  0x000000010105F388
"4   libdispatch.dylib                   0x00000002038b4a38 <redacted> + 24",
"5   libdispatch.dylib                   0x00000002038b57d4 <redacted> + 16",
"6   libdispatch.dylib                   0x0000000203859c80 <redacted> + 684",
"7   libdispatch.dylib                   0x0000000203866030 <redacted> + 372",
"8   libdispatch.dylib                   0x00000002038668d4 <redacted> + 128",
"9   libsystem_pthread.dylib             0x0000000203a961b4 _pthread_wqthread + 464"
)
```

运行后的结果
```
+[TrackBackUpManager backUpTrackData:withProgressBlock:completionBlock:] (in OutdoorAssistantApplication) (TrackBackUpManager.m:0)
-[TrackBackUpManager startBackUpTrack:] (in OutdoorAssistantApplication) (TrackBackUpManager.m:408)
-[TrackBackUpManager addTrackBackUpTaskForTracks:] (in OutdoorAssistantApplication) (TrackBackUpManager.m:0)
__35-[AutoBackupHelper trackAutoUpload]_block_invoke (in OutdoorAssistantApplication) (AutoBackupHelper.m:246)
```
