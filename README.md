<h1 align="center">
  <img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/af6ea950-8b1b-48ac-b19b-303fc8fd5737" width="50%" height="50%">
</h1>

World of Warcraft has sustained my excitement for over a decade of collecting mounts, progressing in raids, hunting achievements, mastering professions, and so much more. In this project, I will walk through my thought process behind designing and implementing new rewards systems for Azeroth and beyond. 

My professional background is in statistical modeling and artificial intelligence/machine learning techniques, which I have applied to push forward our understanding of astrophysics and materials. All machine learning algorithms boil down to maximizing a reward, which takes the form of a function that we design to reflect how accurately the model either predicts a value or classifies a data point. In some cases, there is quite literally a reward that awards a behavior, like in my research to train robots to navigate environments by rewarding positive actions (avoiding an obstacle) and penalizing negative actions (colliding with an obstacle). Similar to some of the project below, my research focused on determining the values of these rewards and penalties that resulted an optimal path that the robot could take through the environment. Outside of work, I write fantasy stories and create board games with my partner. This project demonstrates me applying my professional skills and passion for game design to show my current understanding of rewards systems in my favorite video game. I am very excited and open to learning more through collaboration and applying my background to a game I am incredibly passionate about.

<h2>
  <img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/880d67fa-132f-499b-80b6-5c02f2b9dbfd" width="30%" height="30%">
</h2>

First, we will explore areas of the game in which rewards can be introduced, catering to various types of players. Some of these ideas will be fleshed out more than others and include plans for implementation that are informed by statistical modeling.

Yee (2006) proposed that there are three main types of gamers, each with various subtypes: _achievement_ (advancement, mechanics, competition), _social_ (socializing, relationship, teamwork), and _immersion_ (discovery, roleplaying, customization, escapism). While players often fall into multiple groups, I found that brainstorming rewards that would enhance the experience for these different player groups to be an interesting starting point for brainstorming. 

- An alternative, perhaps more-optimal starting point would be data-driven; for example, asking _where are players spending the most time, and how does retention compare between players who participate in different activities (e.g., pet battles, raiding, professions)? How do these statistics compare to those in previous expansions, where different reward systems were in place?_

I chose to consider new rewards that would incentivize and make the game more exciting for the social type of gamer. PvE and PvP naturally excel in this department in that they typically require teamwork to succeed in mythics, battlegrounds, arenas, etc. Professions, while often a peaceful solo activity, show potential for additional rewards that encourage social interaction. 

The introduction of the Crafting Order system in Dragonflight promoted more interaction between "professionals" and their customers, in contrast to use of the Auction House alone. Therefore, I will focus on developing rewards that promote use of the Crafting Order system while making the game more enjoyable for players that prioritize social interaction as well as those who enjoy immersion through roleplaying. 

<h2>
  <img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/24842a7b-fb34-444c-ac85-c5d1aeb622ee" width="60%" height="60%">
</h2>
Players who complete Crafting Orders are rewarded with gold and, less often, profession levels. The reward for Crafting Orders is therefore the same as that for using the Auction House in most cases. Additionally, the cadence/reward schedule for Crafting Orders is short-term (one reward per order). It might be meaningful to include additional rewards earned over a longer period of time, which could grant an additional sense of pride that resembles long-term career development. I explore two reward systems: Artisan Tokens and Flow State.

