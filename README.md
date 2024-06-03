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

Professionals who complete Crafting Orders are rewarded with gold and, less often, profession levels. Thus, the reward for Crafting Orders is the same as that for using the Auction House in a majority of cases. Potential new reward systems could include...

* **New Currency: Artisan Tokens**
  - Overview: Introduce a new currency, Artisan Tokens, awarded for completing crafting orders. Artisan Tokens can be exhanged for profession-specific cosmetic items (e.g., transmogs, toys, pets, mounts) at a vendor near their profession's station in the capital city.
    - Cosmetics for each profession improve immersion through roleplay and customization, as they better reflect the player's identity as a distinguished member of their profession. Bind-on-pickup (BoP) cosmetics also seem relatively simple to implement with respect to (a lack of) economic impacts, etc.
  - Amount per Order: 
 
* **New Status Effect: Flow State**
  - Overview: Completing a crafting order grants a status effect, Flow State, that increases inspiration for the next crafting order.
    - An interesting alternative is to buff a random crafting stat, or the user's highest crafting stat in order to better distinguish the identity of the player's crafting build (meaning, the stat they are prioritizing).
  - Duration: I am split on two options for duration: 1) each crafting order grants a stack, with a duration of ~20 minutes, or 2) the first crafting order each day grants a stack, with a duration of 24 hours. The former motivates a single, continuing session of orders, whereas the latter motivates a daily "streak" style. In either case, the duration is short enough to motivate more crafting orders, but not too short as to bring source of stress and hasty rudeness to the next customer.
  - Stacking: Another consideration is whether the effect will stack; that is, if the player completes an order before the buff expires, the duration will be reset and the player will gain a stack. Stacks will contribute to additional inspiration gain and thus incentivize "keeping the ball rolling", i.e. sustained contribution to crafting, similar to real blacksmith, etc.
  - Amount and Functional Form: Without stacking, the buff would increase inspiration by either a flat amount, or a percentage of the user's current inspiration. The former would avoid forcing more player's into an inspiration-focused build. With stacking, A linear scaling of inspiration gain ($IG$) with the number of stacks is likely too extreme. Instead, a slower, logarithmic growth seems more appropriate: $$IG = C \ln(s + 1)$$ where constant $C$ rescales the amount of inspiration gained. Note: $s+1$ is used within the logarithm such that $IG(0) = 0$, meaning that no inspiration is gained without a stack.
    - To gauge a reasonable value for C, we recall that 10 more points of inspiration translates to a 1% increase in probability of crafting an item with higher base skill. To put this into relevant context, the Elemental Lariat is a powerful neck item that Jewelcrafters create via Crafting Orders. The 418-ilvl version of the item is impossible to craft without an inspiration proc (the skill required to craft a 418-ilvl is below the maximum skill a player can have, even with ideal skill point allocation). A 3-8% buff in inspiration, equivalent to 3-8 more 418-ilvl Lariats for each 100 crafted, seems like a safe place to constrain the buff, while remaining enticing enough to be sought after. Using this 3% lower bound on the buff results in $C = 30 / \ln(2) = 43.3$, and the following inspiration gains as a function of stack number:
    
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



### Awarding Artisan Tokens

_Do we encourage players to do Crafting Orders for hours by granting the currency for each order? Do we instead motivate diversity in play by granting the currency for only the first X orders each day? Does the former turn the currency into an unenjoyable grind to get any rewards? Does the latter turn the currency into a daily to-do that players end up dreading?_




