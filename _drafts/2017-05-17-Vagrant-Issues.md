Vagrant Issues in 1.9.4

Today, I went to start-up one of my vagrant machines and then the following happened :(.

Possible Solution: http://stackoverflow.com/questions/37312334/error-on-vagrant-up-on-linux; Re-installing Virtualbox fixed the issue.

Details on the issue.
```
$ vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'fedora/23-cloud-base'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'fedora/23-cloud-base' is up to date...
==> default: Setting the name of the VM: vagrant-fedora_default_1495025303821_56967
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Booting VM...
There was an error while executing `VBoxManage`, a CLI used by Vagrant
for controlling VirtualBox. The command and stderr is shown below.

Command: ["startvm", "7f787305-fbbf-491a-ae4b-c1b730b59bcb", "--type", "headless"]

Stderr: VBoxManage: error: The virtual machine 'vagrant-fedora_default_1495025303821_56967' has terminated unexpectedly during startup with exit code 1 (0x1)
VBoxManage: error: Details: code NS_ERROR_FAILURE (0x80004005), component MachineWrap, interface IMachine
```

```
$ vagrant --version
Vagrant 1.9.4
```
Then opening Virtualbox results in crashing behavior.

```
Process:               VirtualBox [42771]
Path:                  /Applications/VirtualBox.app/Contents/MacOS/VirtualBox
Identifier:            org.virtualbox.app.VirtualBox
Version:               5.1.22 (5.1.22)
Code Type:             X86-64 (Native)
Parent Process:        ??? [1]
Responsible:           VirtualBox [42771]
User ID:               omitted

Date/Time:             2017-05-17 07:50:43.334 -0500
OS Version:            Mac OS X 10.12.3 (16D32)
Report Version:        12
Anonymous UUID:        BCD03E3C-475C-61B8-254B-486034508491

Sleep/Wake UUID:       7B9D592A-CA20-46D2-841A-7AB486D9C477

Time Awake Since Boot: 610000 seconds
Time Since Wake:       550 seconds

System Integrity Protection: enabled

Crashed Thread:        0  Dispatch queue: com.apple.main-thread

Exception Type:        EXC_BAD_INSTRUCTION (SIGILL)
Exception Codes:       0x0000000000000001, 0x0000000000000000
Exception Note:        EXC_CORPSE_NOTIFY

Termination Signal:    Illegal instruction: 4
Termination Reason:    Namespace SIGNAL, Code 0x4
Terminating Process:   exc handler [0]

Application Specific Information:
BUG IN CLIENT OF LIBDISPATCH: Assertion failed: Block was expected to execute on queue [com.apple.main-thread]
crashed on child side of fork pre-exec

Thread 0 Crashed:: Dispatch queue: com.apple.main-thread
0   libdispatch.dylib             	0x00007fffea6d0ac7 _dispatch_assert_queue_fail + 99
1   libdispatch.dylib             	0x00007fffea6c8c35 dispatch_assert_queue + 155
2   com.apple.AppKit              	0x00007fffd2fd23cd -[NSPersistentUIRestorer restoreStateFromRecords:usingDelegate:completionHandler:] + 192
3   com.apple.AppKit              	0x00007fffd37206e5 -[NSPersistentUIManager restoreAllPersistentStateWithCompletionHandler:] + 272
4   com.apple.AppKit              	0x00007fffd2cdd5fc -[NSApplication _reopenWindowsAsNecessaryIncludingRestorableState:completionHandler:] + 368
5   com.apple.AppKit              	0x00007fffd2cdd376 -[NSApplication(NSAppleEventHandling) _handleAEOpenEvent:] + 539
6   com.apple.AppKit              	0x00007fffd2cdcfd5 -[NSApplication(NSAppleEventHandling) _handleCoreEvent:withReplyEvent:] + 661
7   com.apple.Foundation          	0x00007fffd6beaebd -[NSAppleEventManager dispatchRawAppleEvent:withRawReply:handlerRefCon:] + 290
8   com.apple.Foundation          	0x00007fffd6bead37 _NSAppleEventManagerGenericHandler + 102
9   com.apple.AE                  	0x00007fffd5fed0da aeDispatchAppleEvent(AEDesc const*, AEDesc*, unsigned int, unsigned char*) + 544
10  com.apple.AE                  	0x00007fffd5fece51 dispatchEventAndSendReply(AEDesc const*, AEDesc*) + 39
11  com.apple.AE                  	0x00007fffd5fecd5d aeProcessAppleEvent + 312
12  com.apple.HIToolbox           	0x00007fffd474374f AEProcessAppleEvent + 55
13  com.apple.AppKit              	0x00007fffd2cd887d _DPSNextEvent + 1833
14  com.apple.AppKit              	0x00007fffd3452d6b -[NSApplication(NSEvent) _nextEventMatchingEventMask:untilDate:inMode:dequeue:] + 2789
15  com.apple.AppKit              	0x00007fffd2cccf35 -[NSApplication run] + 926
16  libqcocoa.dylib               	0x000000011064c0dc QCocoaEventDispatcherPrivate::currentModalSession() + 412
17  libqcocoa.dylib               	0x000000011064bc8d QCocoaEventDispatcher::processEvents(QFlags<QEventLoop::ProcessEventsFlag>) + 1933
18  org.qt-project.QtCoreVBox     	0x000000010d310b11 QEventLoop::exec(QFlags<QEventLoop::ProcessEventsFlag>) + 401
19  org.qt-project.QtWidgetsVBox  	0x000000010dee69fe QDialog::exec() + 510
20  org.qt-project.QtWidgetsVBox  	0x000000010df10c0a 0x10dcd2000 + 2354186
21  VirtualBox.dylib              	0x000000010c81d1a4 TrustedError + 1524
22  org.virtualbox.app.VirtualBox 	0x000000010c7a7fa4 0x10c7a5000 + 12196
23  org.virtualbox.app.VirtualBox 	0x000000010c7a80dd 0x10c7a5000 + 12509
24  org.virtualbox.app.VirtualBox 	0x000000010c7a8b71 0x10c7a5000 + 15217
25  libdyld.dylib                 	0x00007fffea6f4255 start + 1

Thread 1:
0   libsystem_kernel.dylib        	0x00007fffea8234e2 __workq_kernreturn + 10
1   libsystem_pthread.dylib       	0x00007fffea90b791 _pthread_wqthread + 1426
2   libsystem_pthread.dylib       	0x00007fffea90b1ed start_wqthread + 13

Thread 2:
0   libsystem_kernel.dylib        	0x00007fffea8234e2 __workq_kernreturn + 10
1   libsystem_pthread.dylib       	0x00007fffea90b791 _pthread_wqthread + 1426
2   libsystem_pthread.dylib       	0x00007fffea90b1ed start_wqthread + 13

Thread 3:
0   libsystem_kernel.dylib        	0x00007fffea8234e2 __workq_kernreturn + 10
1   libsystem_pthread.dylib       	0x00007fffea90b791 _pthread_wqthread + 1426
2   libsystem_pthread.dylib       	0x00007fffea90b1ed start_wqthread + 13

Thread 4:
0   libsystem_kernel.dylib        	0x00007fffea8234e2 __workq_kernreturn + 10
1   libsystem_pthread.dylib       	0x00007fffea90b791 _pthread_wqthread + 1426
2   libsystem_pthread.dylib       	0x00007fffea90b1ed start_wqthread + 13

Thread 5:
0   libsystem_kernel.dylib        	0x00007fffea8234e2 __workq_kernreturn + 10
1   libsystem_pthread.dylib       	0x00007fffea90b5fe _pthread_wqthread + 1023
2   libsystem_pthread.dylib       	0x00007fffea90b1ed start_wqthread + 13

Thread 6:
0   libsystem_kernel.dylib        	0x00007fffea8234e2 __workq_kernreturn + 10
1   libsystem_pthread.dylib       	0x00007fffea90b791 _pthread_wqthread + 1426
2   libsystem_pthread.dylib       	0x00007fffea90b1ed start_wqthread + 13

Thread 7:
0   libsystem_kernel.dylib        	0x00007fffea8234e2 __workq_kernreturn + 10
1   libsystem_pthread.dylib       	0x00007fffea90b791 _pthread_wqthread + 1426
2   libsystem_pthread.dylib       	0x00007fffea90b1ed start_wqthread + 13

Thread 0 crashed with X86 Thread State (64-bit):
  rax: 0x0000000000000203  rbx: 0x00007ff6e37c3d80  rcx: 0x0000000000000000  rdx: 0x000000010c7d9608
  rdi: 0x0000000000000000  rsi: 0x0000000000000000  rbp: 0x00007fff534535a0  rsp: 0x00007fff53453590
   r8: 0x0000008000100080   r9: 0x0000000000000101  r10: 0x00007ff6e3700000  r11: 0x0000000000003c00
  r12: 0x00007ff6e37b8330  r13: 0x00007ff6e37b8330  r14: 0x00007fffd39c7064  r15: 0x00007fff53453a28
  rip: 0x00007fffea6d0ac7  rfl: 0x0000000000010202  cr2: 0x00007fffea903943
  
Logical CPU:     6
Error Code:      0x00000000
Trap Number:     6


Binary Images:
       0x10c7a5000 -        0x10c7c6ff7 +org.virtualbox.app.VirtualBox (5.1.22 - 5.1.22) <9F3A2D16-33A8-3AE9-A445-D280B72949ED> /Applications/VirtualBox.app/Contents/MacOS/VirtualBox
       0x10c815000 -        0x10d061fff +VirtualBox.dylib (0) <99837641-B5F3-3624-AB00-EF02DF1B2997> /Applications/VirtualBox.app/Contents/MacOS/VirtualBox.dylib
       0x10d11c000 -        0x10d125ff7 +org.qt-project.QtMacExtrasVBox (5.6 - 5.6.2) <D3727953-8B84-38B4-A494-65C9E0EC659E> /Applications/VirtualBox.app/Contents/Frameworks/QtMacExtrasVBox.framework/Versions/5/QtMacExtrasVBox
       0x10d12e000 -        0x10d650ff7 +org.qt-project.QtCoreVBox (5.6 - 5.6.2) <C18777E0-5C5F-399B-A027-52A6CD63CECB> /Applications/VirtualBox.app/Contents/Frameworks/QtCoreVBox.framework/Versions/5/QtCoreVBox
       0x10d706000 -        0x10dbdffff +org.qt-project.QtGuiVBox (5.6 - 5.6.2) <C6432238-0C3D-3CB8-B32A-8287BC76914D> /Applications/VirtualBox.app/Contents/Frameworks/QtGuiVBox.framework/Versions/5/QtGuiVBox
       0x10dcd2000 -        0x10e1dbff7 +org.qt-project.QtWidgetsVBox (5.6 - 5.6.2) <75C6E848-4F18-3833-A3F4-93E39600C054> /Applications/VirtualBox.app/Contents/Frameworks/QtWidgetsVBox.framework/Versions/5/QtWidgetsVBox
       0x10e33e000 -        0x10e372fff +org.qt-project.QtPrintSupportVBox (5.6 - 5.6.2) <91BDB6E1-6874-3546-8857-1B34DCB05B17> /Applications/VirtualBox.app/Contents/Frameworks/QtPrintSupportVBox.framework/Versions/5/QtPrintSupportVBox
       0x10e396000 -        0x10e3d5fff +org.qt-project.QtOpenGLVBox (5.6 - 5.6.2) <BC1AE40B-2B61-341E-987F-F84592AB4C25> /Applications/VirtualBox.app/Contents/Frameworks/QtOpenGLVBox.framework/Versions/5/QtOpenGLVBox
       0x10e3f8000 -        0x10e443fff +VBoxDDU.dylib (0) <414CA576-23B4-378B-B1AE-D83C50411A7B> /Applications/VirtualBox.app/Contents/MacOS/VBoxDDU.dylib
       0x10e44e000 -        0x10e862f67 +VBoxRT.dylib (0) <A3BE05E4-BE29-32C5-B81B-7E880B899023> /Applications/VirtualBox.app/Contents/MacOS/VBoxRT.dylib
       0x10e933000 -        0x10eb59fff +VBoxVMM.dylib (0) <12287687-C8FE-3DDE-A7D7-D4FA8942AA0B> /Applications/VirtualBox.app/Contents/MacOS/VBoxVMM.dylib
       0x10ebcb000 -        0x10ec71fff +VBoxXPCOM.dylib (0) <0680E497-113C-3C65-A03F-7CC0F19BD40B> /Applications/VirtualBox.app/Contents/MacOS/VBoxXPCOM.dylib
       0x10eca2000 -        0x10eca6ffb  com.apple.agl (3.3.1 - AGL-3.3.1) <4E968AA4-9FB1-3425-AC1D-4853BC1182E3> /System/Library/Frameworks/AGL.framework/Versions/A/AGL
       0x110629000 -        0x110767fff +libqcocoa.dylib (0) <4F78214C-F2E0-3863-9708-C1241B0F0840> /Applications/VirtualBox.app/Contents/plugins/platforms/libqcocoa.dylib
       0x111edf000 -        0x111f1c267  dyld (421.2) <947FC440-80F9-32F7-A773-6FC418FE1AB7> /usr/lib/dyld
       0x1139b2000 -        0x113f00ff7  com.apple.driver.AppleIntelHD5000GraphicsGLDriver (10.22.29 - 10.2.2) <7FC0294C-B7AA-3247-9728-227622A83AEF> /System/Library/Extensions/AppleIntelHD5000GraphicsGLDriver.bundle/Contents/MacOS/AppleIntelHD5000GraphicsGLDriver
       0x114111000 -        0x114188fff  com.apple.driver.AppleIntelHD5000GraphicsMTLDriver (10.22.29 - 10.2.2) <320C9191-9ACF-3128-A131-B93E4EBFE265> /System/Library/Extensions/AppleIntelHD5000GraphicsMTLDriver.bundle/Contents/MacOS/AppleIntelHD5000GraphicsMTLDriver
    0x7fffd1cb3000 -     0x7fffd1cb3fff  com.apple.Accelerate (1.11 - Accelerate 1.11) <D700DBDF-69AE-37A2-B9C7-0961CF0B6841> /System/Library/Frameworks/Accelerate.framework/Versions/A/Accelerate
    0x7fffd1cb4000 -     0x7fffd1ccbffb  libCGInterfaces.dylib (331.5) <518D3064-6E1E-3DF6-881B-57867DFE9B1E> /System/Library/Frameworks/Accelerate.framework/Versions/A/Frameworks/vImage.framework/Versions/A/Libraries/libCGInterfaces.dylib
    0x7fffd1ccc000 -     0x7fffd21e5feb  com.apple.vImage (8.1 - ???) <6408805B-67E9-3874-8D32-0BB814CE5CDA> /System/Library/Frameworks/Accelerate.framework/Versions/A/Frameworks/vImage.framework/Versions/A/vImage
    0x7fffd21e6000 -     0x7fffd2356ff3  libBLAS.dylib (1185) <C7E42BBE-2337-3AEF-9C45-A2F2CB1A5B3E> /System/Library/Frameworks/Accelerate.framework/Versions/A/Frameworks/vecLib.framework/Versions/A/libBLAS.dylib
    0x7fffd2357000 -     0x7fffd236bffb  libBNNS.dylib (14) <CFDEE88D-E002-347C-BC68-83099651585B> /System/Library/Frameworks/Accelerate.framework/Versions/A/Frameworks/vecLib.framework/Versions/A/libBNNS.dylib
    0x7fffd236c000 -     0x7fffd2762fef  libLAPACK.dylib (1185) <2E8201CB-9A41-3D65-853E-841917FCE77B> /System/Library/Frameworks/Accelerate.framework/Versions/A/Frameworks/vecLib.framework/Versions/A/libLAPACK.dylib
    0x7fffd2763000 -     0x7fffd2779fff  libLinearAlgebra.dylib (1185) <8CC29DE1-A231-3D5E-B5F1-DCC309036FE0> /System/Library/Frameworks/Accelerate.framework/Versions/A/Frameworks/vecLib.framework/Versions/A/libLinearAlgebra.dylib
    0x7fffd277a000 -     0x7fffd2780fff  libQuadrature.dylib (3) <120F6228-A3D4-3184-89D7-785ADC2AC715> /System/Library/Frameworks/Accelerate.framework/Versions/A/Frameworks/vecLib.framework/Versions/A/libQuadrature.dylib
    0x7fffd2781000 -     0x7fffd2795ff7  libSparseBLAS.dylib (1185) <C35235B7-CFA6-39A7-BD6E-79F4D9CAFD36> /System/Library/Frameworks/Accelerate.framework/Versions/A/Frameworks/vecLib.framework/Versions/A/libSparseBLAS.dylib
    0x7fffd2796000 -     0x7fffd291dfe7  libvDSP.dylib (600) <F59348AA-E1D3-3A27-8AB5-F546D38BFB76> /System/Library/Frameworks/Accelerate.framework/Versions/A/Frameworks/vecLib.framework/Versions/A/libvDSP.dylib
    0x7fffd291e000 -     0x7fffd29d0ffb  libvMisc.dylib (600) <70D4B548-47EE-3C6B-A93B-3EA6B60701E0> /System/Library/Frameworks/Accelerate.framework/Versions/A/Frameworks/vecLib.framework/Versions/A/libvMisc.dylib
    0x7fffd29d1000 -     0x7fffd29d1fff  com.apple.Accelerate.vecLib (3.11 - vecLib 3.11) <A395B521-8E54-30F2-B4FE-355D68900DAF> /System/Library/Frameworks/Accelerate.framework/Versions/A/Frameworks/vecLib.framework/Versions/A/vecLib
    0x7fffd2c91000 -     0x7fffd3a63ff3  com.apple.AppKit (6.9 - 1504.81.100) <0CCB2E18-076E-3D8A-A777-A6E57EF2570A> /System/Library/Frameworks/AppKit.framework/Versions/C/AppKit
    0x7fffd3a75000 -     0x7fffd3a75fff  com.apple.ApplicationServices (48 - 48) <237200C2-28A6-3C19-B34B-53C953F8AE42> /System/Library/Frameworks/ApplicationServices.framework/Versions/A/ApplicationServices
    0x7fffd3a76000 -     0x7fffd3ae4ff7  com.apple.ApplicationServices.ATS (377 - 422.2) <3680281F-DB99-3CA2-9C76-CABFC8DBC980> /System/Library/Frameworks/ApplicationServices.framework/Versions/A/Frameworks/ATS.framework/Versions/A/ATS
    0x7fffd3b7e000 -     0x7fffd3cadfff  libFontParser.dylib (194.6) <F3DF2CF7-B25D-30BB-9EE6-1EA9F3B8A066> /System/Library/Frameworks/ApplicationServices.framework/Versions/A/Frameworks/ATS.framework/Versions/A/Resources/libFontParser.dylib
    0x7fffd3cae000 -     0x7fffd3cf8fff  libFontRegistry.dylib (196.3) <855AF921-EAE0-3D07-B161-5EF09806B643> /System/Library/Frameworks/ApplicationServices.framework/Versions/A/Frameworks/ATS.framework/Versions/A/Resources/libFontRegistry.dylib
    0x7fffd3d55000 -     0x7fffd3d88ff7  libTrueTypeScaler.dylib (194.6) <D0D7DA50-DF52-3D24-AFD2-03B336AA1929> /System/Library/Frameworks/ApplicationServices.framework/Versions/A/Frameworks/ATS.framework/Versions/A/Resources/libTrueTypeScaler.dylib
    0x7fffd3df4000 -     0x7fffd3e9eff7  com.apple.ColorSync (4.12.0 - 502.1) <5F244DE3-A6E8-335F-AE3B-25F0E407DD62> /System/Library/Frameworks/ApplicationServices.framework/Versions/A/Frameworks/ColorSync.framework/Versions/A/ColorSync
    0x7fffd3e9f000 -     0x7fffd3eefff7  com.apple.HIServices (1.22 - 591) <34C950CC-1084-354A-BCE6-9396EDB29DF8> /System/Library/Frameworks/ApplicationServices.framework/Versions/A/Frameworks/HIServices.framework/Versions/A/HIServices
    0x7fffd3ef0000 -     0x7fffd3effff3  com.apple.LangAnalysis (1.7.0 - 1.7.0) <47D1A017-91A4-37F3-93E0-3923CD6ED2DE> /System/Library/Frameworks/ApplicationServices.framework/Versions/A/Frameworks/LangAnalysis.framework/Versions/A/LangAnalysis
    0x7fffd3f00000 -     0x7fffd3f4dfff  com.apple.print.framework.PrintCore (12 - 491) <B7CC15C1-AF50-37F3-8AF6-65F8CDC323F0> /System/Library/Frameworks/ApplicationServices.framework/Versions/A/Frameworks/PrintCore.framework/Versions/A/PrintCore
    0x7fffd3f4e000 -     0x7fffd3f89fff  com.apple.QD (3.12 - 310) <8F718290-DD82-36CE-9AF0-EFB6D31A49F4> /System/Library/Frameworks/ApplicationServices.framework/Versions/A/Frameworks/QD.framework/Versions/A/QD
    0x7fffd3f8a000 -     0x7fffd3f95ff7  com.apple.speech.synthesis.framework (6.3.3 - 6.3.3) <629831B1-B13C-30F5-AE16-6BB9037E3753> /System/Library/Frameworks/ApplicationServices.framework/Versions/A/Frameworks/SpeechSynthesis.framework/Versions/A/SpeechSynthesis
    0x7fffd3f96000 -     0x7fffd41a6fff  com.apple.audio.toolbox.AudioToolbox (1.14 - 1.14) <A1B98513-C19E-376F-8DAF-71BB2F263C5F> /System/Library/Frameworks/AudioToolbox.framework/Versions/A/AudioToolbox
    0x7fffd41a7000 -     0x7fffd41a7fff  com.apple.audio.units.AudioUnit (1.14 - 1.14) <55C6A958-D52B-3D81-B230-EB949212B5D9> /System/Library/Frameworks/AudioUnit.framework/Versions/A/AudioUnit
    0x7fffd4310000 -     0x7fffd46e3ff7  com.apple.CFNetwork (807.2.14 - 807.2.14) <9702C8B9-2984-3DD9-9C59-A83499C2DBC4> /System/Library/Frameworks/CFNetwork.framework/Versions/A/CFNetwork
    0x7fffd46fd000 -     0x7fffd46fdfff  com.apple.Carbon (154 - 157) <1BF9C0EB-45A0-3584-85DC-F64A9914F40D> /System/Library/Frameworks/Carbon.framework/Versions/A/Carbon
    0x7fffd46fe000 -     0x7fffd4701fff  com.apple.CommonPanels (1.2.6 - 98) <6A71E8CB-3BF7-3A49-A5F7-0579BAE1219D> /System/Library/Frameworks/Carbon.framework/Versions/A/Frameworks/CommonPanels.framework/Versions/A/CommonPanels
    0x7fffd4702000 -     0x7fffd4a0aff7  com.apple.HIToolbox (2.1.1 - 856.13) <98D5D2A7-55A6-31A7-9056-CC48EBB16654> /System/Library/Frameworks/Carbon.framework/Versions/A/Frameworks/HIToolbox.framework/Versions/A/HIToolbox
    0x7fffd4a0b000 -     0x7fffd4a0eff7  com.apple.help (1.3.5 - 49) <27C5F9FE-838F-3807-A4AC-D99470185B10> /System/Library/Frameworks/Carbon.framework/Versions/A/Frameworks/Help.framework/Versions/A/Help
    0x7fffd4a0f000 -     0x7fffd4a14fff  com.apple.ImageCapture (9.0 - 9.0) <E3E757FD-4060-33A4-A2AC-85EFBD987FCE> /System/Library/Frameworks/Carbon.framework/Versions/A/Frameworks/ImageCapture.framework/Versions/A/ImageCapture
    0x7fffd4a15000 -     0x7fffd4aacff3  com.apple.ink.framework (10.9 - 219) <B44BA36D-7549-3EB2-8CF6-E171885194FB> /System/Library/Frameworks/Carbon.framework/Versions/A/Frameworks/Ink.framework/Versions/A/Ink
    0x7fffd4aad000 -     0x7fffd4ac7fff  com.apple.openscripting (1.7 - 172) <B204BF70-C4AA-3699-8493-66E6645A92A8> /System/Library/Frameworks/Carbon.framework/Versions/A/Frameworks/OpenScripting.framework/Versions/A/OpenScripting
    0x7fffd4ac8000 -     0x7fffd4ac9ff3  com.apple.print.framework.Print (12 - 267) <CA7E9448-0903-34C8-AAF6-9070B52BF70E> /System/Library/Frameworks/Carbon.framework/Versions/A/Frameworks/Print.framework/Versions/A/Print
    0x7fffd4aca000 -     0x7fffd4accff7  com.apple.securityhi (9.0 - 55006) <ACD20DC1-FBDE-3E1B-91BF-867FE7849CBC> /System/Library/Frameworks/Carbon.framework/Versions/A/Frameworks/SecurityHI.framework/Versions/A/SecurityHI
    0x7fffd4acd000 -     0x7fffd4ad3ff7  com.apple.speech.recognition.framework (6.0.1 - 6.0.1) <A20B0F7B-C32A-3FF1-BB75-BAC0EE4EF889> /System/Library/Frameworks/Carbon.framework/Versions/A/Frameworks/SpeechRecognition.framework/Versions/A/SpeechRecognition
    0x7fffd4bb2000 -     0x7fffd4bb2fff  com.apple.Cocoa (6.11 - 22) <CF1AD0E9-2257-35FE-B719-760B58E405C9> /System/Library/Frameworks/Cocoa.framework/Versions/A/Cocoa
    0x7fffd4cf2000 -     0x7fffd4d82ff7  com.apple.audio.CoreAudio (4.3.0 - 4.3.0) <A38A11A5-130B-39CE-BEBA-F5427F6801DC> /System/Library/Frameworks/CoreAudio.framework/Versions/A/CoreAudio
    0x7fffd4d83000 -     0x7fffd4d96fff  com.apple.CoreBluetooth (1.0 - 1) <76AFC4B4-A9FD-3434-B168-90087E71F5C4> /System/Library/Frameworks/CoreBluetooth.framework/Versions/A/CoreBluetooth
    0x7fffd4d97000 -     0x7fffd5091feb  com.apple.CoreData (120 - 752.8) <FE3F152B-4C35-3A58-A0CB-D04EE5908818> /System/Library/Frameworks/CoreData.framework/Versions/A/CoreData
    0x7fffd5092000 -     0x7fffd511efff  com.apple.CoreDisplay (1.0 - 1) <48B568C0-1E12-34F4-943D-EAB447FBA1BE> /System/Library/Frameworks/CoreDisplay.framework/Versions/A/CoreDisplay
    0x7fffd511f000 -     0x7fffd55b9fff  com.apple.CoreFoundation (6.9 - 1348.28) <A40AA224-7A50-3989-95D0-5A228A0E2FAF> /System/Library/Frameworks/CoreFoundation.framework/Versions/A/CoreFoundation
    0x7fffd55ba000 -     0x7fffd5c3cfff  com.apple.CoreGraphics (2.0 - 1070.13.2) <0685658F-21AE-31D9-8C9A-B92528CDFB59> /System/Library/Frameworks/CoreGraphics.framework/Versions/A/CoreGraphics
    0x7fffd5c3d000 -     0x7fffd5e7ffff  com.apple.CoreImage (12.2.0 - 451.3.1) <CDAD60F3-74F6-3EA5-A8B5-B42476E350FD> /System/Library/Frameworks/CoreImage.framework/Versions/A/CoreImage
    0x7fffd5fe4000 -     0x7fffd5fe4fff  com.apple.CoreServices (775.9.7 - 775.9.7) <A5C444F3-408B-3062-AF4B-BF8CD919F221> /System/Library/Frameworks/CoreServices.framework/Versions/A/CoreServices
    0x7fffd5fe5000 -     0x7fffd6036fff  com.apple.AE (712.2 - 712.2) <342A13C0-4A6A-3947-B66B-0F624A4A7B52> /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/AE.framework/Versions/A/AE
    0x7fffd6037000 -     0x7fffd6312ff7  com.apple.CoreServices.CarbonCore (1159.5 - 1159.5) <11CC2194-0C9C-397A-B7F9-CDAB9B68D87D> /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/CarbonCore.framework/Versions/A/CarbonCore
    0x7fffd6313000 -     0x7fffd6346fff  com.apple.DictionaryServices (1.2 - 274) <864F3808-FFDD-3C4B-A5B7-F1A6C4668A86> /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/DictionaryServices.framework/Versions/A/DictionaryServices
    0x7fffd6347000 -     0x7fffd634fffb  com.apple.CoreServices.FSEvents (1230 - 1230) <13A2FC17-8F8C-35BF-9584-59FDFB738E2B> /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/FSEvents.framework/Versions/A/FSEvents
    0x7fffd6350000 -     0x7fffd64bcff7  com.apple.LaunchServices (775.9.7 - 775.9.7) <E350E4F6-822A-3F04-B59B-468A39AF5C64> /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/A/LaunchServices
    0x7fffd64bd000 -     0x7fffd656dfff  com.apple.Metadata (10.7.0 - 1075.28) <DBB524CD-6938-3623-99C2-4B1EC1E1BE58> /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/Metadata.framework/Versions/A/Metadata
    0x7fffd656e000 -     0x7fffd65cdfff  com.apple.CoreServices.OSServices (775.9.7 - 775.9.7) <E9625B0B-9AE7-3024-9FEF-FEE0A1876D9D> /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/OSServices.framework/Versions/A/OSServices
    0x7fffd65ce000 -     0x7fffd663efff  com.apple.SearchKit (1.4.0 - 1.4.0) <F1B3EF8D-E820-317C-AC7F-8F056C246874> /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/SearchKit.framework/Versions/A/SearchKit
    0x7fffd663f000 -     0x7fffd6685ff7  com.apple.coreservices.SharedFileList (38 - 38) <E1400999-1F08-35A1-9D07-27D80A2AF89A> /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/SharedFileList.framework/Versions/A/SharedFileList
    0x7fffd6712000 -     0x7fffd685eff7  com.apple.CoreText (352.0 - 544.5) <E90EA1D8-3491-3014-9043-9928C4E4349C> /System/Library/Frameworks/CoreText.framework/Versions/A/CoreText
    0x7fffd685f000 -     0x7fffd6894fff  com.apple.CoreVideo (1.8 - 234.0) <48C31E93-87C2-31F4-97E7-9E54C1EA8E7D> /System/Library/Frameworks/CoreVideo.framework/Versions/A/CoreVideo
    0x7fffd6895000 -     0x7fffd6906ffb  com.apple.framework.CoreWLAN (11.0 - 1200.25.1) <BEBE9C03-3B9A-3948-99E3-CC8148FA2AB5> /System/Library/Frameworks/CoreWLAN.framework/Versions/A/CoreWLAN
    0x7fffd6a05000 -     0x7fffd6a0afff  com.apple.DiskArbitration (2.7 - 2.7) <16EA6D93-A2EC-31DB-BF52-C4764E7B1630> /System/Library/Frameworks/DiskArbitration.framework/Versions/A/DiskArbitration
    0x7fffd6b99000 -     0x7fffd6f40ff3  com.apple.Foundation (6.9 - 1349.25) <D820A498-2E62-367D-BC72-5845B14C06E3> /System/Library/Frameworks/Foundation.framework/Versions/C/Foundation
    0x7fffd6f6c000 -     0x7fffd6f9dfff  com.apple.GSS (4.0 - 2.0) <95FAD1F9-1610-3428-B9B4-D32F67C26574> /System/Library/Frameworks/GSS.framework/Versions/A/GSS
    0x7fffd705d000 -     0x7fffd7100ffb  com.apple.Bluetooth (5.0.3 - 5.0.3f1) <CCB4E097-1ED0-3439-8450-2B6EFFBC4608> /System/Library/Frameworks/IOBluetooth.framework/Versions/A/IOBluetooth
    0x7fffd7101000 -     0x7fffd7196ff7  com.apple.framework.IOKit (2.0.2 - 1324.30.13) <163BE7FA-B29A-348F-8B5F-E301F2E8C964> /System/Library/Frameworks/IOKit.framework/Versions/A/IOKit
    0x7fffd7197000 -     0x7fffd719dffb  com.apple.IOSurface (153.3 - 153.3) <3DD3BF22-0800-31F2-B179-87F87D6F0548> /System/Library/Frameworks/IOSurface.framework/Versions/A/IOSurface
    0x7fffd71ef000 -     0x7fffd7348fef  com.apple.ImageIO.framework (3.3.0 - 1582) <564168E7-BEC0-35E3-9BF0-59B65C17225E> /System/Library/Frameworks/ImageIO.framework/Versions/A/ImageIO
    0x7fffd7349000 -     0x7fffd734dfff  libGIF.dylib (1582) <040243CD-3A68-3ADC-805C-FE1D17C80028> /System/Library/Frameworks/ImageIO.framework/Versions/A/Resources/libGIF.dylib
    0x7fffd734e000 -     0x7fffd743eff7  libJP2.dylib (1582) <A55870F9-F27F-3BD0-BE89-981BFF63D485> /System/Library/Frameworks/ImageIO.framework/Versions/A/Resources/libJP2.dylib
    0x7fffd743f000 -     0x7fffd7462ffb  libJPEG.dylib (1582) <58C01E72-10A0-313F-8139-ED6E9D087ABB> /System/Library/Frameworks/ImageIO.framework/Versions/A/Resources/libJPEG.dylib
    0x7fffd7463000 -     0x7fffd748aff7  libPng.dylib (1582) <F2CC3750-3520-311B-9C66-9D86036375B7> /System/Library/Frameworks/ImageIO.framework/Versions/A/Resources/libPng.dylib
    0x7fffd748b000 -     0x7fffd748dff3  libRadiance.dylib (1582) <C3E9CE5C-1A25-391B-9ACB-556AA065B985> /System/Library/Frameworks/ImageIO.framework/Versions/A/Resources/libRadiance.dylib
    0x7fffd748e000 -     0x7fffd74e7ff3  libTIFF.dylib (1582) <71ADCD24-67C9-31B5-8E48-A4B89AFBB19F> /System/Library/Frameworks/ImageIO.framework/Versions/A/Resources/libTIFF.dylib
    0x7fffd80b7000 -     0x7fffd80d0ff7  com.apple.Kerberos (3.0 - 1) <49DCBE1A-130C-3FBF-AAEA-AF9A518913AC> /System/Library/Frameworks/Kerberos.framework/Versions/A/Kerberos
    0x7fffd88ce000 -     0x7fffd8926fff  com.apple.Metal (86.18 - 86.18) <7DFE0437-25A8-3E87-8318-91573C895742> /System/Library/Frameworks/Metal.framework/Versions/A/Metal
    0x7fffd91fa000 -     0x7fffd9202fff  com.apple.NetFS (6.0 - 4.0) <6614F9B8-0861-338B-8FF0-8E402F96141C> /System/Library/Frameworks/NetFS.framework/Versions/A/NetFS
    0x7fffd93d7000 -     0x7fffd93dfff7  libcldcpuengine.dylib (2.8.5) <341EBC48-CCF4-3292-9097-F61715AC573E> /System/Library/Frameworks/OpenCL.framework/Versions/A/Libraries/libcldcpuengine.dylib
    0x7fffd95a8000 -     0x7fffd95f6ff3  com.apple.opencl (2.8.6 - 2.8.6) <553BFCCA-5ACB-3DB0-B958-4BF2DE91838F> /System/Library/Frameworks/OpenCL.framework/Versions/A/OpenCL
    0x7fffd95f7000 -     0x7fffd9610ffb  com.apple.CFOpenDirectory (10.12 - 194) <88E97774-6767-3A01-808B-C923F9310E20> /System/Library/Frameworks/OpenDirectory.framework/Versions/A/Frameworks/CFOpenDirectory.framework/Versions/A/CFOpenDirectory
    0x7fffd9611000 -     0x7fffd961cff7  com.apple.OpenDirectory (10.12 - 194) <0E4E32DD-6592-3860-9793-BAED6915AE0D> /System/Library/Frameworks/OpenDirectory.framework/Versions/A/OpenDirectory
    0x7fffd961d000 -     0x7fffd961ffff  libCVMSPluginSupport.dylib (13.0.10) <43D037C3-9254-3601-9F5B-CD637D517758> /System/Library/Frameworks/OpenGL.framework/Versions/A/Libraries/libCVMSPluginSupport.dylib
    0x7fffd9620000 -     0x7fffd9623ff7  libCoreFSCache.dylib (151.1) <1910EF80-DE30-3817-8FDF-63F3C8B4BA37> /System/Library/Frameworks/OpenGL.framework/Versions/A/Libraries/libCoreFSCache.dylib
    0x7fffd9624000 -     0x7fffd9627fff  libCoreVMClient.dylib (151.1) <8C8E9295-1918-3763-A0B7-6397EB181EF4> /System/Library/Frameworks/OpenGL.framework/Versions/A/Libraries/libCoreVMClient.dylib
    0x7fffd9628000 -     0x7fffd9630ffb  libGFXShared.dylib (13.0.10) <52E92D3C-25EA-31F9-9885-DC0D886D9143> /System/Library/Frameworks/OpenGL.framework/Versions/A/Libraries/libGFXShared.dylib
    0x7fffd9631000 -     0x7fffd963cfff  libGL.dylib (13.0.10) <B40728B5-13D2-3423-9C39-885B1098698D> /System/Library/Frameworks/OpenGL.framework/Versions/A/Libraries/libGL.dylib
    0x7fffd963d000 -     0x7fffd9679fe7  libGLImage.dylib (13.0.10) <3E856113-9217-3B13-98AD-4D0D356931B6> /System/Library/Frameworks/OpenGL.framework/Versions/A/Libraries/libGLImage.dylib
    0x7fffd967a000 -     0x7fffd97f0ffb  libGLProgrammability.dylib (13.0.10) <4C3FD24A-1C43-343E-8EBA-BE1FDCE3F74C> /System/Library/Frameworks/OpenGL.framework/Versions/A/Libraries/libGLProgrammability.dylib
    0x7fffd97f1000 -     0x7fffd9831ff3  libGLU.dylib (13.0.10) <BBCAA457-BA34-3D13-8845-803C63960E08> /System/Library/Frameworks/OpenGL.framework/Versions/A/Libraries/libGLU.dylib
    0x7fffda199000 -     0x7fffda1a7fff  com.apple.opengl (13.0.10 - 13.0.10) <B11A2E1B-4B1D-3ECD-BADA-3508BE5775BF> /System/Library/Frameworks/OpenGL.framework/Versions/A/OpenGL
    0x7fffda1a8000 -     0x7fffda34efff  GLEngine (13.0.10) <62CCEC13-1EB3-3A65-9224-3DCD2838E0C7> /System/Library/Frameworks/OpenGL.framework/Versions/A/Resources/GLEngine.bundle/GLEngine
    0x7fffda34f000 -     0x7fffda379ffb  GLRendererFloat (13.0.10) <E508ABC7-3E67-3845-989F-5B764D36FE12> /System/Library/Frameworks/OpenGL.framework/Versions/A/Resources/GLRendererFloat.bundle/GLRendererFloat
    0x7fffdaec4000 -     0x7fffdb0bfff7  com.apple.QuartzCore (1.11 - 449.41.15) <3CD775C0-683D-3B4E-8EC2-AB1DAC4C3AE9> /System/Library/Frameworks/QuartzCore.framework/Versions/A/QuartzCore
    0x7fffdb625000 -     0x7fffdb944fff  com.apple.security (7.0 - 57740.31.2) <A47D7BAE-0591-3184-8E44-FB2EB08A19C2> /System/Library/Frameworks/Security.framework/Versions/A/Security
    0x7fffdb945000 -     0x7fffdb9bbff7  com.apple.securityfoundation (6.0 - 55132.20.1) <9407620B-B230-3320-B0B7-5AE59F1D135C> /System/Library/Frameworks/SecurityFoundation.framework/Versions/A/SecurityFoundation
    0x7fffdb9e5000 -     0x7fffdb9e8ff3  com.apple.xpc.ServiceManagement (1.0 - 1) <4E24C12E-6164-3A7A-8EB8-C2523492BAE8> /System/Library/Frameworks/ServiceManagement.framework/Versions/A/ServiceManagement
    0x7fffdbd6f000 -     0x7fffdbde0ff7  com.apple.SystemConfiguration (1.14 - 1.14) <D9A57D90-E54F-3E1A-AA2F-F5A694BCE4BB> /System/Library/Frameworks/SystemConfiguration.framework/Versions/A/SystemConfiguration
    0x7fffde444000 -     0x7fffde466ffb  com.apple.framework.Apple80211 (12.0 - 1200.41) <360012DB-DAE7-3EEF-85F0-E5BE1DE3425D> /System/Library/PrivateFrameworks/Apple80211.framework/Versions/A/Apple80211
    0x7fffde467000 -     0x7fffde476fdb  com.apple.AppleFSCompression (88 - 1.0) <B6E2148F-BFBF-3F1B-A7DF-0F39190B4C20> /System/Library/PrivateFrameworks/AppleFSCompression.framework/Versions/A/AppleFSCompression
    0x7fffde565000 -     0x7fffde5f097f  com.apple.AppleJPEG (1.0 - 1) <B4C3209B-58A5-359F-A898-F61B6C40E5E9> /System/Library/PrivateFrameworks/AppleJPEG.framework/Versions/A/AppleJPEG
    0x7fffdea15000 -     0x7fffdea93fff  com.apple.backup.framework (1.8.3 - 1.8.3) <B2E28A7A-1727-3052-AA73-CBC108286C07> /System/Library/PrivateFrameworks/Backup.framework/Versions/A/Backup
    0x7fffdf719000 -     0x7fffdf740ffb  com.apple.ChunkingLibrary (172 - 172) <83E91936-305D-32A4-A256-5582B96B1852> /System/Library/PrivateFrameworks/ChunkingLibrary.framework/Versions/A/ChunkingLibrary
    0x7fffe0069000 -     0x7fffe0072ffb  com.apple.CommonAuth (4.0 - 2.0) <830B940B-3523-38DE-996D-695739616D10> /System/Library/PrivateFrameworks/CommonAuth.framework/Versions/A/CommonAuth
    0x7fffe0792000 -     0x7fffe07a2fff  com.apple.CoreEmoji (1.0 - 39.1) <0A46D6BF-22F3-39AD-B3DC-DE1EE5C442CC> /System/Library/PrivateFrameworks/CoreEmoji.framework/Versions/A/CoreEmoji
    0x7fffe0a85000 -     0x7fffe0ab5ff3  com.apple.CoreServicesInternal (276.2 - 276.2) <7D8DEF04-72F1-39F4-BBFB-09E65D7B8C10> /System/Library/PrivateFrameworks/CoreServicesInternal.framework/Versions/A/CoreServicesInternal
    0x7fffe0d45000 -     0x7fffe0dcffff  com.apple.CoreSymbolication (61050) <F4B7C798-F7B7-3977-AA08-59A03F00308E> /System/Library/PrivateFrameworks/CoreSymbolication.framework/Versions/A/CoreSymbolication
    0x7fffe0dd0000 -     0x7fffe0f0efd7  com.apple.coreui (2.1 - 430.6) <99D08D71-3E9D-300C-9EB2-A73F1B5E228C> /System/Library/PrivateFrameworks/CoreUI.framework/Versions/A/CoreUI
    0x7fffe0f0f000 -     0x7fffe0fbfff3  com.apple.CoreUtils (5.0 - 500.9) <5567181B-721C-339E-A3DC-579E36D92341> /System/Library/PrivateFrameworks/CoreUtils.framework/Versions/A/CoreUtils
    0x7fffe100f000 -     0x7fffe1074ff3  com.apple.framework.CoreWiFi (12.0 - 1200.25.1) <BEFA276C-D284-3160-8641-7DD47E38C9D7> /System/Library/PrivateFrameworks/CoreWiFi.framework/Versions/A/CoreWiFi
    0x7fffe1075000 -     0x7fffe1082ff7  com.apple.CrashReporterSupport (10.12 - 817) <CB5251B1-5BE5-308B-B30B-0050065E04CC> /System/Library/PrivateFrameworks/CrashReporterSupport.framework/Versions/A/CrashReporterSupport
    0x7fffe10f4000 -     0x7fffe10feff7  com.apple.framework.DFRFoundation (1.0 - 104.14) <258B6CFE-FD64-31C5-9973-2FD80597ECDA> /System/Library/PrivateFrameworks/DFRFoundation.framework/Versions/A/DFRFoundation
    0x7fffe1134000 -     0x7fffe11abff7  com.apple.datadetectorscore (7.0 - 539.1) <E9892E38-3D5F-36CF-BDC5-E4E3C5516B55> /System/Library/PrivateFrameworks/DataDetectorsCore.framework/Versions/A/DataDetectorsCore
    0x7fffe11e8000 -     0x7fffe1227fff  com.apple.DebugSymbols (137 - 137) <B229F3F7-250B-3151-8048-CEA7BF80FA52> /System/Library/PrivateFrameworks/DebugSymbols.framework/Versions/A/DebugSymbols
    0x7fffe1228000 -     0x7fffe1339fff  com.apple.desktopservices (1.11.3 - 1.11.3) <CCE689AA-85F3-3587-AE12-1231E8ED127E> /System/Library/PrivateFrameworks/DesktopServicesPriv.framework/Versions/A/DesktopServicesPriv
    0x7fffe161d000 -     0x7fffe1a4eff7  com.apple.vision.FaceCore (3.3.2 - 3.3.2) <DEB42099-6927-332C-8D3E-D45096318D25> /System/Library/PrivateFrameworks/FaceCore.framework/Versions/A/FaceCore
    0x7fffe2da3000 -     0x7fffe2da3fff  libmetal_timestamp.dylib (600.0.48.32) <31DF1B9E-0BBF-308B-B78D-11CCE72DAA68> /System/Library/PrivateFrameworks/GPUCompiler.framework/libmetal_timestamp.dylib
    0x7fffe2db0000 -     0x7fffe2dbbff3  libGPUSupportMercury.dylib (13.0.10) <7CC5CEF8-D132-3234-A078-6D080DFC599F> /System/Library/PrivateFrameworks/GPUSupport.framework/Versions/A/Libraries/libGPUSupportMercury.dylib
    0x7fffe306f000 -     0x7fffe308bff3  com.apple.GenerationalStorage (2.0 - 259.2) <00BF8427-967F-3693-A86F-DA0F29B49BF3> /System/Library/PrivateFrameworks/GenerationalStorage.framework/Versions/A/GenerationalStorage
    0x7fffe3789000 -     0x7fffe37fffff  com.apple.Heimdal (4.0 - 2.0) <00F00E7E-7EF4-3254-86D3-ADA4F67938CF> /System/Library/PrivateFrameworks/Heimdal.framework/Versions/A/Heimdal
    0x7fffe3e22000 -     0x7fffe3e29ffb  com.apple.IOAccelerator (289.32 - 289.32) <6395ACEE-5AD7-3536-AF12-FD6565415D94> /System/Library/PrivateFrameworks/IOAccelerator.framework/Versions/A/IOAccelerator
    0x7fffe3e2b000 -     0x7fffe3e3fff3  com.apple.IOPresentment (1.0 - 25) <40934217-996A-3DDB-A8C4-484CA0F0222B> /System/Library/PrivateFrameworks/IOPresentment.framework/Versions/A/IOPresentment
    0x7fffe3e40000 -     0x7fffe3e62fff  com.apple.IconServices (74.3 - 74.3) <3F0BD358-D019-3083-82F2-69CCAD5E5D66> /System/Library/PrivateFrameworks/IconServices.framework/Versions/A/IconServices
    0x7fffe3f45000 -     0x7fffe40fbfff  com.apple.LanguageModeling (1.0 - 123.2.4) <FEB98F96-A9BB-3E6C-85B4-B466825B8C92> /System/Library/PrivateFrameworks/LanguageModeling.framework/Versions/A/LanguageModeling
    0x7fffe49bf000 -     0x7fffe4a38ff7  com.apple.MetalPerformanceShaders.MetalPerformanceShaders (1.0 - 1) <6A759DBA-B7DF-363B-9827-AB1D1129BB34> /System/Library/PrivateFrameworks/MetalPerformanceShaders.framework/Versions/A/MetalPerformanceShaders
    0x7fffe4bb0000 -     0x7fffe4bd8fff  com.apple.MultitouchSupport.framework (368.7 - 368.7) <A29E6031-E9A6-353A-BDE5-D8DF20FD393C> /System/Library/PrivateFrameworks/MultitouchSupport.framework/Versions/A/MultitouchSupport
    0x7fffe4c87000 -     0x7fffe4c91fff  com.apple.NetAuth (6.0 - 6.0) <1E7765FC-4580-3CE4-A0F1-CAA22006AE43> /System/Library/PrivateFrameworks/NetAuth.framework/Versions/A/NetAuth
    0x7fffe550d000 -     0x7fffe554eff7  com.apple.PerformanceAnalysis (1.145 - 145) <12640C1F-433D-3CD9-B2A8-048D57B8B56D> /System/Library/PrivateFrameworks/PerformanceAnalysis.framework/Versions/A/PerformanceAnalysis
    0x7fffe5bf1000 -     0x7fffe5c0bfff  com.apple.ProtocolBuffer (1 - 249) <D8B7694B-B598-3728-8583-9C4CC0F05B64> /System/Library/PrivateFrameworks/ProtocolBuffer.framework/Versions/A/ProtocolBuffer
    0x7fffe5c25000 -     0x7fffe5c48ff3  com.apple.RemoteViewServices (2.0 - 124) <4765DC2E-CF05-38CF-9564-1FBACB7E167C> /System/Library/PrivateFrameworks/RemoteViewServices.framework/Versions/A/RemoteViewServices
    0x7fffe6946000 -     0x7fffe69c3ff7  com.apple.Sharing (696.1.22 - 696.1.22) <D0A5C682-8996-3851-B332-AD05301E6FA3> /System/Library/PrivateFrameworks/Sharing.framework/Versions/A/Sharing
    0x7fffe69e4000 -     0x7fffe6c43fe7  com.apple.SkyLight (1.600.0 - 122.8) <2B8B6734-2B70-3BD8-BB8E-3338FB2708EE> /System/Library/PrivateFrameworks/SkyLight.framework/Versions/A/SkyLight
    0x7fffe6e24000 -     0x7fffe6e30ff7  com.apple.SpeechRecognitionCore (3.3.2 - 3.3.2) <F9F0FCED-3A72-3639-91F2-B7EF248ED1B9> /System/Library/PrivateFrameworks/SpeechRecognitionCore.framework/Versions/A/SpeechRecognitionCore
    0x7fffe7519000 -     0x7fffe7585ff3  com.apple.Symbolication (61080.2) <27A57DC2-FEB7-3D23-AEB5-E3E76C5AAE79> /System/Library/PrivateFrameworks/Symbolication.framework/Versions/A/Symbolication
    0x7fffe797f000 -     0x7fffe7985ff7  com.apple.TCC (1.0 - 1) <956F7C1A-D457-3FE0-9CFE-3F1719F0865C> /System/Library/PrivateFrameworks/TCC.framework/Versions/A/TCC
    0x7fffe7a14000 -     0x7fffe7bdcff7  com.apple.TextureIO (1.41 - 1.41) <3A9D9FD9-8997-3BD1-8046-76D0BF709806> /System/Library/PrivateFrameworks/TextureIO.framework/Versions/A/TextureIO
    0x7fffe7c50000 -     0x7fffe7c51fff  com.apple.TrustEvaluationAgent (2.0 - 28) <07C1F711-A1E0-3BAC-8F4D-977516D50925> /System/Library/PrivateFrameworks/TrustEvaluationAgent.framework/Versions/A/TrustEvaluationAgent
    0x7fffe7c52000 -     0x7fffe7de2ff3  com.apple.UIFoundation (1.0 - 490.7) <047781ED-9E79-361F-8E04-71FF90C650F3> /System/Library/PrivateFrameworks/UIFoundation.framework/Versions/A/UIFoundation
    0x7fffe8e02000 -     0x7fffe8e04ffb  com.apple.loginsupport (1.0 - 1) <4449ACBA-27A8-3311-BD92-CB7E63583FC6> /System/Library/PrivateFrameworks/login.framework/Versions/A/Frameworks/loginsupport.framework/Versions/A/loginsupport
    0x7fffe8e59000 -     0x7fffe8e74ff7  libCRFSuite.dylib (34) <BACC371B-6153-36B5-BC54-3BCF26FBB221> /usr/lib/libCRFSuite.dylib
    0x7fffe8e75000 -     0x7fffe8e80fff  libChineseTokenizer.dylib (21) <09E74E18-ADB2-30D2-A858-13691CB1186C> /usr/lib/libChineseTokenizer.dylib
    0x7fffe8f12000 -     0x7fffe8f13ff3  libDiagnosticMessagesClient.dylib (102) <422911A4-E273-3E88-BFC4-DF6470E48242> /usr/lib/libDiagnosticMessagesClient.dylib
    0x7fffe8f14000 -     0x7fffe9127fff  libFosl_dynamic.dylib (16.38) <8232FA8A-F16A-3DC0-AE68-B61EFCD5F4A4> /usr/lib/libFosl_dynamic.dylib
    0x7fffe914b000 -     0x7fffe914bfff  libOpenScriptingUtil.dylib (172) <D025E180-BB3B-3FFA-98FC-B6835354D723> /usr/lib/libOpenScriptingUtil.dylib
    0x7fffe914c000 -     0x7fffe9150ff3  libScreenReader.dylib (477.20.6) <8158E263-B7DF-3B0C-BABE-4FE94A53DFE5> /usr/lib/libScreenReader.dylib
    0x7fffe9151000 -     0x7fffe9152ff3  libSystem.B.dylib (1238) <9CB018AF-54E9-300F-82BE-81FE553C9154> /usr/lib/libSystem.B.dylib
    0x7fffe91be000 -     0x7fffe91e9ffb  libarchive.2.dylib (41.41.1) <D53F0A5C-7FAA-3FCF-8A27-B7DF032C4221> /usr/lib/libarchive.2.dylib
    0x7fffe91ea000 -     0x7fffe9266fc7  libate.dylib (1.12.13) <8A963F37-CB4F-37FB-BFA5-273917C42437> /usr/lib/libate.dylib
    0x7fffe926a000 -     0x7fffe926aff3  libauto.dylib (187) <5BBF6A00-CC76-389D-84E7-CA88EDADE683> /usr/lib/libauto.dylib
    0x7fffe926b000 -     0x7fffe927bff3  libbsm.0.dylib (34) <20084796-B04D-3B35-A003-EA11459557A9> /usr/lib/libbsm.0.dylib
    0x7fffe927c000 -     0x7fffe928aff7  libbz2.1.0.dylib (38) <6FD3B63F-0F86-3A25-BD5B-E243F58792C9> /usr/lib/libbz2.1.0.dylib
    0x7fffe928b000 -     0x7fffe92e1ff7  libc++.1.dylib (307.4) <BEE86868-F831-384C-919E-2B286ACFE87C> /usr/lib/libc++.1.dylib
    0x7fffe92e2000 -     0x7fffe930cfff  libc++abi.dylib (307.2) <1CEF8ABB-7E6D-3C2F-8E0A-E7884478DD23> /usr/lib/libc++abi.dylib
    0x7fffe930d000 -     0x7fffe931dffb  libcmph.dylib (6) <2B5D405E-2D0B-3320-ABD6-622934C86ABE> /usr/lib/libcmph.dylib
    0x7fffe931e000 -     0x7fffe9333fc3  libcompression.dylib (34) <1691D6F2-46CD-3DA6-B44F-24CDD9BD0E4E> /usr/lib/libcompression.dylib
    0x7fffe9334000 -     0x7fffe9334ff7  libcoretls.dylib (121.31.1) <BCC32537-4831-3E9F-876E-8C9F4CF52FD3> /usr/lib/libcoretls.dylib
    0x7fffe9335000 -     0x7fffe9336ff3  libcoretls_cfhelpers.dylib (121.31.1) <6F37C5AD-7999-3D31-A52F-7AEED935F32D> /usr/lib/libcoretls_cfhelpers.dylib
    0x7fffe93f0000 -     0x7fffe94d5ff7  libcrypto.0.9.8.dylib (64.30.2) <D41E1901-06DD-3860-BB4F-B3ACE0284C01> /usr/lib/libcrypto.0.9.8.dylib
    0x7fffe9673000 -     0x7fffe96c6ff7  libcups.2.dylib (450) <78243BA4-43AB-3364-8111-8D54D3382621> /usr/lib/libcups.2.dylib
    0x7fffe9741000 -     0x7fffe9741fff  libenergytrace.dylib (15) <A1B040A2-7977-3097-9ADF-34FF181EB970> /usr/lib/libenergytrace.dylib
    0x7fffe9751000 -     0x7fffe9756ff7  libheimdal-asn1.dylib (498.30.1) <4ED9F6E3-83BC-3302-B004-C25399DA0333> /usr/lib/libheimdal-asn1.dylib
    0x7fffe9757000 -     0x7fffe9849ff7  libiconv.2.dylib (50) <42125B35-81D7-3FC4-9475-A26DBE10884D> /usr/lib/libiconv.2.dylib
    0x7fffe984a000 -     0x7fffe9a6fffb  libicucore.A.dylib (57149.0.1) <6B5FDA93-AA88-318F-9608-C2A33D602EC7> /usr/lib/libicucore.A.dylib
    0x7fffe9a75000 -     0x7fffe9a76fff  liblangid.dylib (126) <3F4530C9-8BE1-3AA7-9A82-98694D240866> /usr/lib/liblangid.dylib
    0x7fffe9a77000 -     0x7fffe9a90ffb  liblzma.5.dylib (10) <44BD0279-99DD-36B5-8A6E-C11432E2098D> /usr/lib/liblzma.5.dylib
    0x7fffe9a91000 -     0x7fffe9aa7ff7  libmarisa.dylib (5) <2183D484-032D-3DE5-8984-3A14006E034E> /usr/lib/libmarisa.dylib
    0x7fffe9aa8000 -     0x7fffe9d4fff7  libmecabra.dylib (744.5) <EF046855-CB9C-32D8-B2F1-C85B526E386F> /usr/lib/libmecabra.dylib
    0x7fffe9d82000 -     0x7fffe9dfbff7  libnetwork.dylib (856.30.16) <66C6E4D6-B39C-3309-80C1-CBBE170DDD51> /usr/lib/libnetwork.dylib
    0x7fffe9dfc000 -     0x7fffea1ccd97  libobjc.A.dylib (706) <F9AFE665-A3A2-3285-9495-19803A565861> /usr/lib/libobjc.A.dylib
    0x7fffea1cf000 -     0x7fffea1d3fff  libpam.2.dylib (21.30.1) <71EB0D88-DE84-3C8D-A2C5-58AA282BC5BC> /usr/lib/libpam.2.dylib
    0x7fffea1d4000 -     0x7fffea204ff7  libpcap.A.dylib (67) <450DB888-2C0C-3085-A5F1-69324DFE902C> /usr/lib/libpcap.A.dylib
    0x7fffea222000 -     0x7fffea23effb  libresolv.9.dylib (64) <A244AE4C-00B0-396C-98FF-97FE4DB3DA30> /usr/lib/libresolv.9.dylib
    0x7fffea28e000 -     0x7fffea3d6fe3  libsqlite3.dylib (253) <B5BA5C96-AB13-34A0-8237-DD52A0181DFE> /usr/lib/libsqlite3.dylib
    0x7fffea4cb000 -     0x7fffea4d8fff  libxar.1.dylib (357) <58BFB84B-66FE-3299-AA3D-BBA178ADEE39> /usr/lib/libxar.1.dylib
    0x7fffea4dc000 -     0x7fffea5cbffb  libxml2.2.dylib (30.11) <E12AF929-0FA5-3214-840F-C81E6AC9F36E> /usr/lib/libxml2.2.dylib
    0x7fffea5cc000 -     0x7fffea5f5fff  libxslt.1.dylib (15.8) <FFF5DD45-F544-34B2-BE3C-DB877DC60081> /usr/lib/libxslt.1.dylib
    0x7fffea5f6000 -     0x7fffea607ff3  libz.1.dylib (67) <46E3FFA2-4328-327A-8D34-A03E20BFFB8E> /usr/lib/libz.1.dylib
    0x7fffea616000 -     0x7fffea61aff7  libcache.dylib (79) <0C8092D3-600F-3ADD-A036-F225B6CDCA43> /usr/lib/system/libcache.dylib
    0x7fffea61b000 -     0x7fffea626ff7  libcommonCrypto.dylib (60092.30.2) <B16E29B6-EC8D-3A8F-9A89-DD9CF35F7C4B> /usr/lib/system/libcommonCrypto.dylib
    0x7fffea627000 -     0x7fffea62efff  libcompiler_rt.dylib (62) <E992E8D9-037C-3454-A366-A25E4D31D6BB> /usr/lib/system/libcompiler_rt.dylib
    0x7fffea62f000 -     0x7fffea637fff  libcopyfile.dylib (138) <64E285D9-5485-333B-AEE7-8B0C8FB9275F> /usr/lib/system/libcopyfile.dylib
    0x7fffea638000 -     0x7fffea6bbfdf  libcorecrypto.dylib (442.30.20) <2074B932-FD79-30A9-8E90-AF25C49F2AF1> /usr/lib/system/libcorecrypto.dylib
    0x7fffea6bc000 -     0x7fffea6eefff  libdispatch.dylib (703.30.5) <EA0CC14E-D559-3802-B4B2-0E8C7579AAC4> /usr/lib/system/libdispatch.dylib
    0x7fffea6ef000 -     0x7fffea6f4ff3  libdyld.dylib (421.2) <6F506653-FFF6-3DB8-84F1-109AE3C52F32> /usr/lib/system/libdyld.dylib
    0x7fffea6f5000 -     0x7fffea6f5ffb  libkeymgr.dylib (28) <1A318923-1200-3B06-B432-5007D82F195D> /usr/lib/system/libkeymgr.dylib
    0x7fffea6f6000 -     0x7fffea702ffb  libkxld.dylib (3789.41.3) <87550136-9353-348B-9CD9-C342B48C5AAF> /usr/lib/system/libkxld.dylib
    0x7fffea703000 -     0x7fffea703fff  liblaunch.dylib (972.30.7) <15FACC21-079A-3BDF-9AFB-4253EFDEB587> /usr/lib/system/liblaunch.dylib
    0x7fffea704000 -     0x7fffea709fff  libmacho.dylib (894) <A2F38EC1-C37C-3B93-B0E4-36B07C177F8C> /usr/lib/system/libmacho.dylib
    0x7fffea70a000 -     0x7fffea70cff3  libquarantine.dylib (85) <C1D7749F-5F5F-3BB9-BEFC-1F0B9DA941FD> /usr/lib/system/libquarantine.dylib
    0x7fffea70d000 -     0x7fffea70effb  libremovefile.dylib (45) <CD42974E-BE0B-39FC-9BFC-8A7540A04DC6> /usr/lib/system/libremovefile.dylib
    0x7fffea70f000 -     0x7fffea727ff7  libsystem_asl.dylib (349.30.2) <EFAC72D7-CB13-3DF7-ADF3-EC6635C6F1EA> /usr/lib/system/libsystem_asl.dylib
    0x7fffea728000 -     0x7fffea728ff7  libsystem_blocks.dylib (67) <B8C3701D-5A91-3D35-999D-2DC8D5393525> /usr/lib/system/libsystem_blocks.dylib
    0x7fffea729000 -     0x7fffea7b6fef  libsystem_c.dylib (1158.30.7) <2F881962-03CB-3B9D-A782-D98C1BBA4E3D> /usr/lib/system/libsystem_c.dylib
    0x7fffea7b7000 -     0x7fffea7baffb  libsystem_configuration.dylib (888.30.2) <4FE3983C-E4ED-3939-A578-03AD29C99788> /usr/lib/system/libsystem_configuration.dylib
    0x7fffea7bb000 -     0x7fffea7befff  libsystem_coreservices.dylib (41.4) <1A572B9E-0C47-320F-8C64-7990D0A5FB5A> /usr/lib/system/libsystem_coreservices.dylib
    0x7fffea7bf000 -     0x7fffea7d7ff3  libsystem_coretls.dylib (121.31.1) <4676F06D-274D-31BE-B61C-4D7A4AEF4858> /usr/lib/system/libsystem_coretls.dylib
    0x7fffea7d8000 -     0x7fffea7defff  libsystem_dnssd.dylib (765.30.11) <DC708D84-ED7D-3936-B996-A67C66B8DDAA> /usr/lib/system/libsystem_dnssd.dylib
    0x7fffea7df000 -     0x7fffea808ff7  libsystem_info.dylib (503.30.1) <9ED9121C-F111-3FAD-BC2F-C95DEE1C9362> /usr/lib/system/libsystem_info.dylib
    0x7fffea809000 -     0x7fffea82bff7  libsystem_kernel.dylib (3789.41.3) <B75B128C-7D7A-3318-91CD-82B5A69C5329> /usr/lib/system/libsystem_kernel.dylib
    0x7fffea82c000 -     0x7fffea873fe7  libsystem_m.dylib (3121.4) <266DB92B-A86F-3691-80FB-1B26AD73CFF3> /usr/lib/system/libsystem_m.dylib
    0x7fffea874000 -     0x7fffea892ff7  libsystem_malloc.dylib (116.30.3) <F40DEE3B-386A-3529-A3F7-98117ED55BF4> /usr/lib/system/libsystem_malloc.dylib
    0x7fffea893000 -     0x7fffea8eaffb  libsystem_network.dylib (856.30.16) <4AE368E9-605D-379D-B04C-2AC7455B8250> /usr/lib/system/libsystem_network.dylib
    0x7fffea8eb000 -     0x7fffea8f4ff3  libsystem_networkextension.dylib (563.30.15) <EB020B0C-7DF0-3EEF-8E3C-15DA3C01D687> /usr/lib/system/libsystem_networkextension.dylib
    0x7fffea8f5000 -     0x7fffea8feff3  libsystem_notify.dylib (165.20.1) <E7FD3A7C-DD07-36E2-9FA4-7561F9F114DA> /usr/lib/system/libsystem_notify.dylib
    0x7fffea8ff000 -     0x7fffea907fe7  libsystem_platform.dylib (126.1.2) <3CA06D4E-C00A-36DE-AA65-3A390097D1F6> /usr/lib/system/libsystem_platform.dylib
    0x7fffea908000 -     0x7fffea912ff7  libsystem_pthread.dylib (218.30.1) <C869ED7C-BE29-3532-8E69-3A8DA1447EDC> /usr/lib/system/libsystem_pthread.dylib
    0x7fffea913000 -     0x7fffea916ff7  libsystem_sandbox.dylib (592.31.1) <7BBFDF96-293F-3DD9-B3A4-7C168280B441> /usr/lib/system/libsystem_sandbox.dylib
    0x7fffea917000 -     0x7fffea918fff  libsystem_secinit.dylib (24) <5C1F1E47-0F7D-3E25-8DEB-D9DB1F902281> /usr/lib/system/libsystem_secinit.dylib
    0x7fffea919000 -     0x7fffea920fff  libsystem_symptoms.dylib (532.30.6) <5D990CF5-B58F-39F7-B375-99B4EC62CFBD> /usr/lib/system/libsystem_symptoms.dylib
    0x7fffea921000 -     0x7fffea941ff7  libsystem_trace.dylib (518.30.7) <6D34D1EA-2A3C-3D2D-803E-A666E6AEEE52> /usr/lib/system/libsystem_trace.dylib
    0x7fffea942000 -     0x7fffea947ffb  libunwind.dylib (35.3) <9F7C2AD8-A9A7-3DE4-828D-B0F0F166AAA0> /usr/lib/system/libunwind.dylib
    0x7fffea948000 -     0x7fffea971ff7  libxpc.dylib (972.30.7) <65E41BB6-EBD5-3D93-B0BE-B190CEE4DD93> /usr/lib/system/libxpc.dylib

External Modification Summary:
  Calls made by other processes targeting this process:
    task_for_pid: 0
    thread_create: 0
    thread_set_state: 0
  Calls made by this process:
    task_for_pid: 0
    thread_create: 0
    thread_set_state: 0
  Calls made by all processes on this machine:
    task_for_pid: 731851
    thread_create: 0
    thread_set_state: 0

VM Region Summary:
ReadOnly portion of Libraries: Total=284.3M resident=0K(0%) swapped_out_or_unallocated=284.3M(100%)
Writable regions: Total=154.5M written=0K(0%) resident=0K(0%) swapped_out=0K(0%) unallocated=154.5M(100%)
 
                                VIRTUAL   REGION 
REGION TYPE                        SIZE    COUNT (non-coalesced) 
===========                     =======  ======= 
Accelerate framework               128K        2 
Activity Tracing                   256K        2 
CG backing stores                 7128K        5 
CG image                            36K        6 
CoreServices                        76K        2 
CoreUI image data                  456K        3 
CoreUI image file                  320K        6 
Kernel Alloc Once                    8K        2 
MALLOC                           118.4M       39 
MALLOC guard page                   48K       10 
Memory Tag 242                      12K        2 
STACK GUARD                       56.0M        9 
Stack                             11.6M        9 
VM_ALLOCATE                        148K       20 
__DATA                            22.2M      228 
__GLSLBUILTINS                    2588K        2 
__IMAGE                            528K        2 
__LINKEDIT                       117.6M       19 
__TEXT                           166.7M      228 
__UNICODE                          556K        2 
mapped file                       54.5M       20 
shared memory                     16.3M       11 
===========                     =======  ======= 
TOTAL                            575.3M      607 

Model: MacBookPro11,4, BootROM MBP114.0172.B13, 4 processors, Intel Core i7, 2.5 GHz, 16 GB, SMC 2.29f24
Graphics: Intel Iris Pro, Intel Iris Pro, Built-In
Memory Module: BANK 0/DIMM0, 8 GB, DDR3, 1600 MHz, 0x802C, 0x31364B544631473634485A2D314736453120
Memory Module: BANK 1/DIMM0, 8 GB, DDR3, 1600 MHz, 0x802C, 0x31364B544631473634485A2D314736453120
AirPort: spairport_wireless_card_type_airport_extreme (0x14E4, 0x152), Broadcom BCM43xx 1.0 (7.21.171.68.1a5)
Bluetooth: Version 5.0.3f1, 3 services, 27 devices, 1 incoming serial ports
Network Service: Wi-Fi, AirPort, en0
Serial ATA Device: APPLE SSD SM0256G, 251 GB
USB Device: USB 3.0 Bus
USB Device: USB3.0 Hub
USB Device: USB 10/100/1000 LAN
USB Device: Apple Internal Keyboard / Trackpad
USB Device: Bluetooth USB Host Controller
USB Device: USB2.0 Hub
USB Device: HyperX 7.1 Audio
USB Device: Hub
USB Device: USB Optical Mouse
USB Device: Dell USB Entry Keyboard
Thunderbolt Bus: MacBook Pro, Apple Inc., 27.1
```
