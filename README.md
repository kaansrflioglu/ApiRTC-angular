## Kurulum

1) "`npm install`" kullanarak gerekli moduller kurulacak.

2) "`npm install -g @ionic/cli`" ile ionic eklentisi kurulacak.

3) "`ng add @ionic/angular`" ile angular üzerinde ionic eklentisi kurulacak. 

4) "`ionic init`" ile proje ionicize edilip projeye "`ApiRTC-angular`" ismi verilecek.

5) "angular.json" dosyasında bulunan `"outputPath"` bölümü 
`"outputPath": "www",`
şeklinde değiştirilecek.

6) "src/index.html" dosyasının `<body></body>` bölümü
```
<body>
    <ion-content overflow-scroll="true">
        <app-root></app-root>
    </ion-content>
</body>
```
şeklinde değiştirilecek.

7) "`ionic build --project="ApiRTC-angular"`" komutu ile proje build edilecek.

8) "`ionic cap add android`" ile uygulamaya kapasitör eklenecek.

9) "`npm install @ionic-native/android-permissions`" kullanılarak android üzerindeki izinleri almamıza olanak sağlanacak.

10) "src/app/app.module.ts" konumundaki dosyaya aşağıdaki eklemeler yapılacak
```
import { AndroidPermissions } from '@ionic-native/android-permissions/ngx';
...
providers: [AndroidPermissions],
...
```
11) "src/app/app.component.ts" konumundaki dosyaya aşağıdaki eklemeler yapılacak
```
constructor(private fb: FormBuilder,
    private androidPermissions: AndroidPermissions) {

    this.androidPermissions.checkPermission(this.androidPermissions.PERMISSION.CAMERA).then(
      result => console.log('Has permission?', result.hasPermission),
      err => this.androidPermissions.requestPermission(this.androidPermissions.PERMISSION.CAMERA)
    );

    this.androidPermissions.requestPermissions([this.androidPermissions.PERMISSION.CAMERA, this.androidPermissions.PERMISSION.GET_ACCOUNTS]);
}
```

12) "`ionic cap open android`" komutu ile android studio açılacak.

13) "AndroidManifest.xml" üzerinde permissions bölümüne aşağıdaki izinler eklenecek
```
<uses-feature
    android:name="android.hardware.camera"
    android:required="false" />

<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.INTERNET" />
```
