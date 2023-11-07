# tugasUTS

<h1>Pemrogaman Mobile 1 | Teknik Informatika | Universitas Pelita Bangsa</h1>

NAMA  : Mochammad Raza Falevi <br>
Nim   : 312210156 <br>
Kelas : TI.22.B1 <br>
Mata kuliah : Pemrogaman Mobile


## * toast_activity.xml

### Membuat desain layout tampilan


<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    >
    <Button
        android:id="@+id/buttonToast"
        android:layout_width="408dp"
        android:layout_height="wrap_content"
        android:text="Tampilkan Toast"
        android:textAlignment="center"
        android:textStyle="bold"
        android:textColor="@color/white"
        android:backgroundTint="@color/Merah"/>

    <LinearLayout
        android:id="@+id/linear"
        android:layout_width="match_parent"
        android:layout_height="500dp"
        android:layout_below="@id/buttonToast"
        android:background="#eeeeee"
        android:gravity="center"
        android:orientation="vertical"
        android:paddingLeft="20dp"
        android:paddingRight="20dp"
        android:backgroundTint="@color/kuning">

        <TextView
            android:id="@+id/textNama"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="-50dp"
            android:layout_marginBottom="20dp"
            android:text="REZA BUDGET 312210156"
            android:textAlignment="center"
            android:textSize="24sp"
            android:backgroundTint="@color/kuning"/>

        <TextView
            android:id="@+id/textCount"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Tombol Hitung diklik sebanyak : 0"
            android:textAlignment="center"
            android:textSize="20sp" />

        <TextView
            android:id="@+id/textCountFibo"
            android:layout_width="375dp"
            android:layout_height="wrap_content"
            android:layout_marginTop="30dp"
            android:layout_marginBottom="-70dp"
            android:text="0"
            android:textAlignment="center"
            android:textColor="#000000"
            android:textSize="180sp"
            android:backgroundTint="@color/kuning"/>

    </LinearLayout>

    <Button
        android:id="@+id/buttonCount"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@id/linear"
        android:layout_marginStart="1dp"
        android:layout_marginLeft="1dp"
        android:layout_marginTop="3dp"
        android:text="HITUNG"
        android:textAlignment="center"
        android:textStyle="bold" />

    <Button
        android:id="@+id/buttonReset"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@id/buttonCount"
        android:layout_marginStart="1dp"
        android:layout_marginLeft="1dp"
        android:layout_marginTop="3dp"
        android:text="RESET"
        android:textStyle="bold" />

</RelativeLayout>

## * MainActivity.java

### MainActivity.java ini berfungsi untik memanggil layout activity dan value 

<br>

<br>

package com.example.tugastoast; <br>

import android.annotation.SuppressLint; <br>
import android.support.v4.app.RemoteActionCompatParcelizer; <br>
import android.os.Bundle; <br>
import android.view.View; <br>
import android.widget.Button; <br>
import android.widget.TextView; <br>
import android.widget.Toast; <br>

import androidx.appcompat.app.AppCompatActivity;

import com.example.tugastoast.R;

public class MainActivity extends AppCompatActivity {
    public int count = 0;
    public int countFibo = 0;
    public TextView showCount;
    public TextView showCountFibo;
    public Button buttonToast;
    public Button buttonCount;
    public Button buttonReset;
    public Toast toastA;

    @SuppressLint("MissingInflatedId")
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.toast_activity);
        buttonToast = (Button) findViewById(R.id.buttonToast);
        buttonCount = (Button) findViewById(R.id.buttonCount);
        buttonReset = (Button) findViewById(R.id.buttonReset);
        showCount = (TextView) findViewById(R.id.textCount);
        showCountFibo = (TextView) findViewById(R.id.textCountFibo);


        buttonToast.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (toastA != null) {
                    toastA.cancel();
                }
                toastA = Toast.makeText(getApplicationContext(), "Angka Fibonacci : " + countFibo, Toast.LENGTH_SHORT);
                toastA.show();
            }
        });

        buttonCount.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                calculate(view);
            }
        });

        buttonReset.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                reset(view);
            }
        });


    }

    protected void calculate(View view) {

        count++;
        countFibo = calculateFibo(count);
        showCount.setText("Tombol Hitung diklik sebanyak : " + Integer.toString(count));
        showCountFibo.setText(Integer.toString(countFibo));
        if (count % 7 == 0) {
            if (toastA != null) toastA.cancel();
            toastA = Toast.makeText(getApplicationContext(), "Tombol hitung diklik : " + count + " Kali", Toast.LENGTH_SHORT);
            toastA.show();
        }
    }

    protected int calculateFibo(int n) {
        if (n <= 1) return n;
        int prev, current, next;
        prev = 0;
        current = 1;
        for (int i = 2; i <= n; i++) {
            next = prev + current;
            prev = current;
            current = next;
        }
        return current;
    }

    protected void reset(View view) {
        count = 0;
        countFibo = 0;
        showCount.setText(Integer.toString(count));
        showCountFibo.setText(Integer.toString(countFibo));
    }
}


## * string.xml

### Membuat text tampilan

<resources>
    <string name="app_name">TugasToast</string>
    <string name="activity">activitymain</string>
</resources>


## * color.xml
### Membuat warna pada tampilan



<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="black">#FF000000</color>
    <color name="white">#FFFFFFFF</color>
    <color name="kuning">#FFFFEB3B</color>
    <color name="Merah">#F44336</color>
</resources>

