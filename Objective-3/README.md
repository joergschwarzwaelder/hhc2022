

# Objective 3: Windows Event Logs
**Location: Tolkien Ring**  
**Elf: Dusty Giftwrapy**

This objective is about getting familiar with the analysis of Windows event logs. There are provided for download: https://storage.googleapis.com/hhc22_player_assets/powershell.evtx

In order to complete this objective, the event log file was exported to an XML file for easier handling:

> apt-get install libevtx-utils
> evtxexport powershell.evtx >
> powershell.xml

1. What month/day/year did the attack take place? For example, 09/05/2021.

**12/24/2022**
 
2. The contents of a file were retrieved by the attacker and stored to a variable. Submit the full powershell line that performed this action.

This activity can be found in this action:

```$foo = Get-Content .\Recipe| % {$_ -replace 'honey', 'fish oil'} $foo | Add-Content -Path 'recipe_updated.txt'```

3. The contents of the previous file were retrieved, changed, and stored to a variable by the attacker. Submit the full PowerShell line that performed only these actions.

```$foo = Get-Content .\Recipe| % {$_ -replace 'honey', 'fish oil'} $foo | Add-Content -Path 'recipe_updated.txt'```

  

4. After storing the altered file contents into the variable, the attacker used it to run a separate command that wrote the modified data to a file. Submit the full Powershell line that performed only this action.

  

```$foo | Add-Content -Path 'Recipe.txt'```

  

5. What is the new file’s name that was created with the previous command?

```Recipe.txt```

  

6. Were any files deleted (Yes/No)?

**Yes**

  

7. Was the original file deleted (Yes/No)?

**Yes**

  

8. What is the Event ID of the log that shows the actual command line used to delete the file?

**4104**

  

9. Is the secret ingredient compromised (Yes/No)?

**Yes**

  

10. What is the secret ingredient?

**honey**

**Achievement: Windows Event Logs**