<img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/2160c8da-abd3-4372-9bff-b62d485eca18" width="50%" height="50%">

  - **Overview**
    - A new currency, Artisan Tokens, is awarded for completing crafting orders. Artisan Tokens can be exhanged for profession-specific cosmetic items (e.g., transmogrification armor, toys, pets, mounts). Each profession has their own Artisan Token vendor, located near each profession station in the capital city.
      - Cosmetics unique to each profession improve immersion through roleplay that comes with customization, which as a whole better reflects the player's identity as a distinguished member of their profession. Bind-on-pickup cosmetics also seem relatively simple to implement in terms of (minimal) economic impacts, etc.
      - While I played it safe for the types of cosmetic items sold in the store, I noticed that this could be a great place to explore introducing vanity options for each player's profession stations. Implementation could resemble the mount customization options introduced for Dragonriding in Dragonflight.
     
  - **Rate of Reward**
    - _Do we encourage players to do Crafting Orders for hours by granting Artisan Tokens for each order? Do we instead motivate diversity in play activities by granting the currency for only the first X orders each day? Does the former turn the currency into an unenjoyable grind? Does the latter turn the currency into a daily to-do that players end up dreading?_
      - Limiting the number of Crafting Orders that award tokens each day allows for professions that are in less demand for Crafting Orders a more fair opportunity to earn Artisan Tokens. As such, I will choose to grant Artisan Tokens for the first 4 orders each day to match the current limit of 4 public Crafting Orders per day.
        - Data on the current distribution of Crafting Orders completed per day would be more informative for determining this limit, but 4 seems reasonable.
     
  - **Amount of Tokens Rewarded**
    - More impressive Crafting Orders (e.g., higher item level gear) should be rewarded with more Artisan Tokens as a form of praise for the player's exceptional work. I select a somewhat arbitrary but reasonable range of 8-20 Artisan Tokens awarded per Crafting Order, and focus on determining the cosmetic prices based on this range.
   
  - **Balancing Token Acquisition Across Professions**
    - An obvious flaw in this currency is that some professions use Crafting Orders far less than others (e.g. Alchemy, most notably gathering professions). Two potential solutions arise to balance these professions out in gaining Artisan Tokens while still targeting social interactions:
   
      1) **Collaborative Harvesting**
          - Resource nodes that are harvested by multiple people within the same group simultaneously awards Artisan Tokens, thus motivating guild/friend harvesting runs.
            - Apply to only party (non-raid) groups to maintain the 5-person limit (I believe this is the current limit?) for harvesting a node to avoid an increase in the amount of the resource on the market in order to minimize economic impact.
    
      2) **Collaborative Projects**
          - Professions in lower demand for Crafting Orders (data could inform this) can assist/"collaborate" on Crafting Orders from higher-demand professions; for example, crafting a piece of gear. Such collaboration is inspiring, boosting the Crafting Order's inspiration and thus probability of increasing in quality. Both collaborators are granted additional Artisan Tokens.
            - Use of this system is incentivized by all players involved: customer has a higher chance of receiving a better item, while both collaborators are awarded additional Artisan Tokens and a higher chance of receiving a larger tip (players often tip more gold for higher-quality crafts).

  ### Simulations for Cosmetic Store Pricing
  
  Here, I perform statistical modeling to inform the price of the items in the Artisan Token store; namely, toys, pets, a cosmetic armor set, and a mount. By predicting how many tokens players are expected to accumulate after some amount of time, while accounting for differences in daily activities (i.e., how many orders completed per day on average), we can set prices that reflect the time and effort we believe should be required to earn these items. Setting a well-informed price is essential to ensure that players feel accomplished, without the system becoming an unenjoyable grind.
          
  Instead of assuming a constant number of orders per day, I use a Poisson distribution to capture player variability, with some days having greater or fewer orders than other days. The Poisson distribution is particularly well-suited for modeling the daily number of Crafting Orders, assuming that each order can be considered as an independent event occurring at a roughly constant average rate (λ).
     - This rate reflects the player's engagement to the system, and is equal to the average number of orders completed per day, so I explore a range of values to account for different levels of engagement. 
          
  I then carried out a set of Monte Carlo simulations to translate the randomness in individual player behavior into an understanding of the likely outcomes in accrued token amounts. Monte Carlo methods rely on repeated random sampling, in this case running a large number of simulations, where each simulation represents a player at a specified level of engagement λ. This process results in distributions of the total tokens accumulated over the specified number of days.
  
  **Detailed Procedure:**

  - Source code available in repo, see crafting_orders.ipynb.
    
  1. **Simulating Token Accumulation for an Individual Player:**
     - Each simulated day, the number of Crafting Orders completed by a player is drawn from a Poisson distribution with a specified λ (average number of orders per day).
     - As mentioned earlier, the number of tokens will be in the range 8-20, depending on craft quality. To simulate this, the token value of each craft will be drawn at random from a uniform distribution (each value is equally likely). 
  
  2. **Running Monte Carlo Simulations:**
     - The simulation process above (section i) is repeated 100,000 times for 4 values of λ (corresponding to an average of 1, 2, 3, 4 orders per day). This results in a comprehensive distribution of total tokens for each λ value.
      
  Let's say the average participating player, meaning $λ = 2-3$ orders per day on average, should earn a toy in a week's time. It seems fair to price a piece of the cosmetic set at roughly the same price in time as a toy. We simulate a week of token accrual using the Monte Carlo simulations:
    <p align="center">
      <img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/8306e539-0ce8-418f-944b-c5c33103e7dc" width="60%" height="60%">
    </p>

  
  Based on the previous pricing criteria, the price of a toy and average cosmetic set piece should be somewhere in the overlap of the $λ=2, λ=3$ distributions. I will specifically use the 75th percentile of the $λ=2$ distribution, meaning that 25% of players who complete 2 crafting orders per day on average will be able to afford the toy or cosmetic piece after a week. This prices the item at 220 Artisan Tokens, which is equivalent to the 20th percentile of the $λ=3$ distribution (80% of these players can afford the item).

  I repeated this procedure, simulating two weeks of token earnings, a fair time span for affording the pet again. I again price the item at the 75th percentile of the $λ=2$ distribution. I decided on a month to afford the mount for those working a bit harder, so instead using the 50th percentile (i.e. the median) of the $λ=3$ distribution. In this case, >99% of those maxing their crafting order tokens limit ($λ=4$) every day for a month could afford the mount. This resulted in the following prices and distributions for 30 days of token accrual:

