# Projector2Assembler
Space Engineers script: queue all the components needed to build a blueprint on your assember.

Projector2Assembler by Juggernaut93

With some code by nihilus from here:
https://forum.keenswh.com/threads/adding-needed-projector-bp-components-to-assembler.7396730/#post-1287067721

## Setup
   - You obviously need a programming block, a projector, an assembler
   - Run the script with this argument: [ProjectorName];[AssemblerName];[lightArmor];[staggeringFactor];[fewFirst]
       - [] indicates it's an optional parameter
       - ProjectorName (default: Projector) is the name of the projector with the blueprint you want to build
       - AssemblerName (default: Assembler) is the name of the assembler that will produce the needed components
       - lightArmor is true (default) or false and tells the script to assume all the armor blocks listed by
           the projector are respectively Light Armor Blocks or Heavy Armor Blocks
       - staggeringFactor is a non-negative integer (10 by default) that tells the script how to stagger the
           production
       - fewFirst is true (default) or false and tells the script to queue the components in the assembler
           sorted by amount. If false, the order is undefined (currently it's alphabetical, but it's not
           guaranteed to stay the same in the future).

## How it works
   - The script gets from the projector the remaining blocks to build. Unfortunately, the projector is not
       precise about the type of armor blocks to build and only gives a generic "armor blocks". You can then
       specify if you want to assume all the blocks are light or heavy armor blocks, but keep in mind that
       the script will overproduce if you specify heavy blocks but not all your blocks are full cubes and/or
       you also have light blocks; it will (probably) underproduce if you specify light blocks but you have
       many heavy armor blocks.
   - The script then sorts the components needed to build such blocks (if you set fewFirst to true) by
       ascending amount and will divide the amount of components by staggeringFactor. It will then tell the
       assembler to produce the obtained amount of components staggeringFactor times.
   - EXAMPLE:
       - your blueprint requires 3000 steel plates, 1500 construction components and 300 metal grids
       - you run the script with fewFirst = true and staggeringFactor = 10
       - the script will tell the assembler to build 30 metal grids, 150 construction components and
         300 steel plates 10 times
       - This will ensure your welding process won't be blocked by the lack of a single component
         that might have ended up at the end of the queue, and you will get a nice proportion of each
         component without waiting too much
