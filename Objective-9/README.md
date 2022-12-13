
# Objective 9: Open Boria Mine Door
**Location: Web Ring**  
**Elf: Hal Tandybuck**

This objective is about getting familiar with XXE attacks.
On each of the six individual locks you an supply input, a browser on the server's side renders an image of that, and this image is eventually displayed in the lock.
The target is to connect the equally colored connectors on each 
individual lock.

### Lock 1
A working solution is hidden in the web sources: ```@&@&&W&&W&&&&```

All the remaining locks were solved by providing SVG images to the input field.

### Lock 2
```
<svg width="210" height="170" xmlns="http://www.w3.org/2000/svg">
<line if="lock_2" stroke-width="5" x1="0" y1="72" x2="210" y2="158" stroke="#fff" fill="#ffffff" />
</svg>
```
### Lock 3
```
<svg width="210" height="170" xmlns="http://www.w3.org/2000/svg">
<line if="lock_3" stroke-width="5" x1="0" y1="98" x2="210" y2="19" stroke="#00f" fill="#0000ff" />
</svg>
```
### Lock 4
For lock 4 some input sanitization is performed. The first occurrence of `<`, `>`, `"`, and `'` is removed. To avoid being disturbed by that, these four characters are prefixed to the SVG.
```<>"'
<svg width="210" height="170" xmlns="http://www.w3.org/2000/svg">
<line if="lock_4" stroke-width="5" x1="0" y1="44" x2="210" y2="44" stroke="#fff" fill="#ffffff" />
<line if="lock_4" stroke-width="5" x1="0" y1="135" x2="210" y2="135" stroke="#00f" fill="#0000ff" />
</svg>
```

### Lock 5
In lock 5 the input sanitization was improved compared to lock 4. Now all occurrences of`<`, `>`, `"`, and `'` are removed as soon as the focus is removed from the input field ("blur").
To get this lock solved, the input field is prepared and submitted using Javascript from the browser console. As these six locks are located in individual iframes, the "pin5" context has to be selected upfront.
```
document.querySelector('input').value='<svg width="210" height="170" xmlns="http://www.w3.org/2000/svg"><line if="lock_5" stroke-width="5" x1="0" y1="138" x2="210" y2="40" stroke="#f00" fill="#ff0000" /><line if="lock_5" stroke-width="5" x1="40" y1="170" x2="210" y2="84" stroke="#00f" fill="#0000ff" /></svg>';
document.querySelector('form').submit();
```


### Lock 6
```
<svg width="210" height="170" xmlns="http://www.w3.org/2000/svg"><line if="lock_6" stroke-width="5" x1="0" y1="33" x2="210" y2="33" stroke="#0f0" fill="#00ff00" />
<line if="lock_6" stroke-width="5" x1="0" y1="74" x2="210" y2="110" stroke="#f00" fill="#ff0000" />
<line if="lock_6" stroke-width="5" x1="0" y1="115" x2="145" y2="170" stroke="#00f" fill="#0000ff" />
</svg>
```

This leads to getting all six locks unlocked:
![All six Boria locks unlocked](https://github.com/joergschwarzwaelder/hhc2022/blob/main/Objective-9/BoriaMineDoor.png)

**Achievement: Open Boria Mine Door**

**Achievement: Open Boria Mine Door BONUS**

