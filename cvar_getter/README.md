# Console variable getter script
It is not normally possible to get ConVars with VScripts in CS:GO as there are no functions for it available.
This method uses a very roundabout way to make it possible to do so.

WARNING: This script creates a file each time you acquire a convar in the cfg directory, it might get messy quickly! It is safe to delete them. (can't do it within game unfortunately)

### Setup
Compile the vmf file and merge the scripts directory relative to your csgo gamedir.

### Usage
To Acquire a ConVar (need to be done before to be able to get it's value)
<br/>
<code>
::AcquireCvar(convar)
</code><br/>
where 'convar' is the convar name as a string.

After Acquiring the ConVar you can get its value with:
<br/>
<code>
::GetConVar(convar)
</code>

### Example
Test it out by running the following in console:
<br/>
```
script ::AcquireCvar("mp_warmuptime")
script printl(::GetConVar("mp_warmuptime"))
```

### Caveats
<ul>
<li>There needs to be a delay between acquiring a convar and actually getting the value. It's not really possible to overcome it with this method. If you actually want to do it you need to delay the <code>::GetConVar()</code> part after using <code>::AcquireCvar</code></li>

<li>Some stuff will get sent to chat to obtain the values. I haven't found a better method yet that wouldn't require sv_cheats.</li>

<li>A file is created each time a convar is acquired as mentionted earlier</li>
</ul>

### How it works
This method uses the fact that typing out the convar name without any values will print out the value of it to the console.
The way this method works is that the command is sent to the console which will print out the values with other gibberish, it's also prepended with 'say_team ' and logged to a file that will sit in cfg directory.
That file then gets executed which will make the player say the guts of what has been printed, and that can be interpreted by a event listener that can parse the string and get out the actual value.
  
 
