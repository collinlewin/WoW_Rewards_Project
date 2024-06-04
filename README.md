<h1 align="center">
  <img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/af6ea950-8b1b-48ac-b19b-303fc8fd5737" width="50%" height="50%">
</h1>
For well over a decade, World of Warcraft has sustained my excitement over thousands of hours of collecting mounts, progressing in raids, making friends, and mastering professions. In this project, I will walk through my throught process behind designing and implementing new rewards systems for Azeroth and beyond. 

<h2>
  <img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/880d67fa-132f-499b-80b6-5c02f2b9dbfd" width="30%" height="30%">
</h2>

We will first explore areas of the game in which rewards can be introduced, catering to various types of players. Some of these ideas will be fleshed out more than others and include implementation plans informed by statistical modeling.

Yee (2006) proposed that there are three main types of gamers, each with various subtypes: _achievement_ (advancement, mechanics, competition), _social_ (socializing, relationship, teamwork) and _immersion_ (discovery, roleplaying, customization, escapism). While players often fall into multiple groups, I found brainstorming rewards to enhance these different player groups to be an interesting starting point. 
- An alternative, more-optimal starting point would be data-driven. _Where are players spending the most time, and how does retention compare for players who prefer pet battles versus raiding versus professions? How do these statistics compare to previous expansions/systems?_

I first considered new rewards that would incentivize gameplay that the social gamers would enjoy. PvE and PvP excel in this department, more often than not requiring teamwork to succeed in mythics, battlegrounds, and arenas, to name a few. Professions, while often a peaceful solo activity, show much potential for additional rewarding of social interaction. The introduction of the Crafting Order system in Dragonflight promoted more interaction between "professionals" and their customers, in contrast to the sole use of the Auction House. I will thus focus on developing rewards that will incentivize use of the Crafting Order system, which I hypothesize will positively impact players that enjoy social interaction and immersion through roleplaying. 

<h2>
  <img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/24842a7b-fb34-444c-ac85-c5d1aeb622ee" width="60%" height="60%">
</h2>
Professionals who complete Crafting Orders are rewarded with gold and, less often, profession levels. Thus, the reward for Crafting Orders is the same as that for using the Auction House in a majority of cases. Additionally, the cadence/schedule for the current Crafting Order reward is short-term in that the main reward (gold) is awarded once per Crafting Order. It might be meaningful to include additional rewards earned over a longer period of time, granting a sense of satisfaction similar to that from long-term career development. Such potential new reward systems could include...

