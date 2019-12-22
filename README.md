# eco-game-notes
Documentation of the changes i made to the default eco game to make it more enjoyable.

### Plant Growth
Plants in eco can take multiple real-life days until they're fully grown. (Smaller plants like Beans are fully grown after 19 hours, but large trees can take up to 6 days until they're fully grown)

I divided the plant growth time by 10, so every plant is done in less than 1 real-life day.
This can be accomplished easily by going to your eco installation folder and from there into `Eco_Data/Server/Mods/AutoGen/Plant`.  
Each file in this folder is a plant available in eco.  
Search for the line `this.MaturityAgeDays = x.xf;` - `MaturityAgeDays` is the variable that defines how many real-life days a plant needs to be fully grown (`1.0f` = 24 hours, `0.5f` = 12 hours, etc...)  
I just divided each of these values by 10, e.g. for `Beans`: `this.MaturityAgeDays = 0.8f / 10.0f;`.  

To speed up this process i used Notepad++'s `Search and replace in files...` function
- with `(this.MaturityAgeDays.*)(;)` as search regex
- and `\1 / 10.0f\2` as replace

### Mining Skill
When you reach Mining Level 6 you can choose between 2 Talents:
- `SweepingHands`: Picking up rocks also attempts to pick up similar rocks in an area
- `LuckyBreak`: Mining rocks no longer has a chance to create large chunks

However i felt the game would be far more enjoyable if one could get both perks at once (no more large rock pieces + auto pickup).  
This can be easily accomplished by editing the 2 skill files:
- `Eco_Data\Server\Mods\AutoGen\Benefit\LuckyBreak.cs`
- `Eco_Data\Server\Mods\AutoGen\Benefit\SweepingHands.cs`

Both initialize the set of talents you will get in the `TalentGroup`, e.g. for `SweepingHands.cs`:
```c#
Talents = new Type[] {
  typeof(MiningSweepingHandsTalent),
};
```

Simply replace this section in both files with
```c#
Talents = new Type[] {
  typeof(MiningSweepingHandsTalent),
  typeof(MiningLuckyBreakTalent),
};
```

Now you'll get both perks regardless of which one you pick :)

### External Mods
Additionally i can recommend the following mods:

- [Industrial Elevator](https://eco-mods.com/resources/vanilla-industrial-elevator-mod.154/)
  An Elevator that is large enough to transport a vehicle up and down - a good replacement for ramps thats available in midgame.
- [JD Garbage Man](https://eco-mods.com/resources/jd-garbageman-job.75/)
  Adds the ability to recycle some materials, including tailings which helps in keeping pollution down.  
  This mod is a bit game-breaking, because it removes the challange of having to deal with tailings - i would only recommend it for single-player playthroughs.  
  *NOTE:* The perks don't work for the skills, i would recommend not getting the skills this mod provides.
- [Big Shovel](https://eco-mods.com/resources/big-shovel-asphalt-mdk.34/)
  Adds new shovels that allow you to pick up 10 pieces of dirt instead of just one.  
- [JD Storage Chest](https://eco-mods.com/resources/jd_storagechest.73/)
  Adds new storage chests that can also store blocks.  
  The recipe involving iron is broken, it also just gives the wood version of the chest.
