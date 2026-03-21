# Assignment-1
MainActivity.kt 

@file:Suppress("unused")

package com.example.assignment_1

import android.annotation.SuppressLint
import android.os.Bundle
import android.widget.Button
import android.widget.EditText
import android.widget.TextView
import android.widget.Toast
import androidx.activity.enableEdgeToEdge
import androidx.appcompat.app.AppCompatActivity
import androidx.core.view.ViewCompat
import androidx.core.view.WindowInsetsCompat

@Suppress("SameParameterValue")
class MainActivity : AppCompatActivity() {
    private lateinit var editTextTimeOfDay: EditText
    private lateinit var textViewSuggestion: TextView
    private lateinit var buttonGetSuggestion: Button
    private lateinit var buttonReset: Button



    @SuppressLint("SetTextI18n")
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContentView(R.layout.activity_main)
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main)) { v, insets ->
            val systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars())
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom)
            insets
        }
        editTextTimeOfDay = findViewById(R.id.editTextTimeOfDay)
        textViewSuggestion = findViewById(R.id.textViewSuggestion)
        buttonGetSuggestion = findViewById(R.id.buttonGetSuggestion)
        buttonReset = findViewById(R.id.buttonReset)
//Set click listener for the Get Suggestion button
buttonGetSuggestion.setOnClickListener {
    //Get suggestion based on input time of day
    val timeOfDay = editTextTimeOfDay.text.toString().trim().lowercase()
    val suggestion = getSocialSparkSuggestion(timeOfDay)

    if (suggestion.isNotEmpty()) {
        textViewSuggestion.text = suggestion
    } else {
        Toast.makeText(this, "Please enter a valid time of day", Toast.LENGTH_SHORT).show()

    }
}
        //Set click listener for the Reset button
        buttonReset.setOnClickListener {
            editTextTimeOfDay.text.clear()
            textViewSuggestion.text = "Suggestion will appear here"
        }
    }
    //Function to get suggestion based on input time of day
    private fun getSocialSparkSuggestion(timeOfDay: String): String {
        return when (timeOfDay) {
          "morning"->"Send a'Good morning text to a family member."
          "mid-morning"->"Reach out to a colleague with quick'Thank you.'"
          "afternoon"->"Share a funny meme or interesting link with a friend."
          "afternoon snack time"->"Send a quick 'thinking of you' message."
          "dinner"->"Call a friend or relative for a 5-minute catch-up."
          "after dinner","night"->"Leave a thoughtful comment on a friend's post."
          else -> ""//Return empty if invalid input

        }
      
  Activity_main.xml
  
        <?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#E41111"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/editTextTimeOfDay"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:ems="10"
        android:inputType="text"
        android:text="Name"
        app:layout_constraintBottom_toTopOf="@+id/textViewSuggestion"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/imageView2" />

    <TextView
        android:id="@+id/textViewSuggestion"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Display"
        android:textSize="34sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:text="Display" />

    <Button
        android:id="@+id/buttonReset"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:allowUndo="true"
        android:background="#E7D8D8"
        android:text="Reset"
        android:textColorLink="#F38C2727"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toStartOf="@+id/buttonGetSuggestion"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textViewSuggestion" />

    <ImageView
        android:id="@+id/imageView2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:layout_constraintBottom_toTopOf="@+id/editTextTimeOfDay"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.414"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:srcCompat="@drawable/img_1" />

    <Button
        android:id="@+id/buttonGetSuggestion"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:allowUndo="true"
        android:background="#FF0000"
        android:text="Submit"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@+id/buttonReset"
        app:layout_constraintTop_toBottomOf="@+id/textViewSuggestion" />

</androidx.constraintlayout.widget.ConstraintLayout>
    }
}
