<h1 align="center">
  <img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/af6ea950-8b1b-48ac-b19b-303fc8fd5737" width="50%" height="50%">
</h1>
For well over a decade, World of Warcraft has sustained my excitement over thousands of hours of collecting mounts, progressing in raids, making friends, and mastering professions. In this project, I will walk through my throught process behind designing and implementing new rewards systems for Azeroth and beyond. 

## Brainstorming

We will first explore areas of the game in which rewards can be introduced, catering to various types of players. Some of these ideas will be fleshed out more than others and include implementation plans informed by statistical modeling.

Yee (2006) proposed that there are three main types of gamers, each with various subtypes: _achievement_ (advancement, mechanics, competition), _social_ (socializing, relationship, teamwork) and _immersion_ (discovery, roleplaying, customization, escapism). While players often fall into multiple groups, I found brainstorming rewards to enhance these different player groups to be an interesting starting point. 
- An alternative, more-optimal starting point would be data-driven. _Where are players spending the most time, and how does retention compare for players who prefer pet battles versus raiding versus professions? How do these statistics compare to previous expansions/systems?_

I first considered new rewards that would incentivize gameplay that the social gamers would enjoy. PvE and PvP excel in this department, more often than not requiring teamwork to succeed in mythics, battlegrounds, and arenas, to name a few. Professions, while often a peaceful solo activity, show much potential for additional rewarding of social interaction. The introduction of the Crafting Order system in Dragonflight promoted more interaction between "professionals" and their customers, in contrast to the sole use of the Auction House. I will thus focus on developing rewards that will incentivize use of the Crafting Order system, which I hypothesize will positively impact players that enjoy social interaction and immersion through roleplaying. 

## Crafting Order Reward Systems

Professionals who complete Crafting Orders are rewarded with gold and, less often, profession levels. Thus, the reward for Crafting Orders is the same as that for using the Auction House in a majority of cases. Additionally, the cadence/schedule for the current Crafting Order reward is short-term in that the main reward (gold) is awarded once per Crafting Order. It might be meaningful to include additional rewards earned over a longer period of time, granting a sense of satisfaction similar to that from long-term career development. Such potential new reward systems could include...

* **New Currency: Artisan Tokens**

  - Overview
    - Introduce a new currency, Artisan Tokens, awarded for completing crafting orders. Artisan Tokens can be exhanged for profession-specific cosmetic items (e.g., transmogs, toys, pets, mounts) at each profession's Artisan Token vendor located near each respective profession station in the capital city.
      - Cosmetics for each profession improve immersion through roleplay and customization, as they better reflect the player's identity as a distinguished member of their profession. Bind-on-pickup (BoP) cosmetics also seem relatively simple to implement with respect to (a lack of) economic impacts, etc.
  - Rate of Reward
    - _Do we encourage players to do Crafting Orders for hours by granting the currency for each order? Do we instead motivate diversity in play by granting the currency for only the first X orders each day? Does the former turn the currency into an unenjoyable grind to get any rewards? Does the latter turn the currency into a daily to-do that players end up dreading?_
      - Limiting the number of token-awarding Crafting Orders per day allows a more fair opportunity to earn tokens for professions that struggle to obtain as many orders as other professions. As such, I will choose to grant Artisan Tokens for the first 4 orders each day to match the current limit of 4 public Crafting Orders per day. Data on the current distribution of Crafting Orders might be more informative for determining this value, but 4 seems reasonable.
  - Amount of Reward
    - More impressive Crafting Orders (e.g., higher ilvl gear) should be rewarded with more Artisan tokens as an extra Reward of Glory that praises the player for their exceptional work. I select a somewhat arbitrary but reasonable range of 8-20 Artisan tokens per Crafting Order and determine the cosmetic prices using this range.
  - Balancing Token Acquisition Across Professions
    - An obvious flaw in this currency is that some professions use Crafting Orders far less than the the professions (e.g. Alchemy), and some not at all (e.g. Herbalism). Two potential solutions arise to including these professions in gaining Artisan tokens via social interactions:
      1) Collaborative Harvesting: Resource nodes harvested by multiple people in a group at the same time awards Artisan Tokens, thus motivating guild/friend harvesting runs.
      2) Collaborative Projects: Low-demand Crafting Order professions like Alchemy can assist/"collaborate" with Crafting Orders from high-demand professions, such as a piece of gear. Such collaboration is inspiring, boosting the Crafting Order's inspiration and thus probability of increasing in quality. Both collaborators are granted additional Artisan Tokens (a "Collaborative Bonus").
        - System incentivizes customer by higher chance of better item, and the collaborators with extra Artisan Tokens and a higher chance of receiving a larger tip (players often tip more gold for higher quality crafts).

  - **Artisan Token Cosmetic Store**
  
    - Here, I will design several cosmetic items for sale in the Artisan Token store; namely, two toys, a pet, a cosmetic armor set, and a mount for the Alchemy profession. I will then carry out statistical modeling to inform the price of the items based on the effort deemed need to obtain the item.

    * Toys
      1. Potion of... Which One Was This Again?
        - Description: Upon use, the player changes in appearance for 10 minutes, with one of the following changes selected at random: 1) grow in size, 2) shrink in size, 3) becomes a butterfly. The toy has an animation of the character drinking a potion and then the surprise of the effect.
        - Special Effect: During the effect, the pitch of the character's voice deepens (for growth option), heightens (shrink option), 
      
      2. Alchemy Table
        - Description: A table equipped with an array of herb-filled bowls next to colorful vials and flasks connected via tubes. The player puts on an exciting performance for all viewers. After the performance is complete, one of the possible cosmetic potions is selected at random. 
        - Performance: The bunsen burner is turned on below the now-smoking central cauldron. The player juggles the bowls of herbs before pouring them into the main cauldron, each releasing an effect. The performance could depend on the type of cosmetic potion selected at random (i.e. a love potion, with ingredients that release hearts, red mist, etc.).

    * Pet
      1. Bubbling Cauldron
        - Description: A small cauldron containing a bubbling liquid that releases smoke or another "magical" effects. Two legs made of the liquid sprout through two forcefully made holes near the bottom of the cauldron.
        - Special Abilities: Occasionally brews a small potion that grants a minor buff to the player when consumed. Alternatively, the liquid could change every few minutes, with each liquid having a different effect.

    * Armor Set
      1. **Master Alchemist’s Regalia**
        - **Head**: **Alembic Visor** - A helmet with a glass dome filled with swirling fluid with a shiny mist.
        - **Shoulders**: **Catalyst Epaulets** - Shoulder pads with arcing glass tubes filled with bubbling fluid matching the headpiece.
        - **Chest**: **Transmuter’s Robe** - A robe with intricate patterns that glow faintly, with pockets filled with potions.
        - **Gloves**: **Corrosion-Resistant Gauntlets** - Gloves with embedded tubes containing colorful liquids, similar to the Epaulets.
        - **Belt**: **Elixir Sash** - A belt adorned with various flasks and pouches, each emitting a faint glow.
        - **Leggings**: **Reactive Barrier Leggings** 
        - **Boots**: **Sealed Boots**
            
     * Mount
      1. **Elixir-Infused Drake**
        - **Description**: A majestic drake with scales that shimmer in various colors, as if made from liquid potions. Its wings leave a trail of colorful mist as it flies.
        - **Features**: 
          - **Special Animation**: The drake breathes out a cloud of multi-color alchemical fumes, each color emitting a unique effect (fireworks, fire, etc.)
          - **Alchemy Station**: While mounted, the player can access a portable alchemy station on the drake's back to craft potions on the go.
            - Would be powerful, first implementation of a portable profession station outside of engineering (to my knowledge?).

