# Ex.No:2 Create a simple application client and server service using AIDL interface in android studio.


## AIM:

To create a AIDL interface and communicate the process between client and server using AIDL interface in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as CSAIDL and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display message give in MainActivity file(client/server).

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the client/server services using AIDL”.
Developed by:MANOJ CHOUDHARY V
Registeration Number :212221240025
*/
```
## MainActivity.java
```
package com.example.exp2aidl;

import androidx.appcompat.app.AppCompatActivity;

import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.content.ServiceConnection;
import android.os.Bundle;
import android.os.IBinder;
import android.os.RemoteException;
import android.text.Editable;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity  implements View.OnClickListener  {
    EditText edtFirstNumber,edtSecondNumber;
    Button btnMultiply;
    TextView txtMultiplyResult;
    MultiplyInterface myInterface;

    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        edtFirstNumber=(EditText) findViewById(R.id.edtFirstNumber);
        edtSecondNumber=(EditText) findViewById(R.id.edtSecondNumber);
        btnMultiply=(Button) findViewById(R.id.btnMultiply);
        txtMultiplyResult=(TextView) findViewById(R.id.textView);
        btnMultiply.setOnClickListener(MainActivity.this);
        Intent multiplyService =new Intent(MainActivity.this,MultiplicationService.class);
        bindService(multiplyService,myServiceConnection, Context.BIND_AUTO_CREATE);

    }
    ServiceConnection myServiceConnection =new ServiceConnection() {
        @Override
        public void onServiceConnected(ComponentName componentName, IBinder iBinder) {
            myInterface=MultiplyInterface.Stub.asInterface(iBinder);

        }

        @Override
        public void onServiceDisconnected(ComponentName componentName) {

        }
    };
    public void onClick(View view)
    {
        int firstNumber=Integer.parseInt(edtFirstNumber.getText().toString());
        int secondNumber=Integer.parseInt(edtSecondNumber.getText().toString());
        try{
            int result=myInterface.multiplyTwoValuesTogether(firstNumber,secondNumber);
            txtMultiplyResult.setText(result+"");
        }
        catch(RemoteException e)
        {
            e.printStackTrace();
        }

    }
}
```
## MultiplicationService.java
```
package com.example.exp2aidl;

import android.app.Service;
import android.content.Intent;
import android.os.IBinder;
//import android.app.
import android.os.RemoteException;

public class MultiplicationService extends Service {
    public MultiplicationService() {
    }

    @Override
    public IBinder onBind(Intent intent) {
        // TODO: Return the communication channel to the service.

        return myBinder;
    }
    MultiplyInterface.Stub myBinder=new MultiplyInterface.Stub() {
        @Override
        public int multiplyTwoValuesTogether(int firstNumber, int secondNumber)
                throws RemoteException {
            return firstNumber*secondNumber;
        }
    };
}
```
## MultipllyInterface.aidl
```
// MultiplyInterface.aidl
package com.example.exp2aidl;

// Declare any non-default types here with import statements

interface MultiplyInterface {

int multiplyTwoValuesTogether(int firstNumber,int secondNumber);
}
```
## activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/edtFirstNumber"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10"
        android:inputType="number" />

    <EditText
        android:id="@+id/edtSecondNumber"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10"
        android:inputType="number" />

    <Button
        android:id="@+id/btnMultiply"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Multiply" />

    <TextView
        android:id="@+id/textView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="TextView" />
</LinearLayout>
```

## OUTPUT
![](1.png)
![](2.png)
![](3.png)




## RESULT
Thus a Simple Android Application to create a AIDL interface and communicate the process between client and server using AIDL interface in Android Studio is developed and executed successfully.