* **New Currency: Artisan Tokens**

  - Overview
    - Introduce a new currency, Artisan Tokens, awarded for completing crafting orders. Artisan Tokens can be exhanged for profession-specific cosmetic items (e.g., transmogs, toys, pets, mounts) at each profession's Artisan Token vendor, located near each profession station in the capital city.
      - Cosmetics for each profession improve immersion through roleplay and customization, as they better reflect the player's identity as a distinguished member of their profession. Bind-on-pickup (BoP) cosmetics also seem relatively simple to implement with respect to (a lack of) economic impacts, etc.
      - I played it fairly safe for the items in the store, but I noticed that this could be a great place to explore introducing crafting table customizations. Implementation could resemble mount cosmetic options introduced for Dragonriding in Dragonflight.
  - Rate of Reward
    - _Do we encourage players to do Crafting Orders for hours by granting the currency for each order? Do we instead motivate diversity in play by granting the currency for only the first X orders each day? Does the former turn the currency into an unenjoyable grind to get any rewards? Does the latter turn the currency into a daily to-do that players end up dreading?_
      - Limiting the number of token-awarding Crafting Orders per day allows a more fair opportunity to earn tokens for professions that struggle to obtain as many orders as other professions. As such, I will choose to grant Artisan Tokens for the first 4 orders each day to match the current limit of 4 public Crafting Orders per day. Data on the current distribution of Crafting Orders might be more informative for determining this value, but 4 seems reasonable.
  - Amount of Reward
    - More impressive Crafting Orders (e.g., higher ilvl gear) should be rewarded with more Artisan tokens as an extra Reward of Glory that praises the player for their exceptional work. I select a somewhat arbitrary but reasonable range of 8-20 Artisan tokens per Crafting Order and determine the cosmetic prices using this range.
  - Balancing Token Acquisition Across Professions
    - An obvious flaw in this currency is that some professions use Crafting Orders far less than others (e.g. Alchemy), and some not at all (e.g. gathering professions). Two potential solutions arise to include these professions in gaining Artisan tokens via social interactions:
      1) Collaborative Harvesting: Resource nodes harvested by multiple people in a group at the same time awards Artisan Tokens, thus motivating guild/friend harvesting runs.
      2) Collaborative Projects: Professions in lower demand for Crafting Orders (again, Alchemy comes to mind but data could inform this) can assist/"collaborate" on Crafting Orders from higher-demand professions, such as a piece of gear. Such collaboration is inspiring, boosting the Crafting Order's inspiration and thus probability of increasing in quality. Both collaborators are granted additional Artisan Tokens.
        - System incentivizes customer by higher chance of better item, and the collaborators with extra Artisan Tokens and a higher chance of receiving a larger tip (players often tip more gold for higher quality crafts).

  <h3>
  <img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/8c4c1dfc-a543-47b1-a93f-c5aea246b860" width="65%" height="65%">
  </h3>
  
    - Here, I will perform statistical modeling to inform the price of the items in the Artisan Token store; namely, profession-themed toys, pets, a cosmetic armor set, and a mount. By understanding how many tokens players are expected to accumulate after a simulated amount of time, considering their daily activities (i.e., how many orders on average per day), we can set prices that reflect the time and effort chosen to earn these items. The choice of price is essential for ensuring that players feel a sense of accomplishment and reward, without the system becoming an unenjoyable grind.
      
    - Instead of assuming a constant number of orders per day, I use a Poisson distribution to capture the variability in daily player activities, as some days might have more or fewer orders than others. The Poisson distribution is particularly well-suited for modeling the number of crafting orders a player completes each day, assuming that crafting orders can be considered as independent events occurring at a roughly constant average rate (λ). This rate represents the average number of orders per day a player is expected to complete; as such, we explore a range of values to explore different levels of engagement. 
      
    - To translate this individual variability into a comprehensive understanding of token accumulation over time, we employ Monte Carlo simulations. Monte Carlo methods rely on repeated random sampling, in our case running a large number of simulations to generate a robust distribution of the total tokens accumulated over a specified number of days. This approach allows us to account for the variability and randomness in individual player behavior, providing a detailed statistical understanding of the likely outcomes in token amounts.
      
      **Procedure:**
      
      1. **Simulating Token Accumulation:**
         - Each day, the number of crafting orders completed by a player is drawn from a Poisson distribution with a specified λ (average number of orders per day).
         - As mentioned earlier, the number of tokens will be in the range 8-20 to start, depending on craft quality. To simulate this, the token value of each craft will be drawn at random from a uniform distribution (each value equally likely). 
      
      2. **Running Monte Carlo Simulations:**
         - The above simulation process is repeated 100,000 times for 4 values of λ (corresponding to an average of 1, 2, 3, 4 orders per day). This results in a comprehensive distribution of total tokens for each λ value.
        
      Let's say the average participating player (meaning $λ = 2-3$ orders per day) should earn a toy in a week time. It seems fair to price a piece of the cosmetic set at roughly the same price of time. We run the Monte Carlo simulations for the course of a week (in simulation time, it takes only a few seconds on my Macbook):
      <p align="center">
        <img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/491d2fbb-ab21-4b4b-9f13-8ec2a8886121" width="60%" height="60%">
      </p>
      Based on the results, the price of a toy and average cosmetic set piece should be somewhere in the overlap of the $λ=2, λ=3$ distributions. More specifically, I will use the 75th percentile of the $λ=2$ distribution, meaning that 75% of players who complete 2 crafting orders per day on average will be able to afford the toy/average cosmetic piece after a week. This prices the item at 220 Artisan Tokens, which is equivalent to the 20th percentile of the $λ=3$ distribution. Repeating this procedure for two weeks, which seems fair to afford the pet, and a month to afford the mount and using the 75th percentile of the $λ=2$ distribution results in the following prices:

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
