# Beer-Adviser
Here, I made this project to as to learn how to use spinner and how to add values to them. I also learnt how to use drawables folder and give an icon image. 

XML code: 
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:paddingBottom="@dimen/activity_vertical_margin"
    tools:context="com.example.tanmayjha.beeradviser.FindBeerActivity">

    <Spinner
        android:id="@+id/color"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="37dp"
        android:entries="@array/beer_colors"
        ></Spinner>

    <Button
        android:id="@+id/find_beer"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignLeft="@+id/color"
        android:layout_below="@+id/color"
        android:text="@string/find_beer"
        android:clickable="false"
        android:onClick="onClickFindBeer" />

    <TextView
        android:id="@+id/brands"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignLeft="@+id/find_beer"
        android:layout_below="@+id/find_beer"
        android:layout_marginTop="18dp"
        android:text="@string/brands"
        />



</RelativeLayout>
--------------------------------------------------------------------------
Java code:
FindBeer.java

package com.example.tanmayjha.beeradviser;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Spinner;
import android.widget.TextView;

import java.util.List;

public class FindBeerActivity extends AppCompatActivity {
    private  BeerExpert expert=new BeerExpert();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_find_beer);
    }

    public void onClickFindBeer(View view)
    {
        TextView brands=(TextView)findViewById(R.id.brands);
        Spinner color=(Spinner)findViewById(R.id.color);
        String beertype=String.valueOf(color.getSelectedItem());
        List<String> brandslist=expert.getbrands(beertype);
        StringBuilder brandsFormatted = new StringBuilder();
        for(String brand: brandslist) {
            brandsFormatted.append(brand).append('\n');
        }
        brands.setText(brandsFormatted);
    }
}
Beerexpert.java
package com.example.tanmayjha.beeradviser;
import java.util.ArrayList;
import java.util.List;
/* Created by tanmay jha on 12-06-2016. */
public class BeerExpert {
    List<String> getbrands(String color){
        List<String> brands=new ArrayList<String>();
        if(color.equals("amber")) {
            brands.add("Jack Amber");
            brands.add("Red Moose");
        }
        else{
            brands.add("Jail Pale Ale");
            brands.add("Gout Stout");
        }
        return brands;
    }
}
--------------------------------------------------------------

Resource Files

<resources>
    <string name="app_name">Beer Adviser</string>
    <string name="find_beer">Find Beer!</string>
    <string name="brands"></string>
    <string-array name="beer_colors">
        <item>light</item>
        <item>amber</item>
        <item>brown</item>
        <item>dark</item>
    </string-array>
</resources>
