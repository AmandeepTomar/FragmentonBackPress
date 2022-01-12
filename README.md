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

References 

- https://betterprogramming.pub/a-new-way-to-handle-back-press-in-fragments-8a67cdcda75e
- https://developer.android.com/reference/androidx/activity/OnBackPressedDispatcher
- https://stackoverflow.com/questions/57512327/navigation-component-illegalstateexception-fragment-not-associated-with-a-fragm/63330087#63330087
