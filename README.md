# HTTP-Live-Streaming-Tools-zh

HTTP实时流媒体工具
HTTP实时流媒体（HLS）工具包安装了用于部署和验证HLS和低延迟HLS解决方案的命令行工具。

此包中包含的内容
• 媒体文件分段器
• 媒体字幕分段器
• 媒体流分段器
• 多种播放列表创建器
• 媒体流验证器
• HLS报告
• ID3标签生成器
• 低延迟HLS Golang脚本
• 低延迟HLS PHP脚本
• TS压缩器

工具概述

媒体文件分段器（**mediafilesegmenter**）将MOV，MP4，M4V，M4A或MP3文件划分为媒体段，并创建索引文件。它还可以执行段加密。索引文件和媒体段可以使用几乎任何网络服务器基础设施进行部署，以进行iOS，macOS和tvOS的流媒体传输。媒体文件分段器只生成点播（VOD）流。

媒体字幕分段器（**mediasubtitlesegmenter**）将Quicktime文件中的tx3g格式的字幕轨道或SRT文件转换为WebVTT，并将其分段以使用HLS进行部署。它也会接受WebVTT文件并进行分段。

媒体流分段器（**mediastreamsegmenter**）通过UDP网络连接或本地端口上的输入流接收MPEG-2传输流，并将其打包为HLS。它写入一个单独的实时媒体播放列表及其相应的媒体段（包括低延迟模式中的部分段）。它还可以执行段加密。它将其输出写入本地文件系统或WebDAV端点。实时媒体播放列表和段可以使用几乎任何网络服务器基础设施进行部署，以进行iOS，macOS和tvOS的流媒体传输。媒体流分段器生成实时流或VOD流。

多种播放列表创建器（**variantplaylistcreator**）与媒体文件分段器一起工作，从多个VOD流创建多种播放列表。由媒体文件分段器生成的多种播放列表传递给多种播放列表创建器。

媒体流验证器（mediastreamvalidator）模拟HLS会话并验证索引文件和媒体段是否符合HLS规范。它检查几个“最佳实践”以确保可靠的流式传输。如果发现任何错误或问题，将显示详细的诊断报告。可以使用--validation-data参数将验证数据写入JSON文件。

HLS报告（**hlsreport**）使用媒体流验证器生成的JSON文件为经过验证的流创建报告。

ID3标签生成器（**id3taggenerator**）创建ID3标签，以便用作媒体文件分段器的元数据，或通过网络将它们发送给媒体流分段器。

TS压缩器（**tsrecompressor**）生成并编码多达四个连续的音频和视频流，可以通过程序（从系统时钟派生的bip-bop图像）或通过从系统相机和麦克风捕获视频来实现。它以不同的比特率对流进行编码，并将它们作为MPEG-2传输流组播到本地UDP端口。

低延迟HLS Golang脚本（**ll-hls-origin-example.go**）实现了低延迟HLS媒体播放列表的HLS Origin API。

低延迟HLS PHP脚本（**lowLatencyHLS.php**）实现了低延迟HLS媒体播放列表的HLS Origin API。它可以用作低延迟HLS Golang脚本的替代方案。

系统要求
HLS工具包需要运行macOS 11.0 Big Sur或更高版本的Mac。
在实时编码多个比特率时，建议使用较新的硬件使用tsrecompressor工具。音频/视频捕捉需要由AVFoundation支持的摄像头和麦克风。
提供低延迟HLS流需要一个支持流优先级控制的HTTP/2服务器。大部分测试都是使用Apache进行的。（有关所需服务器配置的更多详细信息，请参阅“低延迟HLS的协议扩展”。）WebDAV必须配置为支持使用mediastreamsegmenter进行跨机器发布。
对于原型设计，将Apache设置在与其他工具相同的Mac上可能会比较方便。macOS附带的Apache版本可以配置为同时支持HTTP/2和PHP。
安装说明
要安装HLS工具，双击HTTP Live Streaming Tools.pkg并按照说明进行操作。安装程序将把这些工具安装到：
```
bash
Copy code
/usr/local/bin/hlsreport
/usr/local/bin/id3taggenerator
/usr/local/bin/mediafilesegmenter
/usr/local/bin/mediastreamsegmenter
/usr/local/bin/mediastreamvalidator
/usr/local/bin/mediasubtitlesegmenter
/usr/local/bin/tsrecompressor
/usr/local/bin/variantplaylistcreator
/usr/local/share/hlstools/ll-hls-origin-example.go
/usr/local/share/hlstools/lowLatencyHLS.php
```
安装程序将安装README文件到：
```
bash
Copy code
/usr/local/share/hlstools/readme.rtf
/usr/local/share/hlstools/README-LL.md
/usr/local/share/hlstools/README-GO.md
```
注意：安装程序将替换先前安装的文件版本。

请参阅man-pages以获取如何使用这些工具的详细说明。man-pages可以从命令行调
