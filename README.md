![...](https://github.com/alraune91/Android-Studio-project-7/blob/main/Screenshot_4.png


import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.app.WindowDecorActionBar;

import android.annotation.SuppressLint;
import android.os.Bundle;
import android.text.TextUtils;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    EditText etNum1;
    EditText etNum2;
    Button btnDel;
    Button btnUmn;
    Button btnMin;
    Button btnPlus;
    Button btnC;
    TextView tvResult;
    String oper = "";
    final int MENU_RESET_ID = 1;
    final int MENU_QUIT_ID = 2;


    @SuppressLint("MissingInflatedId")
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        etNum1 = findViewById(R.id.et1);
        etNum2 = findViewById(R.id.et2);
        btnDel = findViewById(R.id.button1);
        btnUmn = findViewById(R.id.button2);
        btnMin = findViewById(R.id.button3);
        btnPlus = findViewById(R.id.button4);
        btnC = findViewById(R.id.button5);
        tvResult = findViewById(R.id.textView);

    }
    public boolean onCreateOptionsMenu(Menu menu){
        menu.add(0,MENU_RESET_ID, 0,"Reset");
        menu.add(0,MENU_QUIT_ID, 0,"Quit");
        return super.onCreateOptionsMenu(menu);
    }
    public boolean onOptionsItemSelected(MenuItem item){
        int itemId = item.getItemId();
        if (itemId == MENU_RESET_ID) {
            etNum1.setText("");
            etNum2.setText("");
            tvResult.setText("");
            Toast.makeText(this,"Очистка",Toast.LENGTH_LONG).show();
        } else if (itemId == MENU_QUIT_ID) {
            finish();
        }
        return super.onOptionsItemSelected(item);
    }



    public void onClick(View v){
        float num1 = 0;
        float num2 = 0;
        float result = 0;
        if (TextUtils.isEmpty(etNum1.getText().toString())
                || TextUtils.isEmpty((etNum2.getText().toString()))){
            return;
        }
        num1 = Float.parseFloat(etNum1.getText().toString());
        num2 = Float.parseFloat(etNum2.getText().toString());
        int id = v.getId();
        if (id == R.id.button4) {
            oper = "+";
            result = num1 + num2;
        } else if (id == R.id.button3) {
            oper = "-";
            result = num1 - num2;
        }
        else if (id == R.id.button2) {
            oper = "*";
            result = num1 * num2;
        } else if (id == R.id.button1) {
            if (num2!=0){
            oper = "/";
            result = num1 / num2;
        } else {
                v.setTextDirection(Integer.parseInt("0"));
                Toast.makeText(this,"Нельзя делить на ноль",Toast.LENGTH_LONG).show();
            }
        } else if (id == R.id.button5){
            Toast.makeText(this,"Очистка",Toast.LENGTH_LONG).show();
        }

        tvResult.setText(num1 + " "+ oper + " " + num2 + "=" + result);
    }
}
