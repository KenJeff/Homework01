Software Engineering Homework 1
This project is a simple mobile application that performs two functions. The two parts, Part1 and Part2, are separate of each other but implemented in the same application. The java documents to be included are

MainActivity.java
Part1.java
Part2.java
Code Sections
MainActivity.java
This MainActivity code is the initial screen that is launched when the app is opened. The MainActivity contains two buttons that correspond to each of the two activities. Upon pressing the button, the user will be able to navigate to the desired activity.



package basic.app.homework1;
 
import android.content.Intent;
import android.os.Bundle;
 
import androidx.appcompat.app.AppCompatActivity;
 
import android.view.View;
import android.widget.Button;
 
 
public class MainActivity extends AppCompatActivity {
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
 
        setContentView(R.layout.activity_main);
 
        Button numOne = findViewById(R.id.Part1);
        numOne.setOnClickListener(v -> {
            startActivity(new Intent(MainActivity.this, Part1Activity.class));
        });
        Button numTwo = findViewById(R.id.Part2);
        numTwo.setOnClickListener(v -> {
            startActivity(new Intent(MainActivity.this, Part2Activity.class));
        });
    }
 
}
Part1.java
This Part1 code is a single UI containing one textfield and one button. The intial text within the textfield will prompt the user to enter text and to tap the button to change the color. When the button is pressed, the text will then change to the color that was randomly generated. The HTML color code is also displayed.

package basic.app.homework1;
 
import android.graphics.Color;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
 
import com.google.android.material.textfield.TextInputEditText;
 
import java.util.Random;
 
import androidx.appcompat.app.AppCompatActivity;
 
public class Part1Activity extends AppCompatActivity {
 
    private TextInputEditText etColor;
    private TextView colorType;
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_part1);
 
        colorType = findViewById(R.id.colorType);
        etColor = findViewById(R.id.et_color);
 
        Button btnColor = findViewById(R.id.btn_color);
        btnColor.setOnClickListener(v -> change(v));
    }
 
    public void change(View view) {
 
        Random obj = new Random();
 
        int red = obj.nextInt(256);
        int blue = obj.nextInt(256);
        int green = obj.nextInt(256);
 
        int realColor = Color.argb(255, red, blue, green);
        etColor.setTextColor(realColor);
 
        String tColor = String.format("Color %02dr , %02dg , %02db , #%02x%02x%02x", red, green, blue, red, green, blue);
        colorType.setText(tColor);
    }
}
Part2.java
This Part2 code creates a drawing panel for the user. The user will be able to select any color they like. The UI will have mechanisms to clear the drawing panel and to save their drawings.

package basic.app.homework1;
 
import android.os.Bundle;
 
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.LinearLayout;
import android.app.AlertDialog;
import android.app.Dialog;
import android.content.DialogInterface;
import android.view.View.OnClickListener;
 
import androidx.appcompat.app.AppCompatActivity;
 
public class Part2Activity extends AppCompatActivity implements OnClickListener
{
    private DrawingView drawView;
    private float sBrush, mBrush, lBrush;
    private Button newBtn;
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_part2);
        drawView = findViewById(R.id.drawing);
        EditText redBtn = findViewById(R.id.red_val);
        EditText grnBtn = findViewById(R.id.green_val);
        EditText blueBtn = findViewById(R.id.blue_val);
 
        sBrush = getResources().getInteger(R.integer.small_size);
        mBrush = getResources().getInteger(R.integer.medium_size);
        lBrush = getResources().getInteger(R.integer.large_size);
 
        redBtn.setOnClickListener(v -> paintColor(v));
        grnBtn.setOnClickListener(v -> paintColor(v));
        blueBtn.setOnClickListener(v -> paintColor(v));
 
        newBtn = findViewById(R.id.new_btn);
        newBtn.setOnClickListener(this);
    }
 
    @Override
    public void onClick(View view)
    {
        if(view.getId()==R.id.new_btn)
        {
            AlertDialog.Builder newDialog = new AlertDialog.Builder(this);
            newDialog.setTitle("New drawing");
            AlertDialog.Builder builder = newDialog.setMessage("Start new drawing (you will lose the current drawing)?");
            builder.setPositiveButton("Yes", new DialogInterface.OnClickListener(){
                public void onClick(DialogInterface dialog, int which){
                    drawView.newStart();
                    dialog.dismiss();
                }
            });
            newDialog.setNegativeButton("Cancel", new DialogInterface.OnClickListener(){
                public void onClick(DialogInterface dialog, int which){
                    dialog.cancel();
                }
            });
            newDialog.show();
        }
    }
    public void paintColor(View view)
    {
            EditText redBtn = findViewById(R.id.red_val);
            EditText grnBtn = findViewById(R.id.green_val);
            EditText blueBtn = findViewById(R.id.blue_val);
 
            int red = Integer.parseInt(redBtn.getText().toString());
            int green = Integer.parseInt(grnBtn.getText().toString());
            int blue = Integer.parseInt(blueBtn.getText().toString());
 
            drawView.setColor(red, green, blue);
    }
}
Design
The project is designed by using separate activities to navigate between the desired parts of the app. The save image function was not completed and the drawing paths reset color after the path is recorded. The user will be able to switch in between activities whenever is pleased. The functionality of the app is targeted for the end user.
