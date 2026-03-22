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
  
  <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android" xmlns:app="http://schemas.android.com/apk/res-auto" xmlns:tools="http://schemas.android.com/tools" android:id="@+id/main" android:layout_width="match_parent" android:layout_height="match_parent" android:background="#2196F3" tools:context=".MainActivity">
<EditText android:id="@+id/editTextTimeOfDay" android:layout_width="wrap_content" android:layout_height="wrap_content" android:ems="10" android:inputType="text" android:text="Name" app:layout_constraintBottom_toTopOf="@+id/textViewSuggestion" app:layout_constraintEnd_toEndOf="parent" app:layout_constraintStart_toStartOf="parent"/>

<TextView android:id="@+id/textViewSuggestion" android:layout_width="wrap_content" android:layout_height="wrap_content" android:text="Display" android:textSize="34sp" app:layout_constraintBottom_toBottomOf="parent" app:layout_constraintEnd_toEndOf="parent" app:layout_constraintHorizontal_bias="0.501" app:layout_constraintStart_toStartOf="parent" app:layout_constraintTop_toTopOf="parent" app:layout_constraintVertical_bias="0.518" tools:text="Display"/>

<ImageView android:id="@+id/imageView" android:layout_width="261dp" android:layout_height="264dp" app:layout_constraintBottom_toTopOf="@+id/editTextTimeOfDay" app:layout_constraintEnd_toEndOf="parent" app:layout_constraintStart_toStartOf="parent" app:layout_constraintTop_toTopOf="parent" app:srcCompat="@drawable/dayyime"/>

<Button android:id="@+id/buttonReset" android:layout_width="wrap_content" android:layout_height="wrap_content" android:layout_marginStart="135dp" android:layout_marginTop="212dp" android:layout_marginEnd="96dp" android:layout_marginBottom="116dp" android:text="Reset" app:layout_constraintBottom_toBottomOf="parent" app:layout_constraintEnd_toStartOf="@+id/buttonGetSuggestion" app:layout_constraintStart_toStartOf="parent" app:layout_constraintTop_toBottomOf="@+id/editTextTimeOfDay"/>

<Button android:id="@+id/buttonGetSuggestion" android:layout_width="wrap_content" android:layout_height="wrap_content" android:layout_marginStart="96dp" android:layout_marginTop="212dp" android:layout_marginEnd="135dp" android:layout_marginBottom="116dp" android:text="Submit" app:layout_constraintBottom_toBottomOf="parent" app:layout_constraintEnd_toEndOf="parent" app:layout_constraintStart_toEndOf="@+id/buttonReset" app:layout_constraintTop_toBottomOf="@+id/editTextTimeOfDay"/>
</androidx.constraintlayout.widget.ConstraintLayout>
