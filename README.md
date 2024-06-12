# Age Calculator Application

The following is the screenshots of an application which is used to calculate the age of an individual when date of bith is passed as input.

## activity_main.xml
```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/etDateOfBirth"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Date of Birth (YYYY-MM-DD)"
        android:inputType="date"
        android:layout_margin="16dp"
        android:layout_centerHorizontal="true"/>

    <Button
        android:id="@+id/btnCalculateAge"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Calculate Age"
        android:layout_below="@id/etDateOfBirth"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="16dp"/>

    <TextView
        android:id="@+id/tvAgeResult"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text=""
        android:textSize="18sp"
        android:layout_below="@id/btnCalculateAge"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="16dp"/>
</RelativeLayout>
```


## Mainactivity.java
```java
package com.example.agecalucaltor;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;
import java.time.LocalDate;
import java.time.Period;

public class MainActivity extends AppCompatActivity {

    private EditText etDateOfBirth;
    private Button btnCalculateAge;
    private TextView tvAgeResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(getResources().getIdentifier("activity_main", "layout", getPackageName()));
        etDateOfBirth = findViewById(getResources().getIdentifier("etDateOfBirth", "id", getPackageName()));
        btnCalculateAge = findViewById(getResources().getIdentifier("btnCalculateAge", "id", getPackageName()));
        tvAgeResult = findViewById(getResources().getIdentifier("tvAgeResult", "id", getPackageName()));

        btnCalculateAge.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                calculateAge();
            }
        });
    }

    private void calculateAge() {
        String dobString = etDateOfBirth.getText().toString();
        if (dobString.isEmpty()) {
            tvAgeResult.setText("Please enter your date of birth.");
            return;
        }

        try {
            LocalDate dob = LocalDate.parse(dobString);
            LocalDate currentDate = LocalDate.now();

            if (dob.isAfter(currentDate)) {
                tvAgeResult.setText("Date of birth cannot be in the future.");
                return;
            }

            Period age = Period.between(dob, currentDate);
            int years = age.getYears();
            int months = age.getMonths();
            int days = age.getDays();

            tvAgeResult.setText("Your age is " + years + " years, " + months + " months, and " + days + " days.");
        } catch (Exception e) {
            tvAgeResult.setText("Invalid date format. Please use YYYY-MM-DD.");
        }
    }
}
```

## Output Screenshots
![WhatsApp Image 2024-06-12 at 20 54 08](https://github.com/Deekshith19/Android_Security/assets/56424454/f3bd1b66-06ac-4d05-9205-75460f218431)  __
![WhatsApp Image 2024-06-12 at 20 52 39](https://github.com/Deekshith19/Android_Security/assets/56424454/dd8e24bf-8004-43bf-9e9d-5e08b463450d)



