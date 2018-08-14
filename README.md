#CompressTools-Android 压缩，图片压缩，压缩Bitmap


**特性：**

***这是和微信压缩效果类似的压缩方式，采用底层压缩。**

***尽量无损压缩图片，保持清晰度最优。可以对比原生方法bitmap.compress(CompressFormat.JPEG, quality, fileOutputStream);**

***占用内存少，支持压缩生成原图分辨率图片；**

***支持批量压缩，采用线程池提高性能**

***支持压缩监听回调**

***支持返回Bitmap和File**

**对比：**

| ImageInfo     | compressTool  | Wechat|
| ------------- |:-------------:| -----:|
| 1.50MB (1920x1080)| 47.32kb(1280*720) | 51.4kb(1280*720) |


**放两张效果图，大家可以看看效果是不是一样的。尺寸大小几乎一模一样！大家可以down下来，查看一下。**

这个是微信压缩后的图片：
![](https://github.com/lexluthors/CompressTools-Android/blob/master/app/src/main/assets/weixin_compress.jpg)


这个是采用该库压缩后的图片：
![](https://github.com/lexluthors/CompressTools-Android/blob/master/app/src/main/assets/android_compressTool.jpeg)



**使用方法：**

    compile 'com.jaywei:compresstool:1.2.1'

**1.2.1：**

    优化线程池


**1和2使用默认设置，默认设置最大宽高为720*960**

**1，压缩本地图片**

    CompressTools.getInstance(this).compressToFile(oldFile, new CompressTools.OnCompressListener()
    		{
    			@Override
    			public void onStart()
    			{

    			}
                @Override
			    public void onFail(String error)
			    {

				}
    			@Override
    			public void onSuccess(File file)
    			{

    			}
    		});

**2，压缩bitmap：**

    CompressTools.getDefault(this).compressToBitmap(oldFile, new CompressTools.OnCompressBitmapListener()
    		{
    			@Override
    			public void onStart()
    			{

    			}
                @Override
			    public void onFail(String error)
			    {

				}
    			@Override
    			public void onSuccess(Bitmap bitmap)
    			{

    			}
    		});

**3，自定义压缩File：**

   **注意：setKeepResolution(true)//设置是否保持原图分辨率，则设置的最大宽高就无效了,不需要设置最大宽高了。设置也不会报错了，该参数默认false**

    CompressTools.newBuilder(this).setMaxWidth(1080) // 默认最大宽度为720
    				.setMaxHeight(1920) // 默认最大高度为960
    				.setQuality(50) // 默认压缩质量为60,60足够清晰
    				//.setKeepResolution(true)//设置是否保持原图分辨率，则设置的最大宽高就无效了。不需要设置最大宽高了。设置也不会报错了，该参数默认false
    				.setCompressFormat(Bitmap.CompressFormat.JPEG) // 设置默认压缩为jpg格式
    				.setFileName("test1").setDestinationDirectoryPath(FileUtil.getPhotoFileDir().getAbsolutePath()).build()
    				.compressToFile(oldFile, new CompressTools.OnCompressListener()
    				{
    					@Override
    					public void onStart()
    					{

    					}
                        @Override
					    public void onFail(String error)
					    {

					    }
    					@Override
    					public void onSuccess(File file)
    					{
    					}
    				});

**4，自定义压缩bitmap：**

   **注意：setKeepResolution方法在压缩bitmap中无效，以最大宽高为准。**

    CompressTools.newBuilder(this).setMaxWidth(1080) // 默认最大宽度为720
    				.setMaxHeight(1920) // 默认最大高度为960
    				.setQuality(50) // 默认压缩质量为60,60足够清晰
    				.setCompressFormat(Bitmap.CompressFormat.JPEG) // 设置默认压缩为jpg格式
    				.setFileName("test2").setDestinationDirectoryPath(FileUtil.getPhotoFileDir().getAbsolutePath()).build()
    				.compressToBitmap(oldFile, new CompressTools.OnCompressBitmapListener()
    				{
    					@Override
    					public void onStart()
    					{

    					}

    					@Override
    					public void onSuccess(Bitmap bitmap)
    					{
    					}
    					@Override
                        public void onFail(String error)
                        {

                        }
    				});

**5，批量压缩：**

   **可以直接使用循环添加压缩任务，内部做了线程处理**

    for (int i = 0; i < 5; i++)
    		{
    			CompressTools.newBuilder(this).setMaxWidth(1280) // 默认最大宽度为720
    					.setMaxHeight(850) // 默认最大高度为960
    					.setQuality(50) // 默认压缩质量为60,60足够清晰
    					.setCompressFormat(Bitmap.CompressFormat.JPEG) // 设置默认压缩为jpg格式
    					// .setKeepResolution(true)//设置保持原图分辨率，则设置的最大宽高就无效了。不需要设置最大宽高了。设置也不会报错了，该参数默认false
    					.setFileName("test"+i).setDestinationDirectoryPath(FileUtil.getPhotoFileDir().getAbsolutePath()).build()
    					.compressToFile(oldFile, new CompressTools.OnCompressListener()
    					{
    						@Override
    						public void onStart()
    						{

    						}
                            @Override
			                 public void onFail(String error)
			                {

				            }
    						@Override
    						public void onSuccess(File file)
    						{

    						}
    					});
    		}



**写在最后：该项目是工作中使用的实例，我整理了一下，放到这里！如果对你有帮助希望能给个star或fork激励我继续坚持。**

有问题联系我：lexluthors@163.com








