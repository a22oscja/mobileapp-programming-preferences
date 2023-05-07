
# Rapport

To start out a basic layout was created. This included a textView as well as a button.

A second activity was created and made to be openable upon the button in the
original activity being pressed using the following code in the onCreate method:

```
    Button button = findViewById(R.id.button);
    button.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            Intent intent = new Intent(MainActivity.this, SecondActivity.class);
            startActivity(intent);
        }
    });
```
Here an onClickListener is added to the button creating an intent and starting the new activity.

The second activity includes an EditText field in the layout. The onPause method is used to
add the text in this field to shared preferences.

```
    protected void onPause() {
        super.onPause();
        EditText text = findViewById(R.id.text);
        SharedPreferences sharedPref = getSharedPreferences("sharedPref",MODE_PRIVATE);
        SharedPreferences.Editor editor = sharedPref.edit();
        editor.putString("text",text.getText().toString());
        editor.apply();
    }
```
The text field is identified by its id, then a shared preference editor adds its text into
shared preferences and applies.

In the MainActivity these shared preferences are read in onResume as we do not need the text to
display upon opening the app.
```
    protected void onResume() {
        super.onResume();
        TextView textView = findViewById(R.id.textView);
        SharedPreferences sharedPref = getSharedPreferences("sharedPref",MODE_PRIVATE);
        String text = sharedPref.getString("text","");
        textView.setText(text);
    }
```
Here the shared prefences is extracted and then applied to the activities own textView.

The following sequence is an example of how this all looks together:

![Screenshot 1](Screenshot_1.png)

This is the basic app upon being opened.

![Screenshot 2](Screenshot_2.png)

This is the second activity with having "Shared preferences" written in the EditText field.

![Screenshot 3](Screenshot_3.png)

Finally, if the back button is pressed, you are brought back to the original activity
with the text having been written out.
