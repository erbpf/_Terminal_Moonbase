# _Terminal Moonbase

<link width="50%" height="auto"><a href="https://terminal.c1games.com/"><img src="https://ai-games.s3-us-west-2.amazonaws.com/assets/terminalX/playing.gif" alt="alt text" height="auto"></a></div>

---

## Player code repository for  _Terminal

<div  data-v-fbb09ee2="" id="game-reference-container" class="s3 s3-resource-board"><div data-v-fbb09ee2="" id="rules-section" class="reference-content s3"><div id="rules-text" class="rules-text"><!----><div id="GameStory" style="text-align: left;"><h1 id="terminal-master-rule-book">Terminal Master Rule Book</h1><h2 id="game-story">Game Story</h2><p>In the distant future, humanity has no memories of conflict or scarcity. Advanced algorithms solve society's most challenging problems. Everlasting peace, mathematical regularity, and technological progress prevail.</p><p>
    The precondition for society’s peace and progress is the
    <em>Terminal</em>, a global idea battle-arena. In the
    <em>Terminal</em>, algorithms compete based on speed and intelligence. Winning algorithms are highly secure and cleverly breach their opponent’s defenses. The rule of law follows the winning algorithm.
  </p><p>
    But now, you suspect the
    <em>Terminal</em> has been compromised. You must deploy your algorithm to the arena to reclaim it. We are all depending on it…
  </p></div><div id="GameRequirements" style="text-align: left;"><h2 id="game-requirements">Game Requirements</h2><p>
    Terminal requires the
    <a href="https://www.google.com/chrome/" target="_blank">Google Chrome</a> browser to upload, debug and test your algorithms on our website or to play by hand. Please download/update to the latest version for an optimal experience.
  </p><p>However, in order to run the game locally for more convenient testing, there are a few free language installation requirements:</p><h5 id="-a-href-https-www-python-org-downloads-release-python-360-target-_blank-python-3-6-or-latest-a-"><a href="https://www.python.org/downloads/release/python-360/" target="_blank">Python 3.6 or latest</a></h5><br><h5 id="-a-href-https-www-oracle-com-technetwork-java-javase-downloads-jdk11-downloads-5066655-html-target-_blank-java-10-or-latest-a-"><a href="https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html" target="_blank">Java 10 or latest</a></h5><p>Additionally Windows users will need to use:</p><h5 id="windows-powershell-v5-or-latest-included-in-windows-10-">Windows PowerShell v5 or latest (included in Windows 10)</h5><p>
    Older versions of Windows, such as Windows 7, can
    <a href="https://docs.microsoft.com/en-us/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell" target="_blank">update their PowerShell for free</a>, simply click the link under the PS 5.1 column matching your windows version.
  </p><p>
    If you have trouble playing the game on our website or locally please check the
    <a href="https://github.com/correlation-one/C1GamesStarterKit/" target="_blank">readme in the starterkit repo</a>, or our
    <b><a href="#Troubleshooting">troubleshooting section</a></b>.
  </p></div><div id="GameplayOverview" style="text-align: left;"><h2 id="gameplay-overview">Gameplay Overview</h2><p>Correlation One’s Terminal is a member of the Tower Defense game genre. It is a two-player, simultaneous-turns game that takes place on the diamond-shaped arena shown above. One player occupies the bottom half of the arena, while the other player occupies the top half. When creating your algorithm, you can assume you occupy the bottom half of the arena and write code from this orientation. The game engine handles symmetry when running your algo from the top half.</p><p>Players code algorithms that send <b><a href="#Glossary">Information</a></b> (offensive units) to either of the two Edges on their opponent’s side of the arena. Players use <b><a href="#Glossary">Firewall</a></b> (defensive units) to defend their own arena edges. All units have <b><a href="#Glossary">Health</a></b> (i.e. health) and when their health reaches zero, they are destroyed and removed from the arena. Some units will <b><a href="#Glossary">Attack</a></b> and attempt to destroy enemy units that enter their <b><a href="#Glossary">Range</a></b> of operation. Throughout the game, both players are provided two resources - <b><a href="#Glossary">Bits</a></b> and <b><a href="#Glossary">Cores</a></b> - which are used to create Information and Firewall, respectively.</p><p>The key differences between Information and Firewall are shown in the table below:</p><table><thead><tr><th></th><th>Information</th><th>Firewall</th></tr></thead><tbody><tr><td>Where is it Deployed?</td><td>From either of your two arena edges</td><td>On any square in your half of the arena</td></tr><tr><td>How does it Move?</td><td>Moves to opposite arena edge, using pathing algorithm described <b><a href="#UnitMovement">below</a></b></td><td>Stationary (does not move)</td></tr><tr><td>What does it Target?</td><td>Targets all enemy units</td><td>Only attacks enemy Information units</td></tr><tr><td>What resources are used to Deploy it?</td><td>Bits</td><td>Cores</td></tr></tbody></table><p>Units differ in their cost, health, damage, and range of operation. Click on the drop-downs below to learn more about Units. </p><details open="open"><summary>Information Units - Attackers:</summary><p>Information units are deployed from either of the two edges on the player’s side of the arena, and aim to reach the opposite edge in enemy territory. They attack enemy Information and Firewall while moving. Firewall attack incoming enemy Information units, acting as a defense. </p><p>
      If Information units successfully reach the opposite edge, they decrease the opponent’s Health by
      <span>1</span>
      point and award
      <span>1</span>
      Cores for the deploying player; they then disappear from the arena.
    </p><p>There are three types of Information units. The <b><a href="#Glossary">Ping</a></b> is a fast-moving unit which deals light damage. The <b><a href="#Glossary">EMP</a></b> is expensive and easily destroyed, but it's high damage and far range and can wreak havoc on enemy defenses. The <b><a href="#Glossary">Scrambler</a></b> is a high-health unit that deals high damage to enemy Information units, but cannot attack enemy Firewall. The three types of Information units and their characteristics are detailed below:</p><table><thead><tr><th></th><th>Unit Image</th><th>Cost</th><th>Health</th><th>Range*</th><th>Damage</th><th>Speed*</th></tr></thead><tbody><tr><td>Ping</td><td><img src="https://storage.googleapis.com/prod-terminal-assets/prod-manager-static/static/img/ping.26f2d1ea.svg" alt="alt text"></td><td><span>1</span>
            Bits
          </td><td><span>15</span></td><td><span>3.5</span></td><td><span>2</span></td><td><span>1</span></td></tr><tr><td>EMP</td><td><img src="https://storage.googleapis.com/prod-terminal-assets/prod-manager-static/static/img/emp.30305da4.svg" alt="alt text"></td><td><span>3</span>
            Bits
          </td><td><span>5</span></td><td><span>4.5</span></td><td><span>8</span></td><td><span>2</span></td></tr><tr><td>Scrambler</td><td><img src="https://storage.googleapis.com/prod-terminal-assets/prod-manager-static/static/img/scrambler.23a58279.svg" alt="alt text"></td><td><span>1</span>
            Bits
          </td><td><span>40</span></td><td><span>4.5</span></td><td><span>20</span></td><td><span>4</span></td></tr></tbody></table><p><sup> *Range: Maximum euclidian distance of a targetable coordinate </sup><br><sup> *Speed: Frames required to move one space</sup></p></details><details open="open"><summary>Firewall Units - Defenders:</summary><p>Firewall are stationary units that do not move. They block the paths of both friendly and enemy Information units, and no two Firewall can occupy the same location. They persist across multiple turns.</p><p>There are three types of Firewall. The <b><a href="#Glossary">Filter</a></b> is a cheap, simple Firewall used to influence the paths units take and to protect more valuable Firewall. <b><a href="#Glossary">Encryptor</a></b> provide additional health once to friendly Information units that pass within range. <b><a href="#Glossary">Destructor</a></b> attack enemy Information units. A Firewall unit can also be upgraded to gain stats. Missing health persists when a tower's health is increased by an upgrade. The upgrade cost is the same as the units base cost unless otherwise stated. The three types of Firewall and their characteristics are:</p><table><thead><tr><th></th><th>Unit Image</th><th>Cost</th><th>Health</th><th>Range*</th><th>Damage</th><th>Encryption</th><th>Upgrade</th></tr></thead><tbody><tr><td>Filter</td><td><img src="https://storage.googleapis.com/prod-terminal-assets/prod-manager-static/static/img/filter.04350892.svg" alt="alt text"></td><td><span>1</span>
            Cores
          </td><td><span>60</span></td><td><span>N/A</span></td><td><span>N/A</span></td><td>N/A</td><td>
            Health -&gt; 120
          </td></tr><tr><td>Encryptor</td><td><img src="https://storage.googleapis.com/prod-terminal-assets/prod-manager-static/static/img/encryptor.ad139259.svg" alt="alt text"></td><td><span>4</span>
            Cores
          </td><td><span>30</span></td><td><span>3.5</span></td><td><span>N/A</span></td><td><span>3</span></td><td>
            Range -&gt; 7
            <div>
              Shield -&gt; 4
            </div></td></tr><tr><td>Destructor</td><td><img src="https://storage.googleapis.com/prod-terminal-assets/prod-manager-static/static/img/destructor.9bdf4285.svg" alt="alt text"></td><td><span>6</span>
            Cores
          </td><td><span>75</span></td><td><span>3.5</span></td><td><span>16</span></td><td>N/A</td><td>Damage -&gt; 32</td></tr></tbody></table><p><sup> *Range: Maximum euclidian distance of a targetable coordinate </sup></p></details><br><br></div><div id="Objective" style="text-align: left;"><h4 id="objective">Objective</h4><p>In Terminal, the objective is to reduce your opponents health to zero. You can do this by advancing Information units to your opponent's edge, while defending your own edges from your opponent's incoming Information. Players compete by coding algorithms to manage offensive units (Information) and defensive units (Firewall).</p><p><img src="https://ai-games.s3-us-west-2.amazonaws.com/assets/terminal-example-gameplay.gif" alt="alt text" title="Terminal Example Round"></p></div><div id="Map" style="text-align: left;"><h4 id="map">Map</h4><p>Units in terminal are placed and move along a diamond-shaped grid. The coordinates on the grid range from 0,0 to 27,27. Note that half of these coordinates fall outside the diamond shaped gameplay area. Understanding these coordinates is essential for algo creation.</p><p><img src="https://ai-games.s3-us-west-2.amazonaws.com/assets/map.png" alt="alt text" title="Map"></p></div><div id="GameStart" style="text-align: left;"><h4 id="game-start">Game Start</h4><p>
    Each player begins the game with
    <span>40</span> Cores,
    <span>5</span> Bits, and
    <span>30</span> Health.
  </p><p><img src="https://ai-games.s3-us-west-2.amazonaws.com/assets/terminal-resources-ui.png" alt="alt text" title="Terminal Resource and Health"></p><p>
    You can see each players' available resources at current point of game playback in the upper corners
    of the game board. The gauge represents your owned proportion of the total resources available
    between the players.
  </p></div><div id="TurnStructure" style="text-align: left;"><h4 id="turn-structure">Turn Structure</h4><p>Each turn is split up into three phases: Restore, Deploy, and Action. In the restore phase, players are granted resources. In the deploy phase, players choose where they want to deploy their units. In the action phase, deployed units act automatically according to the game rules.</p></div><div id="RestorePhase" style="text-align: left;"><p><strong>1. “Restore” Phase</strong> Players lose a fraction of their stored Bits from the previous turn and then are given additional Bits and Cores. Players are also shown the current game state. The below resource schedule explains how resources are allocated during the game.
  </p><details open="open"><summary>More</summary><p>
      At the start of each turn (except the first one), a “decay” mechanic is applied whereby each player automatically loses <span>0.25</span> of all Bits stored from the previous turn. Following this players are given  <span>5</span> Cores and <span>5</span> Bits, plus an additional <span>1</span> Bits for every <span>10</span> turns that have passed. For example, at the start of turns 0 through <span>9</span> you recieve <span>5</span> Bits, at the start of turns <span>10</span> - <span>19</span> you recieve <span>6</span>, and so on.
    </p><p>
      In addition to the resources gained at the start of each turn, players gain <span>1</span> Cores for each point of damage they dealt to their opponent’s health in the previous turn.
    </p><p>
      The turn then proceeds in 2 phases: Deploy Phase and Action Phase.
    </p><p><small>Note: Bits decay amount rounds to the nearest tenth.</small></p></details><p><br></p></div><div id="DeployPhase" style="text-align: left;"><p><strong>2. “Deploy” Phase</strong> Players select locations to deploy Information and Firewall using their accumulated Bits and Cores. Players can also choose to remove existing Firewall for some refund. Once both players have made their selections, the Deploy phase is over, and the Action phase begins.
  </p><details open="open"><summary>More</summary><p>
      Players send commands that list where and how many Firewall and Information units they wish to deploy. During this phase, the player can see enemy Firewall which survived the previous action phase, but not the new Units their opponent is deploying. Players will have
      <span>5</span> seconds to submit their commands each turn, after which they will begin taking 1 damage per second.
    </p><p>
      Players are also allowed to remove previously built Firewall from the arena in this phase and receive a refund. This refund is equal to
      <span>0.75</span> of the initial cost of the Firewall, times the percentage of the Firewall’s original health remaining at the time of removal.
    </p><p style="text-align: center; font-size: 1.35em;"><i>Refund</i> =
      <span>0.75</span> *
      <i>InitialCost</i> * (
      <i>RemainingHealth</i>/
      <i>OriginalHealth</i>)
    </p><p>Firewall that are selected to be removed will remain active in the arena for one turn marked visually with a glow and then disappear from the arena after one turn has passed.</p><p>Only one Firewall can be placed on any given board square. In contrast, multiple Information units can be placed on the same board square. When this happens, the Information units ‘stack’ and act independently and simultaneously according to their movement logic (detailed in the Movement and Pathing section below).</p><p><small>Note: Firewall refund amount rounds to the nearest tenth.</small></p></details><br></div><div class="rules-section" id="ActionPhase" style="text-align: left;"><p><strong>3. “Action” Phase</strong> The game engine deploys Information and Firewall according to player choices made in the Deploy phase. The Action phase progresses in discrete Frames and continues until all Information units are destroyed or reach the opponent’s edge.
  </p><details open="open"><summary>More</summary><p>After both players have chosen which units they wish to deploy, the game engine deploys Information and Firewall according to the commands sent in the Deploy Phase. Then, based on the movement and targeting logic (detailed later), the game automatically controls each player’s units for the duration of the Action Phase. The Action Phase has many discrete Frames and continues until all Information units are destroyed or reach the opponent’s edge.</p><p>Each Frame during the Action Phase is sent to both players. Players cannot send commands during the Action Phase, but can observe, collect information, and plan for the next turn. After the Action Phase, the next turn begins and the cycle repeats.</p><p>During each frame, actions will occur in this order:</p><ol><li><p>Each unit takes a step, if it is time for them to take a step.</p></li><li><p>Each shield decays. See ‘Shielding’ in <b><a href="#UnitDetails">Advanced</a></b> for information about shields. Note that in some variants of terminal, shields do not decay.</p></li><li><p>New shields are applied, if a unit has entered the range of a friendly </p></li><li><p>All units attack. See ‘Targeting’</p></li><li><p>Units that were reduced below 0 health are removed</p></li></ol></details><br></div><div id="GameplayEnd" style="text-align: left;"><h4 id="gameplay-end">Gameplay End</h4><p>
    If a player reduces their opponents health to zero, they will win. If the 100th round is completed, the player with
    the highest health will win. If both algos have the same health at the end of the 100th round or lose all their health simultaniously, the algo with the lowest computation time will be declared the winner.
  </p></div><div id="Resources" style="text-align: left;"><h2 id="resources">Resources</h2><p>Throughout the game, both players are provided two resources - Bits and Cores - which are used to create Information and Firewall, respectively.</p></div><div id="Bits" style="text-align: left;"><h4 id="bits">Bits</h4><p>
    The player gains Bits each turn. They can be used to create Information Units. At the start of the game players are provided with
    <span>5</span> bits. Players are then given
    <span>5</span> bits per turn, with an additional
    <span>1</span> bits per turn for every
    <span>10</span> turns that have passed. A decay effect is applied to stockpiled bits, with bits kept from the previous turn being reduced by
    <span>0.25</span>.
  </p></div><div id="Cores" style="text-align: left;"><h4 id="cores">Cores</h4><p>
    The player gains cores each turn. They can be used to create Firewall Units. At game start players are given
    <span>40</span> cores, and
    <span>5</span> more cores on each subsequent turn. Furthermore, players are awarded with
    <span>1</span> cores for each point of damage dealt to the enemy.
  </p></div><div id="UnitDetails" style="text-align: left;"><h2 id="units-advanced">Units - Advanced</h2><p>
    This section refers to specific details about the implementation of Shielding, pathing, and targeting that is only needed by advanced users. For more basic unit information, see the
    <b><a href="#GameplayOverview">Gameplay Overview</a></b></p></div><div id="UnitMovement" style="text-align: left;"><h4 id="unit-behavior">Unit Behavior</h4><p>Unit Movement, Pathing and Targeting are determined automatically by the game engine.</p><details open="open"><summary>Movement and Pathing:</summary><p>Movement and Pathing are automated by the game’s engine. Details of the information movement logic, as well as edge cases when movement is blocked, are described below.</p><p><strong>Pathing Logic</strong></p><p>In general, the Information Units will always take the shortest path to their destination, and will prefer to zig-zag rather than moving in a straight line for extended periods of time.</p><p>Each Information unit moves at its speed detailed above, taking one step after the required number of frames have passed. Information units can only move left, right, up, or down (not diagonally). Each time the Information Unit takes a step, it will choose the most ideal tile to step onto using the following logic:</p><h5 id="when-it-is-time-for-a-unit-to-choose-a-tile-to-step-onto">When it is time for a Unit to choose a tile to step onto</h5><ol><li><p>Choose the tile which is the shortest number of steps from the Unit’s destination, described below.</p></li><li><p>If multiple tiles are equally close to the units destination, move in the opposite direction of the previous movement. For example, if the Unit made a vertical move on its previous step, it will prefer a horizontal move.</p></li><li><p>In the case where a Unit has just been deployed and has yet to move, it will prefer a vertical movement.</p></li><li><p>If there are two tiles with equal distances and are equally prefered based on direction, the unit will choose one that is in the direction of it’s target edge. For example, if a unit wants to reach the top-right edge, and must choose between moving left and right, if both paths have the same minimum number of steps it will move right.</p></li></ol><h4 id="choosing-a-destination">Choosing a destination</h4><p>A Units destination is usually the opposite edge of the edge it was created on. If the opposite edge is unreachable due to firewall placements, the Unit will instead attempt to reach the deepest possible location in the enemy territory, and then self destruct as described below. The deepest location is the location with the furthest Y coordinate from your territory. If multiple such locations are reachable, the Unit will choose the one closest to its target edge. For example, A unit attempting to reach the top-right corner who can reach [13, 26], [14, 26] and [15, 25] will choose [14, 26]. First, it will narrow its search to [13, 26] and [14, 26], as they have the deepest Y coordinate into enemy territory. Then, it will choose [14, 26] because it wants to reach the top-right edge, and [14, 26] is further to the right than [13, 26]. As another example, a Unit whos target edge is the top-left it will choose [13, 26]</p><p>Note that if a Firewall is destroyed at any point during the Action Phase, a path can become available to a better self-destruct location or the target edge, causing a unit’s path to change dramatically, sometimes even causing it to double back.</p><p><strong>Self-Destruct</strong> If the Information unit’s path is completely blocked, it will go to an open space closest to the opposing edge as described above in pathing logic and self-destruct. The self-destruct only damages enemy units and has a range of <span>1.5</span> (every adjacent square including diagonals). The damage dealt to each affected enemy is equal to the starting health of the self-destructing unit. However, self-destruct damage will only occur if the unit has moved at least <span>5</span> spaces before self-destructing. Units will still attack on the frame that they self-destruct.
    </p></details><details open="open"><summary>Targeting:</summary><p>Targeting is also handled automatically by the game; players cannot directly control which enemy units their deployed Information or Firewall target. Information and Firewall units both follow the same targeting heuristics. They begin with a list of all eligible enemy targets within range, and remove targets from the list in the following order until a unique target is identified:</p><ol><li><p>Prioritize Information over Firewall units</p></li><li><p>Choose the nearest target(s). Note that the potential targets could include multiple locations if they are the same distance away.</p></li><li><p>Choose the target(s) with the lowest remaining health</p></li><li><p>Choose the target(s) which are the furthest into/towards your side of the arena</p></li><li><p>Choose the target closest to an edge</p></li></ol><p>This will almost always uniquely identify at most one enemy unit to target. Each unit can deal damage at most once per Frame.</p><p><strong>Additional Clarifications</strong></p><p>Units fire in the order that they were created. In the rare case that the above logic does not identify a unique unit, the most recently created unit will be chosen. Units that have 0 health will not be targeted. Overkill damage to a unit will not affect another unit. For example, if two one health units are in the same location and one takes 2 damage, the extra point of damage will not affect the other unit.</p></details><h4 id="encryption">Shielding</h4><p>The below informational boxes contain clarifications about the ‘Shielding’ mechanic</p><details open="open"><summary>Shielding:</summary><p>
      Encryptors provide bonus health to allies that move near them as a Shield.
    </p><p>
      A given Encryptor can only shield a given ally one time.
    </p><p>
      Each Encryptor can shield any number of unique allies.
    </p><p>
      Shields stack, and any ally can be shielded by any number of unique encryptors.
    </p><p>
      An Encryptor will attempt to apply a Shield to friendly units that enter its range.
    </p><p>
      There is no limit to the number of new Shields it can apply simultaniously.
    </p></details></div><div id="Download" class="alt-table" style="text-align: left;"><h2 id="download-starter-kit">Download Starter Kit</h2><h4 id="select-your-language">Select Your Language</h4><p>Download the starter kit to start programming your bot. The kit includes starter bots for python, java, and rust.</p><p>
    View the programming documentation
    <a href="https://docs.c1games.com/">here</a></p><p>Can't find your preferred language? We love contributions!</p><p>
    Check out our
    <a href="https://github.com/correlation-one/C1GamesStarterKit/tree/master/community">contribution guide</a> for more information on how to contribute.
  </p><table><thead><tr><th>Language</th><th>Github Repository</th><th>Download</th></tr></thead><tbody><tr><td>Python</td><td><a href="https://github.com/correlation-one/AIGamesStarterKit/tree/master/python-algo"><i class="icon mdi mdi-github"></i> GitHub
          </a></td><td><a href="https://github.com/correlation-one/C1GamesStarterKit/archive/master.zip"><i class="icon mdi mdi-download"></i> Download
          </a></td></tr><tr><td>Java</td><td><a href="https://github.com/correlation-one/AIGamesStarterKit/tree/master/java-algo"><i class="icon mdi mdi-github"></i> GitHub
          </a></td><td><a href="https://github.com/correlation-one/C1GamesStarterKit/archive/master.zip"><i class="icon mdi mdi-download"></i> Download
          </a></td></tr><tr><td>Rust</td><td><a href="https://github.com/correlation-one/AIGamesStarterKit/tree/master/rust-algo"><i class="icon mdi mdi-github"></i> GitHub
          </a></td><td><a href="https://github.com/correlation-one/C1GamesStarterKit/archive/master.zip"><i class="icon mdi mdi-download"></i> Download
          </a></td></tr></tbody></table><h4 id="available-tools">Available Tools</h4><p>Download tools to play games locally. Read the CLI Client Tools README included in the download for installation and usage instructions.</p><table><thead><tr><th>Tool</th><th>Resources</th></tr></thead><tbody><tr><td>CLI Client Tools</td><td><a href="https://github.com/correlation-one/C1GamesStarterKit/tree/master/scripts"><i class="icon mdi mdi-github"></i> GitHub
          </a></td></tr></tbody></table><h4 id="community-tools">Community Tools</h4><p>
    Our community creates and shares a wide variety of tools for developing algos on Terminal. The Terminal
    <a href="https://forum.c1games.com/t/terminal-community-contributions/800/4">projects forum</a> is a great place to talk about any tools you are working on or perhaps even one you'd like to see!
  </p><table><thead><tr><th>Tool</th><th>User</th><th>Resources</th></tr></thead><tbody><tr><td>replay analysis scripts</td><td><a href="https://forum.c1games.com/u/isaac/summary">@Issac</a></td><td><a href="https://forum.c1games.com/t/visualizing-matches-locally/627/17">Thread</a>,
          <a href="https://github.com/correlation-one/C1GamesStarterKit/tree/master/scripts/contributions">Source</a></td></tr><tr><td>Terminal Tools</td><td>
          maintained by
          <a href="https://forum.c1games.com/u/isaac/summary">@Issac</a> (creator
          <a href="https://forum.c1games.com/u/876584635678890/summary">@8</a>)
        </td><td><a href="https://forum.c1games.com/t/terminal-tools/518/10">Thread</a>,
          <a href="https://github.com/876584635678890/876584635678890.github.io">Source</a></td></tr><tr><td>Algo Analizer</td><td><a href="https://forum.c1games.com/u/bcverdict/summary">@bcverdict</a></td><td><a href="https://forum.c1games.com/t/visualizing-elo-growth/753/3">Thread</a>,
          <a href="https://github.com/bcverdict/bcverdict.github.io">Source</a></td></tr><tr><td>Map Maker</td><td><a href="https://forum.c1games.com/u/kevinbai0/summary">@kevinbai0</a></td><td><a href="https://forum.c1games.com/t/map-maker/742">Thread</a>,
          <a href="https://github.com/kevinbai0/terminal-map-maker">Source</a></td></tr><tr><td>API toolkit</td><td><a href="https://forum.c1games.com/u/isaac/summary">@Issac</a></td><td><a href="https://forum.c1games.com/t/using-the-terminal-api/806">Thread</a>,
          <a href="https://github.com/idraper/terminal_svr">Source</a></td></tr><tr><td>Frame info Documentation</td><td><a href="https://forum.c1games.com/u/876584635678890/summary">@8</a></td><td><a href="https://forum.c1games.com/t/frame-info-documentation/727">Thread</a></td></tr></tbody></table></div><div id="Troubleshooting" style="text-align: left;"><h2 id="troubleshooting">Troubleshooting</h2><p>
    If you are still having trouble after trying everything here be sure to checkout the
    <a href="https://forum.c1games.com/" target="_blank">forum</a>. It is likely someone else had a similar issue.
  </p><h4 id="algo-failed-to-compile-">Algo Failed to Compile:</h4><p>Firstly, try clicking the algo on the My Algo page, it won't refresh its compiling status unless you click on it.</p><p>
    Make sure all file and folder names in your project, even inside the zip that you submit, are free of
    spaces and special characters.
  </p><p>
    Your algo may not appear in the dropdown list on the
    <a href="/playground" target="_blank">Playground</a> if it is still
    being prepared for automated play. Try waiting a minute, or re-uploading a zip with
    extraneous files removed.
  </p><h4 id="website-issues-">Website Issues:</h4><p>Make sure you are using chrome and it is updated to the latest version. Unfortunately, only chrome is supported for this build.</p><p>
    If the game board has visual issues, enable hardware acceleration for chrome. It can be enabled in chrome settings by clicking
    <a href="chrome://settings/system" target="_blank">here</a>.
    Then simply click the toggle for
    <span id="rules-highlight">"Use hardware acceleration when available"</span>. Additionally users have reported
    <span id="rules-highlight">disabling hardware acceleration and reenabling</span> it while restarting the browser also helps.
  </p><p>
    Lastly for the above and any other kind of strange behavior found on the website, try refreshing the page. If that doesn't work try
    <span id="rules-highlight">empty cache and hard reload</span>; right click anywhere on the website and click
    <span id="rules-highlight">inspect</span>, ignore the new developer section that opens up. Instead, right click the refresh page icon on the normal url bar next to the back and forward arrow icons and hit
    <span id="rules-highlight">empty cache and hard reload</span>.
  </p><h4 id="game-issues-">Game Issues:</h4><p>
    First make sure to read the
    <a href="https://github.com/correlation-one/C1GamesStarterKit" target="_blank">README.md</a> included in the starterkit viewable on the github page by scrolling down. Additionally make sure to get the latest version of starterkit as your issue may have been solved by a recent update. We also may have updated it with improved documentation and new features.
  </p><p>Below we will list some common errors and how to address them:</p><p><span id="rules-highlight">com.google.gson.JsonSyntaxException</span> or
    <span id="rules-highlight">com.google.gson.Gson.fromJson</span>: This is caused by using the normal
    <span id="rules-highlight">print</span> function instead of using our provided
    <span id="rules-highlight">debug_print</span> function. This causes all sorts of strange behavior including the json error because stdout print statements is how your algo talks to the game engine, instead use our
    <span id="rules-highlight">debug_print</span> function which prints to stderr.
  </p><p><span id="rules-highlight">... has been compiled by a more recent version of the Java Runtime</span> : This means your version of java isn't java 10 or above. Please install a
    <a href="https://www.oracle.com/technetwork/java/javase/downloads/jdk11-downloads-5066655.html" target="_blank">newer version</a>. You may have to restart your computer for the update to take affect. See below if this persists and you are on windows.
  </p><p><span id="rules-highlight">Error: Unable to access jarfile engine.jar</span> or
    <span id="rules-highlight">No such file or directory</span>: You are likely running the run_match script while in the scripts directory. First, try running our new run_match.py script which is directory independent and more flexible in how you call it. If you do want to use an older run_match script your console has to be run in the parent folder that the engine.jar is contained in. Details for how to run the commands correctly are in the
    <a href="https://github.com/correlation-one/C1GamesStarterKit" target="_blank">README.md</a>.
  </p><h4 id="windows-os-issues-">Windows OS Issues:</h4><p>Firstly, make sure you are using powershell not cmd or git bash.</p><p>
    You likely will also have to run
    <span id="rules-highlight">Set-ExecutionPolicy</span> as detailed in the
    <a href="https://github.com/correlation-one/C1GamesStarterKit" target="_blank">README.md</a>.
  </p><p><span id="rules-highlight">... has been compiled by a more recent version of the Java Runtime</span> or
    <span id="rules-highlight">java is not recognized as an internal or external command...</span>: If after installing java as described above you still get this error you likely have to update your windows PATH variable
    <a href="https://docs.oracle.com/en/java/javase/11/install/installation-jdk-microsoft-windows-platforms.html#GUID-96EB3876-8C7A-4A25-9F3A-A2983FEC016A" target="_blank">which you can see how to do here</a>. For example, we had to add C:\Program Files\Java\jdk-11.0.1\bin to the PATH variable using the windows interface (command line changes to PATH didn't stick but doing it through control panel did).
  </p><p><span id="rules-highlight">Split-Path : Cannot bind argument to parameter ‘Path’ because it is null</span> : Your powershell may be out of date which is likely if you are using a windows version before windows 10. See the
    <b><a href="#GameplayOverview">requirements section for details</a></b> on how to update your powershell.
  </p><p><span id="rules-highlight">The term ‘py’ is not recognized as the name of a cmdlet, function, script file, or operable program.</span> : Make sure you have python 3.7 installed and not python 2 or an older version. Also make sure during installation that you set the option to add it to the PATH variable and install for all users. Lastly, after installing restart your powershell.
  </p><h4 id="permission-issues-">Permission Issues:</h4><p>
    If you are having issues relating to permissions, your machine may be automatically disabling execute permissions on the scripts in the scripts folder. On a Unix machine, you can use ls -la to check the
    <a href="https://en.wikipedia.org/wiki/File_system_permissions">permissions</a> on your files, and
    <a href="https://en.wikipedia.org/wiki/Chmod">chmod</a> to add execute permissions. Similar commands exist in windows powershell. The README in the starterkit provides more information and tips related to our scripts.
  </p></div><div id="Glossary" style="text-align: left;"><h2 id="glossary">Glossary</h2><table><thead><tr><th></th><th>Description</th></tr></thead><tbody><tr><td>Attack</td><td>An attack will reduce the health of a Unit equal to the attacker's damage</td></tr><tr><td>Bits</td><td>Currency for placing Information units on the board</td></tr><tr><td>Cores</td><td>Currency for placing Firewall on the board</td></tr><tr><td>Destructor</td><td>Firewall which attacks enemy Information Units</td></tr><tr><td>EMP</td><td>An expensive and easily destroyed Unit. Has high damage and far range. Can wreak havoc on enemy defenses if properly used.</td></tr><tr><td>Encryptor</td><td>Firewall which provides additional health to friendly Information units</td></tr><tr><td>Firewall</td><td>Stationary units that do not move. They block the paths of both friendly and enemy Information units. No two Firewall can occupy the same location.</td></tr><tr><td>Filter</td><td>A cheap, simple Firewall used to influence a Unit’s path and protect more valuable Firewall</td></tr><tr><td>Health (Player)</td><td>For every Information Unit that reaches the opponent’s edge, the health of the opponent is decreased by one.</td></tr><tr><td>Information Unit</td><td>Units which move across the board to the opponent’s edge. Multiple Information Units can occupy the same location.</td></tr><tr><td>Scrambler</td><td>A high-health unit that deals high damage to enemy Information Units, but cannot attack enemy Firewall</td></tr><tr><td>Ping</td><td>A fast-moving unit which deals light damage.</td></tr><tr><td>Health (Unit)</td><td>Health of an Unit. If it is reduced to zero, the unit is destroyed and removed from the arena.</td></tr></tbody></table></div></div></div></div>