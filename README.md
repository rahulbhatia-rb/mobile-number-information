# MobileNo_Info

Demo project to find my IP Address in Android using REST (Retrofit Library)

https://market.mashape.com/ajith/indian-mobile-info

## activity_main.xml 

[Reference activity_main.xml](https://github.com/iamvickyav/MobileNo_Info/blob/master/app/src/main/res/layout/activity_main.xml)

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/mobile_no"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="39dp"
        android:ems="10"
        android:hint="Enter Mobile No"
        android:inputType="phone" />

    <Button
        android:id="@+id/submit"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="119dp"
        android:text="Submit" />

    <LinearLayout
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:weightSum="2"
        android:layout_below="@id/submit"
        android:paddingTop="30dp"
        android:orientation="horizontal">

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:orientation="vertical">

            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textSize="30sp"
                android:text="Number"/>

            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textSize="30sp"
                android:text="Series"/>

            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textSize="30sp"
                android:text="State"/>

            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textSize="30sp"
                android:text="Provider"/>

            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textSize="30sp"
                android:text="Service"/>

        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:orientation="vertical">

            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textSize="30sp"
                android:id="@+id/no"
                android:text=""/>

            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textSize="30sp"
                android:id="@+id/series"
                android:text=""/>

            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textSize="30sp"
                android:id="@+id/state"
                android:text=""/>

            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textSize="30sp"
                android:id="@+id/provider"
                android:text=""/>

            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textSize="30sp"
                android:id="@+id/service"
                android:text=""/>

        </LinearLayout>
    </LinearLayout>
</RelativeLayout>
 ```
 
## build.gradle (app)

```gradle
implementation 'com.squareup.retrofit2:retrofit:2.4.0'
implementation 'com.squareup.retrofit2:converter-gson:2.4.0'
```

 
## MainActivity.java
 
[Reference MainActivity java](https://github.com/iamvickyav/MobileNo_Info/blob/master/app/src/main/java/com/iamvickyav/jarvis/mobileno_data/MainActivity.java)
 
### Initialise Retrofit
 
 ```java
Retrofit retrofit = new Retrofit.Builder()
                .baseUrl("https://ajith-indian-mob-info.p.mashape.com/")
                .addConverterFactory(GsonConverterFactory.create())
                .build();
 ```
 
## MobileData.java
  
```java
public class MobileData {
    String Number;
    String Series;
    String State;
    String Provider;
    String Service;
}
```
  
## MobileDataService.java

```java
public interface MobileDataService {
    @GET("/getInfo")
    Call<MobileData> getMobileData(@Header("X-Mashape-Key") String header, @Query("mobno") String number);
}
```

## MainActivity.java

```java
MobileDataService mobileDataService = retrofit.create(MobileDataService.class);
mobileDataService.getMobileData("DUMMY_MASHAPE_CODE",number).enqueue(new Callback<MobileData>() {
            @Override
            public void onResponse(Call<MobileData> call, Response<MobileData> response) {
                MobileData mobileData = response.body();
                no.setText(mobileData.Number);
                series.setText(mobileData.Series);
                state.setText(mobileData.State);
                provider.setText(mobileData.Provider);
                service.setText(mobileData.Service);
            }

            @Override
            public void onFailure(Call<MobileData> call, Throwable t) {
                Toast.makeText(MainActivity.this, "Connection Issue", Toast.LENGTH_SHORT).show();
            }
});
```

## AndroidManifest.xml
```xml
<uses-permission android:name="android.permission.INTERNET"></uses-permission>
```
