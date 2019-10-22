####1.info.plist注册文件类型
在**info.plist**文件中，添加一个新的属性**CFBundleDocumentTypes**，这是一个数组类型的属性,这里可以注册等多个类型。![1x.png](https://upload-images.jianshu.io/upload_images/6941348-8accc2446d0a9b7d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
或者在info.plist文件中以Source code的方式添加以下代码：
````
	<key>CFBundleDocumentTypes</key>
	<array>
		<dict>
			<key>CFBundleTypeName</key>
			<string>BIN</string>
			<key>LSHandlerRank</key>
			<string>Owner</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>com.apple.macbinary-​archive</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeName</key>
			<string>PDF</string>
			<key>LSHandlerRank</key>
			<string>Owner</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>com.adobe.pdf</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeName</key>
			<string>Microsoft Word</string>
			<key>LSHandlerRank</key>
			<string>Alternate</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>com.microsoft.word.doc</string>
				<string>com.microsoft.word.wordml</string>
				<string>org.openxmlformats.wordprocessingml.document</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeName</key>
			<string>Microsoft Excel</string>
			<key>LSHandlerRank</key>
			<string>Alternate</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>com.microsoft.excel.xls</string>
				<string>org.openxmlformats.spreadsheetml.sheet</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeIconFiles</key>
			<array/>
			<key>CFBundleTypeName</key>
			<string>Microsoft PowerPoint</string>
			<key>LSHandlerRank</key>
			<string>Alternate</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>com.microsoft.powerpoint.​ppt</string>
				<string>org.openxmlformats.presentationml.presentation</string>
				<string>public.presentation</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeName</key>
			<string>Text</string>
			<key>LSHandlerRank</key>
			<string>Alternate</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>public.text</string>
				<string>public.plain-text</string>
				<string>public.utf8-plain-text</string>
				<string>public.utf16-external-plain-​text</string>
				<string>public.utf16-plain-text</string>
				<string>com.apple.traditional-mac-​plain-text</string>
				<string>public.source-code</string>
				<string>public.c-source</string>
				<string>public.objective-c-source</string>
				<string>public.c-plus-plus-source</string>
				<string>public.objective-c-plus-​plus-source</string>
				<string>public.c-header</string>
				<string>public.c-plus-plus-header</string>
				<string>com.sun.java-source</string>
				<string>public.script</string>
				<string>public.shell-script</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeName</key>
			<string>Rich Text</string>
			<key>LSHandlerRank</key>
			<string>Alternate</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>public.rtf</string>
				<string>com.apple.rtfd</string>
				<string>com.apple.flat-rtfd</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeName</key>
			<string>HTML</string>
			<key>LSHandlerRank</key>
			<string>Alternate</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>public.html</string>
				<string>public.xhtml</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeName</key>
			<string>Web Archive</string>
			<key>LSHandlerRank</key>
			<string>Alternate</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>com.apple.webarchive</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeName</key>
			<string>Image</string>
			<key>LSHandlerRank</key>
			<string>Alternate</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>public.image</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeName</key>
			<string>iWork Pages</string>
			<key>LSHandlerRank</key>
			<string>Alternate</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>com.apple.page.pages</string>
				<string>com.apple.iwork.pages.pages</string>
				<string>com.apple.iwork.pages.template</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeName</key>
			<string>iWork Numbers</string>
			<key>LSHandlerRank</key>
			<string>Alternate</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>com.apple.numbers.numbers</string>
				<string>com.apple.iwork.numbers.numbers</string>
				<string>com.apple.iwork.numbers.template</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeName</key>
			<string>iWork Keynote</string>
			<key>LSHandlerRank</key>
			<string>Alternate</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>com.apple.keynote.key</string>
				<string>com.apple.iwork.keynote.key</string>
				<string>com.apple.iwork.keynote.kth</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeName</key>
			<string>Audio</string>
			<key>LSHandlerRank</key>
			<string>Alternate</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>public.audio</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeName</key>
			<string>Movie</string>
			<key>LSHandlerRank</key>
			<string>Alternate</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>public.movie</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeName</key>
			<string>Archive</string>
			<key>LSHandlerRank</key>
			<string>Alternate</string>
			<key>LSItemContentTypes</key>
			<array>
				<string>public.archive</string>
			</array>
		</dict>
	</array>
````
或者可以根据自己的需求更改，在[这里](https://developer.apple.com/library/archive/documentation/Miscellaneous/Reference/UTIRef/Articles/System-DeclaredUniformTypeIdentifiers.html)有文件后缀和 UTI 的对应表,可以查看是否支持文件共享。添加好键值对之后就代表已经成功的注册好了App支持的文件类型，运行Xcode，然后再到第三方App如QQ打开一个QQ不支持打开的文件，会显示用其他应用打开，点击的话会出现系统的弹框：![2x.png](https://upload-images.jianshu.io/upload_images/6941348-e97d8e9e06723c5d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
####2.获取共享文件
````
#define HSFolderName @"Inbox"
- (NSArray *)getAllFile
{
    NSFileManager *fileManager = [NSFileManager defaultManager];
    NSString *path = [[NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) firstObject] stringByAppendingPathComponent:HSFolderName];
    NSArray *files = [fileManager contentsOfDirectoryAtPath:path error:nil];
    NSMutableArray *dataSource = [NSMutableArray array];

    if (files.count < 1) {
        return dataSource;
    }

    for (NSString *fileString in files) {
        FileShareModel *model = [[FileShareModel alloc] init];
        if ([fileString rangeOfString:@".bin"].location !=NSNotFound) {
            model.fileUrl =  [[NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) lastObject] stringByAppendingPathComponent:[NSString stringWithFormat:@"%@/%@",HSFolderName,fileString]];
            model.fileName = fileString;
            [dataSource addObject:model];
        }
    }
    return dataSource;
}
````
[Demo](https://github.com/DQXSY/FileShare1)