<h3 align="center"></h3>

<table>
  <tr>
    <td>
      <table>
        <tr>
          <th>Item</th>
          <th>Price in Time (days)</th>
          <th>Price in <br>Artisan Tokens</th>
        </tr>
        <tr>
          <td>Toys</td>
          <td>7</td>
          <td>220</td>
        </tr>
        <tr>
          <td>Average Transmog<br> Piece</td>
          <td>7</td>
          <td>220</td>
        </tr>
        <tr>
          <td>Pets</td>
          <td>14</td>
          <td>420</td>
        </tr>
        <tr>
          <td>Mount</td>
          <td>30</td>
          <td>1100</td>
        </tr>
      </table>
    </td>
    <td>
      <img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/43f298d1-ba5c-4af1-b67e-9e56190b5ee3">
    </td>

  </tr>

</table>

<img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/6d6ecda2-d06d-4390-a97c-8f238cf862dd" width="50%" height="50%">

  - **Overview**
    - Completing a crafting order grants a status effect, Flow State, that increases inspiration for the next crafting order.
      - An interesting alternative is to buff either a random crafting stat or the player's highest crafting stat, which could emphasize the player's crafting build/prioritized stat and thus an identity for immersion purposes.
        
  - **Duration**
    - I am divided between two options for the buff duration: ~30 minutes, or 24 hours. The former motivates a single, continuous session of orders. The latter motivates a daily 'streak'-style engagement with the feature. In either case, the duration is short enough to motivate more crafting orders, but not too short as to bring source of stress and hasty rudeness to the next customer.
      
  - **Stacking**
    - Another consideration is whether the effect will stack; that is, if the player completes an order before the buff expires, the duration will be reset and the player will gain a stack. Additional stacks will provide additional inspiration gain and thus incentivize "keeping the ball rolling", i.e. sustained Crafting Order completion.
   
  - **Buff Amount and Functional Form**
    - Without stacking, the buff could increase inspiration by either a flat amount, or a percentage of the user's current inspiration.
      - Buffing by a flat amount could avoid encouraging more players into an inspiration-focused build, as would be the case with a percentage-informed buff.
    - With stacking, a linear scaling of inspiration gained ($IG$) with the number of stacks ($s$) is likely too extreme. Instead, a slower, logarithmic growth seems more appropriate: $$IG = C \ln(s + 1)$$ where $C$ is a constant that rescales the amount of inspiration gained. Note: $s+1$ is used within the logarithm such that $IG(0) = 0$, meaning that no inspiration is gained without a stack.
    - To determine a reasonable value for C, we recall that 10 more points of inspiration translate to a 1% increase in probability of crafting an item with higher base skill. To put this into recent context, the Elemental Lariat is a neck item that Jewelcrafters commonly craft for Crafting Orders. Crafting the 418-ilvl version of the item requires an inspiration proc (the skill required to craft a 418-item-level version is below the maximum skill that a player can have). A 3-8% buff in inspiration is equivalent to 3-8 more 418-ilvl Lariats expected for each 100 crafted, which seems like a safe range for the buff while remaining enticing enough to be sought after. Using this 3% lower bound on the buff results in $C = 30 / \ln(2) = 43.3$, with the following inspiration gains as a function of stack number:
    
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

<h1 align="center">
  <img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/9e914fa0-76ea-4e41-b486-ec5960219824" width="20%" height="20%">
</h1> 
<p align="center">
Thank you for reading! I appreciate you taking the time in your busy day to read through the project. See you in Azeroth!
  <br>

<p align="center">  
 <img alt="Screenshot 2024-06-03 at 8 36 20 PM" src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/4f88c2fe-5778-445c-a175-5acb6d0d3553" width="10%" height="10%"> <br>
</p>
</p>

