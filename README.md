<h1 align="center">
  <img src="https://github.com/collinlewin/WoW_Rewards_Project/assets/28280691/d2b215d6-a225-460e-92da-7714274b9e98" width="50%" height="50%">
</h1>
For well over a decade, World of Warcraft has sustained my excitement over thousands of hours of collecting mounts, progressing in raids, making friends, and mastering professions. In this project, I will walk through my throught process behind designing and implementing new rewards systems for Azeroth and beyond. 

## Brainstorming

We will first explore areas of the game in which rewards can be introduced, catering to various types of players. Some of these ideas will be fleshed out more than others and include implementation plans informed by statistical modeling.

Yee (2006) proposed that there are three main types of gamers, each with various subtypes: _achievement_ (advancement, mechanics, competition), _social_ (socializing, relationship, teamwork) and _immersion_ (discovery, roleplaying, customization, escapism). While players often fall into multiple groups, I found brainstorming rewards to enhance these different player groups to be an interesting starting point. 
- An alternative, more-optimal starting point would be data-driven. _Where are players spending the most time, and how does retention compare for players who prefer pet battles versus raiding versus professions? How do these statistics compare to previous expansions/systems?_

I first considered new rewards that would incentivize gameplay that the social gamers would enjoy. PvE and PvP excel in this department, more often than not requiring teamwork to succeed in mythics, battlegrounds, and arenas, to name a few. Professions, while often a peaceful solo activity, show much potential for additional rewarding of social interaction. The introduction of the Crafting Order system in Dragonflight promoted more interaction between "professionals" and their customers, in contrast to the sole use of the Auction House. I will thus focus on developing rewards that will incentivize use of the Crafting Order system, which I hypothesize will positively impact players that enjoy social interaction and immersion through roleplaying. 

## Crafting Order Reward Systems

Professionals who complete Crafting Orders are rewarded with gold and, less often, profession levels. Thus, the reward for Crafting Orders is the same as that for using the Auction House in a majority of cases. Potential new reward systems could include...

* New Currency: Artisan Tokens
  - Introduce a new currency, Artisan Tokens, awarded for completing crafting orders. Artisan Tokens can be exhanged for profession-specific cosmetic items (e.g., transmogs, toys, pets, mounts) at a vendor near their profession's station in the capital city.
    - Cosmetics enable better immersion through roleplay and customization, as they better reflect the player's identity as a distinguished member of their profession. Bind-on-pickup (BoP) cosmetics also appear to be the simplest to implement in terms of economic impacts, etc.
  - 
 
* New Status Effect: Flow State
  - Completing a crafting order grants a status effect, Flow State, that increases inspiration for the next crafting order.
  - Duration needs to be short enough to keep the cycle going of crafting orders, but not too short as to bring source of stress and hasty rudeness to the next customer.
    - Suggested time: 5-10 minutes.
  - Consider whether the effect will stack (e.g. max of 5 stacks), contributing to additional inspiration and incentivizing a sustained contribution to the economy akin to real blacksmith, etc.
    - A linear scaling of additional inspiration (hereafter, $AI$) with the numer of stacks is likely too extreme. Instead, a slower, logarithmic growth seems more appropriate: $$AI = A \ln(s + 1)$$ where constant $C$ rescales the amount of inspiration gained. Note: $C$ does not affect the percent increase between number of stacks (e.g., the ratio $AI(3)/AI(2)$ is independent of $C$). As a check of our functional form, we check the percentage increase in $AI$ across the number of stacks.
   
| Stacks (s)  | % Increase in  |
| ------------- | ------------- |
| 1 →  2  | Content Cell  |
| 2 →  3  | Content Cell  |
| 3 →  4  | Content Cell  |
| 4 →  5  | Content Cell  |

### Awarding Artisan Tokens

_Do we encourage players to do Crafting Orders for hours by granting the currency for each order? Do we instead motivate diversity in play by granting the currency for only the first X orders each day? Does the former turn the currency into an unenjoyable grind to get any rewards? Does the latter turn the currency into a daily to-do that players end up dreading?_




