# codeTlv
c++  做的tlv协议封装的数据

# 介绍
TLV即tag length value，广义上来讲他并不是一个固定格式的协议，他可以是人们自己定义的用来网络通讯的协议，只有遵循了定义人的装包解包流程才能建立通讯.

-  自定义消息格式
 
固定帧头| 指定TAG | 长度 | 值 | crc效验
------------ | ------------- | ------------- | ------------- | -------------
oxFD | ox1E | 5(Tlv最小的长度)+值得长度 | 值 | crc1+crc2(2个字节)
 
# 使用场景
比如蓝牙、wifi、NFC之间的数据传递,要求数据的安全和一致性


# 用法(只限于android arm64-v8a,只编译此架构的so库)

- 在项目(最外层)的build.gradle 下面添加仓库地址 

```
allprojects {
    repositories {
        google()
        jcenter()
        maven { url "https://github.com/oceanhub168pub/maven_repo/raw/master" }  // 这一句
    }
}
```
- 在项目中引用 
> api 'com.hub168.yh:CoderTlv-android:1.0.0@aar'
   
- 使用

public class TlvDataWarp {

    static {
        System.loadLibrary("tlvpack");
    }

    /**
     * 文本tlv格式封装
     * @param srcData  要封装的文本
     * @return
     */
    public static native byte[] tlvPackData(String srcData);

    /**
     * 解封装
     * @param packData  封装过的tlv格式文本
     * @return
     */
    public static native byte[] tlvUnpackData(byte[] packData);

}

  
