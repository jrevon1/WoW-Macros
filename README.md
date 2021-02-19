# What is this?

  A macro for World of Warcraft Classic for all-in-one damage and healing, with mouseover and target priority, and downranking using a preferred toggle key.

# Wait, what? Why?

  A macro is a way to bind more than one action to a single button in World of Warcraft (WoW). Blizzard uses the Lua coding language to interpret macros.

  Due to the nature of the game's mechanics, there are times when I, as a player, need to "downrank", or cast a spell with a lower resource cost than that of my best spells. Normally, this would mean I'd need to keep multiple copies, or "ranks", of the same spell on my screen just for this purpose, which would take up way too much space and clutter my game interface.

  Instead, I use a macro to allow me to toggle between larger- and smaller -resource-cost spells with the same button, effectively replacing multiple buttons with a single button. It also allows the option to use an additional, separate spell to deal damage to enemies when they don't need to heal, freeing up even more space.

  Finally, it also prioritizes the spell based on whether your mouse is hovering over a friendly or enemy target, or even yourself.
  
  I made this macro over the course of a few months because I had been unable to find anything like it. Despite World of Warcraft originally releasing nearly 16 years ago, there is a surprising lack of documentation for macros. I was able to cobble together enough information from various sources, forum posts, and wikis to develop this, and have laid out what I've learned all in one place at the [bottom](#breaking-down-the-code). While there are some addons that can do some of the same functions, personally I found they're either overly complicated to setup or too cumbersome for what I need. This macro is easy to understand, and can quickly be adapted not only for priests, but any of the other classes in the game.
  
## How to use
  Simply paste the code of the [All-In-One](https://github.com/jrevon1/WoW-Macros/blob/main/All-In-One.lua) macro into a new macro. Make sure not to create any erroneous spaces!
  
  You can manually highlight and re-type the spell names as needed, or you can directly import the specific name and rank by opening your spellbook, and shift-clicking the spell itself into the macro.

  Drag that new macro to your actionbar and enjoy!

## Breaking down the code

  This is a really detailed breakdown of the macro code, based on what I know about how WoW intreprets the Lua code for macros. I wasn't really able to find this information in one place, so it is cobbled together from what I could find. It's super detailed, and you don't need to read any of this unless you want to understand exactly how and why the code does what it does.
 
        #showtooltip
  This controls what shows up in the spell description on your interface, even when we manipulate which spell will be cast later in the code. Without this, it will simply show the name of the macro. It's not entirely required, but it looks much nicer. Plus it allows us to visibly double-check that we are casting different spells.
 
          /cast
  This tells the macro what action to take. Every time you normally cast a spell in the game, it is effectively doing the command "/cast [spell name]<spell rank>". We're going to use that same method to build this macro.
 
        [@mouseover,harm,nodead]
  It's important to note that we put this mouseover command FIRST. The reasoning for this priority will be clear later, but for now just know it needs to be the first one! 

  This is the WoW macro equivalent of an "if" statement. In this case, we'll be telling the macro "If your mouse is over a target", in this case, another player or an enemy character, "then do X". In this case, we add a few more checks here to see if the target being moused over can be harmed (i.e. that they are an enemy player or non-player character (NPC)), and that they have at least 1 health point (i.e. that they are not dead).
 
        [@target,harm,nodead]
  This is the WoW macro equivalent of an "else if" statement; in this case, if the mouse is not over an enemy target, it'll now check to see if you have clicked on an enemy player/NPC. If so, and using the same checks as before to see if they can be harmed and have at least 1 health point, it will perform the spell cast.
  
  Because this statement is second, the macro will first attempt to see if your mouse is over an enemy target. If not, it'll see if you've manually-clicked on a target and have them still targeted. If not, it won't cast the defined spell. However, if you have a manually-clicked target, and hover your mouse over another separate target, the spell will be prioritized to cast on the mouseover target.
 
        Smite(Rank 8);
  This is the spell to be cast by the previous two if-statements. This can be replaced by the player's chosen spell, with or without the "(Rank X)" part, which defaults to the highest rank. There must also be a ";" to separate the following statements, otherwise this will not work!
 
        [@mouseover,help,nodead,mod:shift]
  Same as before, this is our if-statement to see if our mouse is over a target. There are two primary differences, however. First, "help", as you may have guessed, is the same as the "harm" check, but for whether a target being moused over can be healed (i.e. they are a friendly player or NPC). This means we can cast healing spells on them, so we want to make sure they have at least 1 health point with a "nodead" check. And finally, the second difference is the "mod". This tells the macro to do something if a button is being pressed. In this case, if we press "shift" while using this macro, it will allow us to perform a different spellcast than if we were not holding down "shift".

  Note: Only "shift", "alt", and "control" can be used to mod a spellcast. They can be swapped out in the above statement, but please note to use "control" rather than "ctrl".
 

        [@target,help,nodead,mod:shift]
  Same as before: if the mouse is not over a friendly target, and they can be helped and have at least 1 health point, and you're pressing shift, do X
 
        [@player,mod:shift]
  Another "else if" statement, but this allows the macro to self-cast only if you neither have a mouseover target, nor have a selected target. This is not needed in the "harm" section, since there's no reason to cast damaging spells on yourself (nor could you do that!) You are, however, always "friendly" to yourself.
  
  Now that we have a third order of events, when casting a friendly spell, the macro will prioritize in this order:
    1. Mouseover target
    2. Manually-clicked target
    3. Yourself

        Heal(rank 2);
  This is the friendly spell cast by the previous three statements, but only if the user is holding the shift key. The spell name can also be replaced as needed with any friendly-cast spell, however you'll likely want to actually put the rank of the spell here. The ";" is again essential to separate the last statement!
 
        [@mouseover,help,nodead]
  Same as before, if there's a mouseover friendly target with at least 1 health point. This is the default "friendly" action of the macro if the user is not pressing the key defined as "mod" earlier.
 
        [@target,help, nodead]
  Same as before, if there's a selected friendly target with at least 1 health point. This is the default "friendly" action of the macro if the user is not pressing the key defined as "mod" earlier.
 
        [@player]
  Same as before, self-cast this spell if you neither have a mouseover target, nor have a selected target. Remember: you are always "friendly" to yourself.
 
        Heal(rank 4)
  The friendly spell being cast by the previous three statements. This is the default friendly action of the macro if the user is not pressing the key defined as "mod" earlier.
