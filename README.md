
# Ex.No:3 Design an android application Send SMS using Intent.


## AIM:

To create and design an android application Send SMS using Intent using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Latest Version)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as smsintent and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Send SMS and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to create and design an android application Send SMS using Intent.
*/
```
## activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:background="#FFF0F5">

    <Button
        android:id="@+id/btnSendSMS"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Send SMS"
        android:backgroundTint="@android:color/holo_blue_light"
        android:layout_centerInParent="true" />

</RelativeLayout>
```
## MainActivity.java
```
package com.example.sendsmsapp;

import android.Manifest;
import android.content.Intent;
import android.content.pm.PackageManager;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

public class MainActivity extends AppCompatActivity {

    private static final int SMS_PERMISSION_CODE = 101;
    Button btnSendSMS;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        btnSendSMS = findViewById(R.id.btnSendSMS);

        btnSendSMS.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // Check if SMS permission is granted
                if (ContextCompat.checkSelfPermission(MainActivity.this,
                        Manifest.permission.SEND_SMS) != PackageManager.PERMISSION_GRANTED) {
                    ActivityCompat.requestPermissions(MainActivity.this,
                            new String[]{Manifest.permission.SEND_SMS}, SMS_PERMISSION_CODE);
                } else {
                    sendSMS();
                }
            }
        });
    }

    private void sendSMS() {
        String phone = "9840155373";   // Replace with target phone number
        String message = "Hello, this is an SMS using Intent!";

        Intent smsIntent = new Intent(Intent.ACTION_VIEW);
        smsIntent.setData(Uri.parse("smsto:" + phone));
        smsIntent.putExtra("sms_body", message);

        try {
            startActivity(smsIntent);
        } catch (Exception e) {
            Toast.makeText(this, "SMS failed: " + e.getMessage(), Toast.LENGTH_LONG).show();
        }
    }

    // Handle permission result
    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions,
                                           @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);

        if (requestCode == SMS_PERMISSION_CODE) {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                sendSMS();
            } else {
                Toast.makeText(this, "Permission denied to send SMS", Toast.LENGTH_SHORT).show();
            }
        }
    }
}
```


## OUTPUT

<img width="1667" height="1028" alt="image" src="https://github.com/user-attachments/assets/9f84a8ec-7b14-4868-af4e-ec0511232573" />
<img width="1663" height="1045" alt="image" src="https://github.com/user-attachments/assets/8c8f471b-e6ca-4b0d-8fbe-1398cf970e2d" />



## RESULT
Thus a Simple Android Application create and design an android application Send SMS using Intent using Android Studio is developed and executed successfully.
