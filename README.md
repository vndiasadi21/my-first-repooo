package com.example.notepad

import android.content.Context
import android.os.Bundle
import android.widget.*
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    private lateinit var noteInput: EditText
    private lateinit var saveButton: Button
    private lateinit var noteList: ListView
    private lateinit var adapter: ArrayAdapter<String>
    private val notes = mutableListOf<String>()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        noteInput = findViewById(R.id.noteInput)
        saveButton = findViewById(R.id.saveButton)
        noteList = findViewById(R.id.noteList)

        loadNotes()

        adapter = ArrayAdapter(this, android.R.layout.simple_list_item_1, notes)
        noteList.adapter = adapter

        saveButton.setOnClickListener {
            val note = noteInput.text.toString()
            if (note.isNotEmpty()) {
                notes.add(note)
                adapter.notifyDataSetChanged()
                noteInput.text.clear()
                saveNotes()
            } else {
                Toast.makeText(this
