# What is this?

  A macro for World of Warcraft Classic for all-in-one damage and healing, with mouseover and target priority, and downranking using a preferred toggle key.

# Wait, what? Why?

  I play a priest in World of Warcraft (WoW) Classic. Due to the nature of WoW's mechanics, there are times when I need to "downrank", or cast a spell with a lower resource cost than that of my best spells. Normally, this would mean I'd need to keep multiple copies, or "ranks", of the same spell on my screen just for this purpose, which would take up way too much space and clutter my game interface.

  This macro allows the user to downrank their larger-resource-cost spells with the same button, effectively replacing multiple buttons with a single button. It also allows them the option to use an additional, separate spell to deal damage when they don't need to heal, freeing up even more space.

  Finally, it also prioritizes the right spell based on whether your mouse is hovering over a friendly or enemy target, or even yourself.
  
  I made this macro because I had been unable to find anything like it in my searching. There are addons that can do some of the same functions, but they're either overly complicated to setup or don't have all the same features. This macro is easy to understand, and can be adapted not only for priests, but any of the other classes in the game.

## Breaking down the code
 
 1. 
        #showtooltip
  This controls what shows up in the spell description on your interface, even when we manipulate which spell will be cast later in the code. Without this, it will simply show the name of the macro. It's not entirely required, but it looks much nicer.
 
 2. 
          /cast
  This tells the macro what action to take. Every time you normally cast a spell in the game, it is effectively doing the command "/cast [spell name]". We're going to use that same method to build this macro.
 
 3. 
        [@mouseover,harm,nodead]
  It's important to note that we put this @mouseover command FIRST. This is the WoW macro equivalent of an "if" statement. In this case, we'll be telling the macro "If your mouse is over a target", in this case, another player or an enemy character, "then do X". In this case, we add a few more checks here to see if the target being moused over can be harmed (i.e. that they are an enemy player or non-player character (NPC)), and that they have at least 1 health point (i.e. that they are not dead).
 
 4. 
        [@target,harm,nodead]
  This is the WoW macro equivalent of an "else if" statement; in this case, if the mouse is not over an enemy target, it'll now check to see if you have clicked on an enemy player/NPC. If so, and using the same checks as before to see if they can be harmed and have at least 1 health point, it will perform the spell cast.
 
 5. 
        Smite(Rank 8);
  This is the spell to be cast by the previous two if-statements. This can be replaced by the player's chosen spell, with or without the "(Rank X)" part, which defaults to the highest rank. There must also be a ";" to separate the following statements, otherwise this will not work!
 
 6. 
        [@mouseover,help,nodead,mod:shift]
  Same as before, this is our if-statement to see if our mouse is over a target. There are two primary differences, however. First, "help", as you may have guessed, is the same as the "harm" check, but for whether a target being moused over can be healed (i.e. they are a friendly player or NPC). This means we can cast healing spells on them, so we want to make sure they have at least 1 health point with a "nodead" check. And finally, the second difference is the "mod". This tells the macro to do something if a button is being pressed. In this case, if we press "shift" while using this macro, it will allow us to perform a different spellcast than if we were not holding down "shift".

  Note: At the time of writing this, only "shift", "alt", and "control" can be used to mod a spellcast. They can be swapped out in the above statement.
 
 7. 
        [@target,help,nodead,mod:shift]
  Same as before: if the mouse is not over a friendly target, and they can be helped and have at least 1 health point, and you're pressing shift, do X
 
 8. 
        [@player,mod:shift]
  Another "else if" statement, but this allows the macro to self-cast only if you neither have a mouseover target, nor have a selected target. This is not needed in the "harm" section, since there's no reason to cast damaging spells on yourself (nor could you do that!) You are, however, always "friendly" to yourself.

 9. 
        Heal(rank 2);
  This is the spell cast by the previous three statements, but only if the user is holding the shift key. The spell name can also be replaced as needed with any friendly-cast spell, however you'll likely want to actually put the rank of the spell here. The ";" is again essential to separate the last statement!
 
 10. 
        [@mouseover,help,nodead]
  Same as before, if there's a mouseover friendly target with at least 1 health point. This is the default "friendly" action of the macro if the user is not pressing the key defined as "mod" earlier.
 
 11. 
        [@target,help, nodead]
  Same as before, if there's a selected friendly target with at least 1 health point. This is the default "friendly" action of the macro if the user is not pressing the key defined as "mod" earlier.
 
 12. 
        [@player]
  Same as before, self-cast this spell if you neither have a mouseover target, nor have a selected target. Remember: you are always "friendly" to yourself.
 
 13. 
        Heal(rank 4)
  The spell being cast by the previous three statements. This is the default friendly action of the macro if the user is not pressing the key defined as "mod" earlier.