* **New Status Effect: Flow State**

  - Overview
    - Completing a crafting order grants a status effect, Flow State, that increases inspiration for the next crafting order.
      - An interesting alternative is to buff a random crafting stat, or the user's highest crafting stat in order to better distinguish the identity of the player's crafting build (meaning, the stat they are prioritizing).
  - Duration
    - I am split on two options for duration: 1) each crafting order grants a stack, with a duration of ~20 minutes, or 2) the first crafting order each day grants a stack, with a duration of 24 hours. The former motivates a single, continuing session of orders, whereas the latter motivates a daily "streak" style. In either case, the duration is short enough to motivate more crafting orders, but not too short as to bring source of stress and hasty rudeness to the next customer.
  - Stacking
    - Another consideration is whether the effect will stack; that is, if the player completes an order before the buff expires, the duration will be reset and the player will gain a stack. Stacks will contribute to additional inspiration gain and thus incentivize "keeping the ball rolling", i.e. sustained contribution to crafting, similar to real blacksmith, etc.
  - Amount and Functional Form
    - Without stacking, the buff would increase inspiration by either a flat amount, or a percentage of the user's current inspiration. The former would avoid forcing more player's into an inspiration-focused build. With stacking, A linear scaling of inspiration gain ($IG$) with the number of stacks is likely too extreme. Instead, a slower, logarithmic growth seems more appropriate: $$IG = C \ln(s + 1)$$ where constant $C$ rescales the amount of inspiration gained. Note: $s+1$ is used within the logarithm such that $IG(0) = 0$, meaning that no inspiration is gained without a stack.
    - To gauge a reasonable value for C, we recall that 10 more points of inspiration translates to a 1% increase in probability of crafting an item with higher base skill. To put this into recent context, the Elemental Lariat is a powerful neck item that Jewelcrafters create via Crafting Orders. The 418-ilvl version of the item is impossible to craft without an inspiration proc (the skill required to craft a 418-ilvl is below the maximum skill a player can have, even with ideal skill point allocation). A 3-8% buff in inspiration, equivalent to 3-8 more 418-ilvl Lariats for each 100 crafted, seems like a safe place to constrain the buff, while remaining enticing enough to be sought after. Using this 3% lower bound on the buff results in $C = 30 / \ln(2) = 43.3$, and the following inspiration gains as a function of stack number:
    
<h3 align="center"></h3>

<table>
  <tr>
    <td>
      <table>
        <tr>
          <th>Stacks (s)</th>
          <th>Inspiration Gain (IG)</th>
          <th>% Increase in IG from <br>Previous Stack Count</th>
        </tr>
        <tr>
          <td>1</td>
          <td>30</td>
          <td>-</td>
        </tr>
        <tr>
          <td>2</td>
          <td>47.6</td>
          <td>58.4%</td>
        </tr>
        <tr>
          <td>3</td>
          <td>60.0</td>
          <td>26.2%</td>
        </tr>
        <tr>
          <td>4</td>
          <td>69.7</td>
          <td>16.1%</td>
        </tr>
        <tr>
          <td>5</td>
          <td>77.6</td>
          <td>11.3%</td>
        </tr>
      </table>
    </td>
    <td>
      <img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/6b78957d-e10f-4f26-94a0-8d541837edd2">
    </td>
  </tr>
</table>
