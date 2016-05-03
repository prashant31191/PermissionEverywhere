PermissionEverywhere alpha
=============
<img src='art/screenshot.png' width='270' height='480' />
<br>
Library enables to request a permission from any Context(Service, IntentService, etc). 
It creates a Notification with prompt, when user click notification,
opens a transparent Activity with our request to permission. 
When user accepts, it sends back as Callback or as boolean synchonised value.


##How to include:
###Gradle
```gradle
repositories {
    maven { url "https://jitpack.io" }
}
```

####Permission Everywhere
```gradle
dependencies {
     compile 'com.github.kaknazaveshtakipishi:PermissionEverywhere:alpha'
}
```


###Usage
###With Callback
```java

 PermissionEverywhere.getPermission(getApplicationContext(), 
            new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
                    REQ_CODE, 
                    "Notification title", 
                    "This app needs a write permission",
                    R.mipmap.ic_launcher)
                    .enqueue(new PermissionResultCallback() {
                                @Override
                                public void onComplete(PermissionResponse permissionResponse) {
                                    Toast.makeText(TestService.this, "is Granted " + permissionResponse.isGranted(), Toast.LENGTH_SHORT).show();
                                }
            });

```

###On the fly(synchronized)
```java

 @Override
  protected Boolean doInBackground(Void... params) {
      PermissionResponse response = PermissionEverywhere.getPermission(getApplicationContext(), 
      new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE},
              REQ_CODE,
              "Notification title", 
              "This app needs  a write permission", 
              R.mipmap.ic_launcher)
              .call();
      //waits..
      boolean isGranted = response.isGranted();

      if(isGrante){
      // Do stuff
      }
  }

```
