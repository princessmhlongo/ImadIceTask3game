package com.example.myice


import android.os.Bundle
import android.widget.ImageView
import android.widget.TextView
import androidx.activity.enableEdgeToEdge
import androidx.appcompat.app.AppCompatActivity
import com.example.imadicetask.R
import kotlin.random.Random

private val Any.activity_main: Any
    get() {
        TODO("Not yet implemented")
    }

class MainActivity : AppCompatActivity() {

    private lateinit var resultTextView: TextView
    private lateinit var computerChoiceImageView: ImageView
    private lateinit var rockImageView: ImageView
    private lateinit var paperImageView: ImageView
    private lateinit var scissorsImageView: ImageView


    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContentView(R.layout.activity_main)

        resultTextView = findViewById(R.id.resultTextView)
        computerChoiceImageView = findViewById(R.id.computerChoiceImageView)
        rockImageView = findViewById(R.id.rockImageView)
        paperImageView = findViewById(R.id.paperImageView)
        scissorsImageView = findViewById(R.id.scissorsImageView)


        attachClickListener(rockImageView, "Rock")
        attachClickListener(paperImageView, "Paper")
        attachClickListener(scissorsImageView, "Scissors")


    }


    private fun attachClickListener(imageView: ImageView, choice: String) {
        imageView.setOnClickListener {
            playGame(choice)
        }
    }

    private fun playGame(Choice: String) {
        val choices = listOf("Rock", "Paper", "Scissors")
        val computerChoice = choices[ Random.nextInt(3)]



        //set computer Choice image
        when(computerChoice){
            "rock"->computerChoiceImageView.setImageResource(R.drawable.rock)
        }
        when(computerChoice){
            "paper"->computerChoiceImageView.setImageResource(R.drawable.paper)
        }
        when(computerChoice){
            "scissors"->computerChoiceImageView.setImageResource(R.drawable.scissors)
        }
        computerChoiceImageView.setImageResource(computerChoice)


       val result = when {
            Choice == computerChoice -> "It's a tie!"
            Choice == "Rock" && computerChoice == "Scissors" ||
                    Choice == "Paper" && computerChoice == "Rock" ||
                    Choice == "Scissors" && computerChoice == "Paper" -> "You win!"

            else -> "You lose!"
        }


        resultTextView.text = result
    }


}

private fun ImageView.setImageResource(computerChoice: String) {

}

private fun getImageResource(choice: String): Int {
    return when (choice) {
        "Rock" -> R.drawable.rock
        "Paper" -> R.drawable.paper
        "Scissors" -> R.drawable.scissors
        else -> throw IllegalArgumentException("Invalid choice")
    }
}


<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    tools:context=".MainActivity">


    <ImageView
        android:id="@+id/computerChoiceImageView"
        android:layout_width="150dp"
        android:layout_height="120dp"
        android:layout_marginEnd="16dp" />

    <TextView
        android:id="@+id/resultTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Choose your move!"
        android:textSize="24sp"
        android:textStyle="bold"
        android:layout_marginBottom="16dp"/>

    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center">

        <ImageView
            android:id="@+id/rockImageView"
            android:layout_width="100dp"
            android:layout_height="100dp"
            android:src="@drawable/rock"
            android:layout_marginEnd="16dp"
            android:onClick="onRockClicked"/>

        <ImageView
            android:id="@+id/paperImageView"
            android:layout_width="100dp"
            android:layout_height="100dp"
            android:src="@drawable/paper"
            android:layout_marginEnd="16dp"
            android:onClick="onPaperClicked"/>

        <ImageView
            android:id="@+id/scissorsImageView"
            android:layout_width="100dp"
            android:layout_height="100dp"
            android:src="@drawable/scissors"
            android:onClick="onScissorsClicked"/>
    </LinearLayout>

</LinearLayout>
