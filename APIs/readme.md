 - = Overall Goals = -
 
This projects goal is to build a database structure to support API responses that are captured from a video game and store them for later analysis and to build better tools to view the data that is coming from the game. To do this we will need to build a set of database tables that can acomplish a number of tasks. The goal of the project will be to store all the information in the database in the most efficient way possible to prevent duplicates. Data from replays are static and once stored will not be changed anymore. Player tables will change whenever new updated information is received from a player.

1. Record all battles/replays in a way that all battles can be queried and viewed.
2. Extract a players Hero, Titans, and Pet stats from replays and using a seperate set of tables keep an updated record of the current stats of each. The only historical data that will be kept of players is name and clanid.
3. Keep a recreatable record of Guild War and Asguard battles. All data from the Guild War and Asguard JSON should be stored in a way the JSON file can be exported from the database.



- = Section 1 (Files prefixed with '1-') = -
 
These JSON files represent server responses sent from the client to the web server. We need to extract the battles/replay sections of these files and store them in the replay section of the database. Everything else in this file is not needed.


- = Section 2 (Files prefixed with '2-') = -
 
These files need to be able to be recreated in its entirety. Player and replay information needs to be extracted and the JSON file will need to be able to be exported if needed.


- = Section 4 (Files prefixed with '4-') = -
 
These files are lootbox type responses that contain the rewards gained from various sources.

 - = General notes = -
 
1. JSON nodes that essentially show result, response, true, true,  true, etc are not needed. They can be ignored.

- = File Instruction Breakdown = -
 
1-Arena: The only thing needed from this file is Results.result.response.battles. There should only ever be 1 battle from this specific JSON file and each of them should be placed in the replay tables. Player information should be read and updated if needed from this file.


1-Grand-Arena: The only thing needed from this file is results.result.response.battles. This file will contain between 2 and 3 battles and each of them should be placed in the replay tables. Player information should be read and updated if needed from this file. The rest of the information can be disguarded.


1-Guild-Battle_Heroes: The only thing needed from this file is results.result.reponse.replay. There should only ever be 1 battle from this specific JSON file and each of them should be placed in the replay tables. Player information should be read and updated if needed from this file.


1-Guild-Battle_Titans: The only thing needed from this file is results.result.reponse.replay. There should only ever be 1 battle from this specific JSON file and each of them should be placed in the replay tables. Player information should be read and updated if needed from this file.


1-Private-Battle_Heroes: The only thing needed from this file is results.result.reponse.replay. There should only ever be 1 battle from this specific JSON file and each of them should be placed in the replay tables. Player information should be read and updated if needed from this file.


1-Private-Battle_Titans: The only thing needed from this file is results.result.reponse.replay. There should only ever be 1 battle from this specific JSON file and each of them should be placed in the replay tables. Player information should be read and updated if needed from this file.


2-Guild-War: This file will contain up to 80 replays each of which need to be documented to the replays tabs, but all information from the JSON file needs to be stored as on occassion we will need to recreate the JSON file and export it for use in other projects.


3-Asgaurd: This file will contain multiple sections, the only one of value is the last node that contains result.response.<PlayerID>.<battleID>. Each battle ID contains a replay and there can be up to 150 battles per reponse.


4-Lootbox: This file is from a lootbox opened from the players inventory. The child nodes of the results.result.response node need to be captured.


4-TowerChest: This file contains the reward from opening a chest in the tower. The child nodes of the results.result.response.reward node need to be captured.


4-PetSummoning: This file contains the reward(s) opening 10 pet eggs. The child nodes of the Results.result.reponse.rewards node need to be captured. It It seems like petCard can be safely ignored.


4-OutlandChest: This file contains the reward from opening a chest in the outlands. The child nodes of the results.result.response.rewards.free/payed node need to be captured.


4-HeroicChest: This file contains the reward from opening the heroic chest in town center. The child nodes of the results.result.response.rewards node need to be captured.


4-Expedition: This file contains the reward from completing expeditions. The child nodes of the results.result.response.reward.consumable should be collected.


4-CampaignRaid: This file contains the reward for raiding campaign missions. The child nodes of the results.result.response.raid.consumable should be collected.


4-Campaign: This file contains the reward for completing campaign missions. The child nodes of the results.result.response.reward should be collected.


4-ArtifactChest: This file contains the reward for opening artifact chest. The child nodes of the results.response.chestreward should be collected. Starmoneyspent should be updated on the player database.


4-adventure: The file contains the reward for collecting adventure chests. The child nodes of the results.result.response.consumable should be collected.


Last but not least: I have started this project a bit mapping out the DB structure using google sheets: https://docs.google.com/spreadsheets/d/1vzyao_mv3btmf62qnCPX6pnGF5o4gvOO838UVXLgbWs/edit?usp=sharing
