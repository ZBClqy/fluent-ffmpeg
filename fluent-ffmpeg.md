# fluent-ffmpeg视频切片

首先这只是个node的插件通过js去操控本地的ffmpeg所以一定要确定我们本地安装了ffmpeg

做我们的m3u8视频切片示例如下

const ffmpeg=require('fluent-ffmpeg')

//首先导入我们的fluent-ffmpeg插件

ffmpeg("要切片的文件地址")

.videoCodec('libx264')//这里设置我们的视频编码

.format('hls')//这里我们选择传输协议为hls

.outputOption('-hls_list_size 0')//这里设置我们的输出配置文件列表大小设置0表示读取全部

.outputOption('-hls_time 10')//这里设置我们每片信息的大小我这里设置为10秒

.output//这里设置输出的m3u8文件存放的位置

.on('progress',(progress)=>{

​	console.log(progress.percent)//这里可以设置监听我们的切片进度

})

.on('end',()=>{

​	console.log("切片完成")//当我们切片完成时触发这个监听

})

.run()//最后执行我们的切片等待即可