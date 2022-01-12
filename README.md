# FragmentonBackPress Demo

If you’ve been an Android developer, you have handled back-press events using the ```onBackPressed()``` function in activities.
That was fine until the introduction of architectural components and a single source of truth patterns. Now we have ```onBackPressedDispatcher``` so use this in fragments and we can handle
the back-press for fragments with in the fragments.

In this Repo we have achieved the same using ```onBackPressedDispatcher``` and ```OnBackPressedCallback```. 

We just need to add the block of code in your fragments and rest will be done. 

``` 
    requireActivity().onBackPressedDispatcher.addCallback(this,object : OnBackPressedCallback(true){
            override fun handleOnBackPressed() {
                if(you have any specific conditions){
                // handle back-press in fragments
                }else{
                  isEnabled = false. // this will disable the onBackPressedDispatcher callback
                  activity?.onBackPressed() // called activity onBackPressed()
                }
            }
        })
        
```        

Unregistered the ```onBackPressedDispatcher``` in fragments ```onDestroyView()```

```
override fun onDestroyView() {
    super.onDestroyView()
    //unregister listener here
    onBackPressedCallback.isEnabled = false
    onBackPressedCallback.remove()
}
```

I am facing issues , when i tried to implement the same in my ongoing project and its not received call in ```handleOnBackPressed()``` or ```OnBackPressedCallback()``` is not called so i have gone through project code and struture after checking codes, foung that ```onBackPressed()``` in Activity must not be do some stuff related to fragment.

- As i have written some code in my Activit's ```onBackPressed()``` posted below. 
- ``` 
        @Override
    public void onBackPressed() {
        Log.e("Here We are","in BlinkIDScanBaseActivity");
        Intent intent = new Intent();
        setResult(RESULT_CANCELED, intent);
        finish();
    }
    ```
- just commented the code and all works fine , Its my observation , will read about it and post here.    

- Same happen another Activity. 

- Finally fixed my proble after removing the code from Activity's ```onBackPressed()``` 
    
    

References 

- https://betterprogramming.pub/a-new-way-to-handle-back-press-in-fragments-8a67cdcda75e
- https://developer.android.com/reference/androidx/activity/OnBackPressedDispatcher
- https://stackoverflow.com/questions/57512327/navigation-component-illegalstateexception-fragment-not-associated-with-a-fragm/63330087#63330087
