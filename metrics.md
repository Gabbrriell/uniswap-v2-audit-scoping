
[<img width="200" alt="get in touch with Consensys Diligence" src="https://user-images.githubusercontent.com/2865694/56826101-91dcf380-685b-11e9-937c-af49c2510aa0.png">](https://consensys.io/diligence)<br/>
<sup>
[[  🌐  ](https://consensys.io/diligence)  [  📩  ](mailto:diligence@consensys.net)  [  🔥  ](https://consensys.io/diligence/tools/)]
</sup><br/><br/>



# Solidity Metrics for 'CLI'

## Table of contents

- [Scope](#t-scope)
    - [Source Units in Scope](#t-source-Units-in-Scope)
        - [Deployable Logic Contracts](#t-deployable-contracts)
    - [Out of Scope](#t-out-of-scope)
        - [Excluded Source Units](#t-out-of-scope-excluded-source-units)
        - [Duplicate Source Units](#t-out-of-scope-duplicate-source-units)
        - [Doppelganger Contracts](#t-out-of-scope-doppelganger-contracts)
- [Report Overview](#t-report)
    - [Risk Summary](#t-risk)
    - [Source Lines](#t-source-lines)
    - [Inline Documentation](#t-inline-documentation)
    - [Components](#t-components)
    - [Exposed Functions](#t-exposed-functions)
    - [StateVariables](#t-statevariables)
    - [Capabilities](#t-capabilities)
    - [Dependencies](#t-package-imports)
    - [Totals](#t-totals)

## <span id=t-scope>Scope</span>

This section lists files that are in scope for the metrics report. 

- **Project:** `'CLI'`
- **Included Files:** 
    - ``
- **Excluded Paths:** 
    - ``
- **File Limit:** `undefined`
    - **Exclude File list Limit:** `undefined`

- **Workspace Repository:** `unknown` (`undefined`@`undefined`)

### <span id=t-source-Units-in-Scope>Source Units in Scope</span>

Source Units Analyzed: **`6`**<br>
Source Units in Scope: **`6`** (**100%**)

| Type | File   | Logic Contracts | Interfaces | Lines | nLines | nSLOC | Comment Lines | Complex. Score | Capabilities |
| ---- | ------ | --------------- | ---------- | ----- | ------ | ----- | ------------- | -------------- | ------------ | 
| 📝 | contracts\UniswapV2ERC20.sol | 1 | **** | 94 | 94 | 79 | 1 | 61 | **<abbr title='Uses Assembly'>🖥</abbr><abbr title='Uses Hash-Functions'>🧮</abbr><abbr title='Handles Signatures: ecrecover'>🔖</abbr>** |
| 📝 | contracts\UniswapV2Factory.sol | 1 | **** | 49 | 49 | 40 | 2 | 46 | **<abbr title='Uses Assembly'>🖥</abbr><abbr title='Uses Hash-Functions'>🧮</abbr><abbr title='create/create2'>🌀</abbr>** |
| 📝 | contracts\UniswapV2Pair.sol | 1 | **** | 201 | 201 | 167 | 34 | 184 | **<abbr title='Uses Hash-Functions'>🧮</abbr>** |
| 📚 | contracts\libraries\Math.sol | 1 | **** | 23 | 23 | 18 | 2 | 5 | **** |
| 📚 | contracts\libraries\SafeMath.sol | 1 | **** | 17 | 17 | 12 | 1 | 4 | **** |
| 📚 | contracts\libraries\UQ112x112.sol | 1 | **** | 20 | 20 | 10 | 6 | 4 | **** |
| 📝📚 | **Totals** | **6** | **** | **404**  | **404** | **326** | **46** | **304** | **<abbr title='Uses Assembly'>🖥</abbr><abbr title='Uses Hash-Functions'>🧮</abbr><abbr title='Handles Signatures: ecrecover'>🔖</abbr><abbr title='create/create2'>🌀</abbr>** |

<sub>
Legend: <a onclick="toggleVisibility('table-legend', this)">[➕]</a>
<div id="table-legend" style="display:none">

<ul>
<li> <b>Lines</b>: total lines of the source unit </li>
<li> <b>nLines</b>: normalized lines of the source unit (e.g. normalizes functions spanning multiple lines) </li>
<li> <b>nSLOC</b>: normalized source lines of code (only source-code lines; no comments, no blank lines) </li>
<li> <b>Comment Lines</b>: lines containing single or block comments </li>
<li> <b>Complexity Score</b>: a custom complexity score derived from code statements that are known to introduce code complexity (branches, loops, calls, external interfaces, ...) </li>
</ul>

</div>
</sub>


##### <span id=t-deployable-contracts>Deployable Logic Contracts</span>
Total: 2
* 📝 `UniswapV2Factory`
* 📝 `UniswapV2Pair`



#### <span id=t-out-of-scope>Out of Scope</span>

##### <span id=t-out-of-scope-excluded-source-units>Excluded Source Units</span>

Source Units Excluded: **`0`**

<a onclick="toggleVisibility('excluded-files', this)">[➕]</a>
<div id="excluded-files" style="display:none">
| File   |
| ------ |
| None |

</div>


##### <span id=t-out-of-scope-duplicate-source-units>Duplicate Source Units</span>

Duplicate Source Units Excluded: **`0`** 

<a onclick="toggleVisibility('duplicate-files', this)">[➕]</a>
<div id="duplicate-files" style="display:none">
| File   |
| ------ |
| None |

</div>

##### <span id=t-out-of-scope-doppelganger-contracts>Doppelganger Contracts</span>

Doppelganger Contracts: **`0`** 

<a onclick="toggleVisibility('doppelganger-contracts', this)">[➕]</a>
<div id="doppelganger-contracts" style="display:none">
| File   | Contract | Doppelganger | 
| ------ | -------- | ------------ |


</div>


## <span id=t-report>Report</span>

### Overview

The analysis finished with **`0`** errors and **`0`** duplicate files.





#### <span id=t-risk>Risk</span>

<div class="wrapper" style="max-width: 512px; margin: auto">
			<canvas id="chart-risk-summary"></canvas>
</div>

#### <span id=t-source-lines>Source Lines (sloc vs. nsloc)</span>

<div class="wrapper" style="max-width: 512px; margin: auto">
    <canvas id="chart-nsloc-total"></canvas>
</div>

#### <span id=t-inline-documentation>Inline Documentation</span>

- **Comment-to-Source Ratio:** On average there are`7.09` code lines per comment (lower=better).
- **ToDo's:** `0` 

#### <span id=t-components>Components</span>

| 📝Contracts   | 📚Libraries | 🔍Interfaces | 🎨Abstract |
| ------------- | ----------- | ------------ | ---------- |
| 3 | 3  | 0  | 0 |

#### <span id=t-exposed-functions>Exposed Functions</span>

This section lists functions that are explicitly declared public or payable. Please note that getter methods for public stateVars are not included.  

| 🌐Public   | 💰Payable |
| ---------- | --------- |
| 18 | 0  | 

| External   | Internal | Private | Pure | View |
| ---------- | -------- | ------- | ---- | ---- |
| 14 | 32  | 5 | 7 | 2 |

#### <span id=t-statevariables>StateVariables</span>

| Total      | 🌐Public  |
| ---------- | --------- |
| 26  | 20 |

#### <span id=t-capabilities>Capabilities</span>

| Solidity Versions observed | 🧪 Experimental Features | 💰 Can Receive Funds | 🖥 Uses Assembly | 💣 Has Destroyable Contracts | 
| -------------------------- | ------------------------ | -------------------- | ---------------- | ---------------------------- |
| `=0.5.16` |  | **** | `yes` <br/>(2 asm blocks) | **** | 

| 📤 Transfers ETH | ⚡ Low-Level Calls | 👥 DelegateCall | 🧮 Uses Hash Functions | 🔖 ECRecover | 🌀 New/Create/Create2 |
| ---------------- | ----------------- | --------------- | ---------------------- | ------------ | --------------------- |
| **** | **** | **** | `yes` | `yes` | `yes`<br>→ `AssemblyCall:Name:create2` | 

| ♻️ TryCatch | Σ Unchecked |
| ---------- | ----------- |
| **** | **** |

#### <span id=t-package-imports>Dependencies / External Imports</span>

| Dependency / Import Path | Count  | 
| ------------------------ | ------ |


#### <span id=t-totals>Totals</span>

##### Summary

<div class="wrapper" style="max-width: 90%; margin: auto">
    <canvas id="chart-num-bar"></canvas>
</div>

##### AST Node Statistics

###### Function Calls

<div class="wrapper" style="max-width: 90%; margin: auto">
    <canvas id="chart-num-bar-ast-funccalls"></canvas>
</div>

###### Assembly Calls

<div class="wrapper" style="max-width: 90%; margin: auto">
    <canvas id="chart-num-bar-ast-asmcalls"></canvas>
</div>

###### AST Total

<div class="wrapper" style="max-width: 90%; margin: auto">
    <canvas id="chart-num-bar-ast"></canvas>
</div>

##### Inheritance Graph

<a onclick="toggleVisibility('surya-inherit', this)">[➕]</a>
<div id="surya-inherit" style="display:none">
<div class="wrapper" style="max-width: 512px; margin: auto">
    <div id="surya-inheritance" style="text-align: center;"></div> 
</div>
</div>

##### CallGraph

<a onclick="toggleVisibility('surya-call', this)">[➕]</a>
<div id="surya-call" style="display:none">
<div class="wrapper" style="max-width: 512px; margin: auto">
    <div id="surya-callgraph" style="text-align: center;"></div>
</div>
</div>

###### Contract Summary

<a onclick="toggleVisibility('surya-mdreport', this)">[➕]</a>
<div id="surya-mdreport" style="display:none">
 

 Files Description Table


|  File Name  |  SHA-1 Hash  |
|-------------|--------------|
| contracts\UniswapV2ERC20.sol | 43899aa9ba2a46788825a3e90e9d8635ed84de94 |
| contracts\UniswapV2Factory.sol | e23a923205bbe0766721393232a68cd01eb75ed4 |
| contracts\UniswapV2Pair.sol | a9af70edbee09b22ee91e5690761baa1f83a2ef6 |
| contracts\libraries\Math.sol | 1348a437cf092bb525e65d5b825ce19e5024ca26 |
| contracts\libraries\SafeMath.sol | 074e21997d7ba23f6fc85ae4fe265dafc884f188 |
| contracts\libraries\UQ112x112.sol | cbb25b70152d23f5845542403004f2cccb992c29 |


 Contracts Description Table


|  Contract  |         Type        |       Bases      |                  |                 |
|:----------:|:-------------------:|:----------------:|:----------------:|:---------------:|
|     └      |  **Function Name**  |  **Visibility**  |  **Mutability**  |  **Modifiers**  |
||||||
| **UniswapV2ERC20** | Implementation | IUniswapV2ERC20 |||
| └ | <Constructor> | Public ❗️ | 🛑  |NO❗️ |
| └ | _mint | Internal 🔒 | 🛑  | |
| └ | _burn | Internal 🔒 | 🛑  | |
| └ | _approve | Private 🔐 | 🛑  | |
| └ | _transfer | Private 🔐 | 🛑  | |
| └ | approve | External ❗️ | 🛑  |NO❗️ |
| └ | transfer | External ❗️ | 🛑  |NO❗️ |
| └ | transferFrom | External ❗️ | 🛑  |NO❗️ |
| └ | permit | External ❗️ | 🛑  |NO❗️ |
||||||
| **UniswapV2Factory** | Implementation | IUniswapV2Factory |||
| └ | <Constructor> | Public ❗️ | 🛑  |NO❗️ |
| └ | allPairsLength | External ❗️ |   |NO❗️ |
| └ | createPair | External ❗️ | 🛑  |NO❗️ |
| └ | setFeeTo | External ❗️ | 🛑  |NO❗️ |
| └ | setFeeToSetter | External ❗️ | 🛑  |NO❗️ |
||||||
| **UniswapV2Pair** | Implementation | IUniswapV2Pair, UniswapV2ERC20 |||
| └ | getReserves | Public ❗️ |   |NO❗️ |
| └ | _safeTransfer | Private 🔐 | 🛑  | |
| └ | <Constructor> | Public ❗️ | 🛑  |NO❗️ |
| └ | initialize | External ❗️ | 🛑  |NO❗️ |
| └ | _update | Private 🔐 | 🛑  | |
| └ | _mintFee | Private 🔐 | 🛑  | |
| └ | mint | External ❗️ | 🛑  | lock |
| └ | burn | External ❗️ | 🛑  | lock |
| └ | swap | External ❗️ | 🛑  | lock |
| └ | skim | External ❗️ | 🛑  | lock |
| └ | sync | External ❗️ | 🛑  | lock |
||||||
| **Math** | Library |  |||
| └ | min | Internal 🔒 |   | |
| └ | sqrt | Internal 🔒 |   | |
||||||
| **SafeMath** | Library |  |||
| └ | add | Internal 🔒 |   | |
| └ | sub | Internal 🔒 |   | |
| └ | mul | Internal 🔒 |   | |
||||||
| **UQ112x112** | Library |  |||
| └ | encode | Internal 🔒 |   | |
| └ | uqdiv | Internal 🔒 |   | |


 Legend

|  Symbol  |  Meaning  |
|:--------:|-----------|
|    🛑    | Function can modify state |
|    💵    | Function is payable |
 

</div>
____
<sub>
Thinking about smart contract security? We can provide training, ongoing advice, and smart contract auditing. [Contact us](https://consensys.io/diligence/contact/).
</sub>


