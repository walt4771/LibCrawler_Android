# LibCrawler - 안양시립도서관 노트북실 대기번호 알림앱
이 문서는 'LibCrawler - 안양시립도서관 노트북실 대기번호 알림앱'(이하 앱)의 개인정보처리방침에 대한 문서입니다. 
앱 주요 코드, 설명과 민감한 권한 요청 사유를 포함하고 있습니다. <br>
앱의 Source Code는 이 Repository에 게시되며 메인 컴퓨터와 동기화됩니다. 

**이 앱은 인터넷 권한을 HTML 데이터를 가져올 때 사용하며**
**전화번호 열람은 본인의 전화로 메세지를 보내기 위해 사용합니다.**
**또한 어떠한 정보도 외부로 전달하지 않습니다.**

# Updates

> 2022.03.28
```
deleted Message Alert
```

> 2022.03.27
```
check `waitNum` before first `NotiIntentService` alarm starts
```

> 2022.03.25
```
optimize application logic, logic has been slightly changed
```

> 2022.03.24
```
Dark Mode support, change recepit image due to Dark Mode support
```

> 2022.03.17
```
add fab for a better accessability, recepit image adjustment
```

# Permissions
1.
```xml
<!-- Internet Access -->
<uses-permission android:name="android.permission.INTERNET" />  
```
첫 번째 권한은 **인터넷 접속**에 대한 권한입니다. 
이 권한이 없으면 다음 에러가 발생합니다
```
No Network Security Config specified, using platform default  
```

  그리고 안양시립도서관 홈페이지는 
  http://222.233.168.6:8094와 같이 `https 통신` 을 사용하지 않아 
  `usesCleartextTraffic` 을 허용해 앱이 정상적으로 데이터를 가져오도록 했습니다.

```xml
<application  
  ...
  android:networkSecurityConfig="@xml/network_security_config"  
  ... 
  android:usesCleartextTraffic="true">  
 <activity...
```

<br><br>  2. 
```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" /> 
```
두 번째 권한은 **비행기 모드의 확인**을 위한 권한입니다.  

버튼을 누르기 전 앱은 비행기모드 여부를 확인 후 인터넷 접속을 시도합니다. 
비행기모드 검증을 위한 함수는 다음과 같습니다. 
```Kotlin
private fun isAirplaneModeOn(context: Context): Boolean {  
    return Settings.Global.getInt(context.contentResolver, Settings.Global.AIRPLANE_MODE_ON, 0) != 0;  
}
```
