# ICT4D2021-RadioMaliVoterVoiceXML

<img src="logo.jpg" width=64/>

This is the VoiceXML files for organizing the voting system, by ICT4D 2021's group three.

This repository intends to provide a clean version, ready to be forked, set up, and used with the [Voxeo platform](http://evolution.voxeo.com).

There are 7 files with following purposes:

| File(s)      | Purpose |
|--------------|:--------|
| language.xml | The entry point for the app that allows radio host to create new polls and retrieve the vote count of the last conducted one. Contain a menu for choosing the language and redirecting to the menu with the chosen language. |
| *_menu.xml   | Menu files only differ in the language (English or French). Contain all functionality for creating a new poll and retrieving the vote count of the last conducted one.|
| Vote.xml     | Contain functionality for registering votes (beeps) |
| *.wav        | Audio files are used during asking to choose or change the language|

All created in Voxeo applications have the following parameters:
- 'Voice phone calls' form of communication
- 'Development' deployment
- 'Europe' region
- 'VoiceXML' app type
- 'Nuance' ASR/TTS
- 'EU - Prophecy VoiceXML' platform


## Installation
Instructions reproduce the state of the prototype infrastructure.

***Preconditions:***

You have an accessible database with proper structure (report, section 13) and created a server with backend functionality as in [RadioMaliVoterBackend](https://github.com/Michelindoll/ICT4D2021-RadioMaliVoterBackend). Now you want to add the voice operable part of the system.

***Actions:***
1. Make a copy of this repository
2. Add the link to your server in the following files:
      1. Vote.xml, line 13
      2. EN_menu.xml, line 13
      3. FR_menu.xml, line 14
3. Create an application in Voxeo for managing polls and retrieving vote counts (use the parameters mentioned above)
4. Add to the storage of this application files: language.xml, EN_menu.xml, FR_menu, FR.wav, changeLang3_EN.wav, changeLang3_FR.wav; specify language.xml as Voice URL (entry point)
5. If not done yet, add a new radio station to the database: insert `Name` and `Code` in the RadioStation table (Id will be assigned automatically, DefaultYes and DefaultNo fields are filling later)
6. Create two apps in Voxeo for voting/beeping (use the parameters mentioned above)
7. Add to each of them the Vote.xml file and specify it as Voice URL (entry point)
8. Fill in the following fields in the database:
      1. insert applications pin as `Number` in the `PhoneNumber` table (`Id` will be assigned automatically, fields `Answer` and `Poll` are optional)
      2. add `PhoneNumber.Id`(s) of inserted numbers to `DefaultYes` and `DefaultNo` fields of the new radio station in the `RadioStation` table
9. Now, when you call the application pin for managing polls pin you can create polls for your new radio station or retrieve the count for the last conducted poll. When you call the chosen poll option (application pin) your vote will appear in the Vote table 

If you have a running system in place that was implemented as described before and need to connect a new radio station to the system, you need to insert `Name` and `Code` for the new radio station in the RadioStation table and repeat steps 6-8.

## See also
- [RadioMaliVoterBackend](https://github.com/Michelindoll/ICT4D2021-RadioMaliVoterBackend)
- [RadioMaliVoterBot](https://github.com/Plastikpizza/ICT4D2021-RadioMaliVoterBot)