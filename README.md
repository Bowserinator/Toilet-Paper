4. # How to patch ~~all~~ some of the stupid Paper bugfixes

    ## Introduction

    PaperMC is a popular Minecraft server that offers optimizations and plugin support. They also fix bugs they deem "exploits" before vanilla does, often without giving an option to disable this patch. As such, vanilla parity is severely broken (note: Spigot and Bukkit already beeak vanilla parity). There's a reason all the technical Minecrafters are using fabric and lithium instead.

    But what if you want a fun world with some friends, and want the plugins & performance optimizations Paper offers, but without all the parity breaking? After all, whether you want to slice portals with update suppression to make OP farms (patched by Spigot), do RNG manipulation to get enchants, or make sand dupers to cover your perimeter floors in glass, are all up to you. The Paper devs however, will tell you to "/give" yourself the enchanted books and sand instead, because apparently there are right ways to play a sandbox game.

    Well they tell us to go fork the project since it's OSS so here it is.

    ## Stuff unpatched (so far):
    - Player seed based RNG Manipulation
        + `Use-a-Shared-Random-for-Entities`
        + Note: Entities still used a shared RNG, but players do not
    - Colored signs with color escape codes
        + `Fix-exploit-that-allowed-colored-signs-to-be-created`
        + Note: doesn't work in latest version of vanilla anyways
    - Villager demand can go negative again
        + `Fix-villager-trading-demand-MC-163962`
        + Villager prices won't go up faster than vanilla
    - Moving arrows no longer despawn
        + `Fix-arrows-never-despawning-MC-125757`
        + Breaks "arrow" fountains, TNT railguns and TNT looting
    - Falling sand can't be a command block
        + Forgot the patch but it's in Fallingsand
        + Pointless in creative because people can summon them / open their saved hotbars anyways
    - Void trading with villagers (doesn't work, need moar fix)
        + `Ensure-safe-gateway-teleport`
        + `Fix-merchant-inventory-not-closing-on-entity-removal`
    - Sand duping (doesn't work yet, need moar fix)
        - `Fix-sand-duping`
        - `Fix-dangerous-end-portal-logic`
## Steps:

1. Clone the repo: `git clone https://github.com/PaperMC/Paper`

2. Extract `src.zip` into `/Paper-Server`
   
    Note: it's more recommended you apply the patches yourself. All the code changes can be found in `patches.patch`
    
3. Run the following commands:

    ```
    cd Paper-Server
    git add .
    git commit -m "Unpatch paper"
    cd ../
    gradlew rebuildPatches
    gradlew createReobfBundlerJar
    ```

Verify the changes with `git diff` or viewing the generated patches file in `patches/server/[the last patch]`
    

4. Patched paper jar is in `build/libs/whatever paper version.jar`