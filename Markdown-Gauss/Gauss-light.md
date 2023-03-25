









<center> <font size=8 ><b>Markdown 主题</b></font></center> 





[toc]



# Session 1: Introduction of Liquidity Risk



## 1 Liquidity Risk And Leverage



### 1.1 Introduction to liquidity risk



**Tasks:**

- Explain and calculate liquidity trading risk via cost of liquidation and liquidity-adjusted VaR (LVaR)

- Identify liquidity funding risk, funding sources, and lessons learned from real cases: Northern Rock, Ashanti Goldfields, and Metallgesellschaft

- Distinguish methods to measure and manage funding liquidity risk and transactions liquidity risk
- Summarize the asset-liability management process at a fractional reserve bank, including the process of liquidity transformation



**Introduction**

- **Solvency vs liquidity** 偿债能力
  - **Solvency**: ==assets more than liabilities== (equity is positive)
  - **Liquidity**: ability of a company to make cash payments as they become due

- **Two type of liquidity**
  - **Transaction liquidity:** an asset is easy to exchange for other assets
  - **Funding liquidity:** is the ability to finance assets continuously at an acceptable borrowing rate



**Sources of liquidity risk**

- **Transaction liquidity risk:** the risk of ==moving the price of an asset adversely== in the act of buying or selling it (**a.k.a Market liquidity risk or trading liquidity risk**)
  - ==Transaction liquidity risk is low== if assets can be liquidated quickly, cheaply, and without moving the price too much 快速、公允

- **Funding liquidity risk**: the risk that creditors either ==withdraw credit or change the terms==, (**aka Balance sheet risk**)
  - Borrower's credit quality is or perceived to be deteriorating and borrower's financial conditions are deteriorating
- **Systemic risk:** the risk of a ==general impairment== of the financial system
  - In situations of severe financial stress, the ability of the financial system to allocate credit, support markets in financial assets, and even administer payments and settle financial transactions may be impaired

- These types of liquidity risk ==interact==
  - **Funding liquidity risk increases transaction liquidity risk:** If collateral requirements or the cost of financing increase, the trader may have to unwind securities
  - **Transaction liquidity risk increases funding liquidity risk**: If a leveraged market participant have illiquid assets on its books, its funding will be in greater jeopardy
  - **Systemic risk increases transaction and funding liquidity risk**



**Measuring market liquidity**

- Financial institutions can sell the asset at the **bid** to market maker and buy at the **offer** from market maker
  - The market maker is likely to **increase** the bid-offer spread above a certain size

- For ==an asset==, one measure of the market liquidity is its bid ==offer spread==
  - **Dollar amount: p** = Offer price - Bid price
  - **Proportational spread: s** = $\frac{Offer \ price - Bid \ price}{Mid \ market \ price}$



> **Example**
>
> - Suppose a dealer quoted the bid price and the offer price for a particular bond at 98 and 102 dollars, respectively Calculate the dollar amount spread(p) and proportional spread(s)
>
> **Answer:**
>
> - $p = Offer \ price  -Bid \ price = 102 - 98 - 4$
> - $Mid \ price = \frac{offer \ price + bid \ price}{ 2} = \frac{102+98}{2} = 100$
> - $s = \frac{offer \ price - Bid \ price}{Mid \ market \ price} = \frac{4}{100} = 4\%$
>
> |      Portfolio      | Bond A | Bond B |
> | :-----------------: | :----: | :----: |
> |    Market value     | 40000  | 46000  |
> | Proportional spread |  10%   |  20%   |



- For a book, measure of market liqudity is ==**cost of liquidation**==

  - In ==normal market== conditions

  $$
  Cost \ of \ liquidation. =\sum_{i=1}^n \frac{1}{2} s_i \alpha_i
  $$

  $s_i$: proportional spread 

  $\alpha_i$: is the dollar value(=mid-price $\times$ volume) of the position

  - In ==stressed market== conditions:

  $$
  Cost \ of \ liquidation = \sum_{i=1}^n \frac{1}{2} (\mu_i +\lambda \sigma_i ) \alpha_i
  $$

  $\mu_i$: mean of proportional spread  

  $\sigma_i$: standard deviation of proportional spread 

  $\lambda$: critical value under certain confidence level



> **Example**
>
> - Tom's portfolio has two bond positions The related information is shown in the table What is the cost of liquidation of the whole portfolio in normal market?
>
> |      Portfolio      | Bond A | Bond B |
> | :-----------------: | :----: | :----: |
> |    Market value     | 40000  | 46000  |
> | Proportional spread |  10%   |  20%   |

> **Answer：**
>
> - Cost of liquidation of the whole portfolio = $\sum_{i=1}^n \frac{1}{2} s_i \alpha_i = \frac{1}{2} \times 10\% \times 40000 + \frac{1}{2} \times 20\% \times 46000 = 6600$
>
> 
>
> **Example**
>
> - Given the following extra information, what is the cost of liquidation of the whole portfolio in stressed market with confidence level of 99%?
>
> |                 Portfolio                 | Bond A | Bond B |
> | :---------------------------------------: | :----: | :----: |
> |               Market value                | 40000  | 46000  |
> |          Mean of spread($\mu_i$)          |  10%   |  20%   |
> | Standard deviation of spread ($\sigma_i$) |   6%   |   8%   |

> **Answer**
> $$
> Cost \ of \ liquidation \ of \ the \ whole \ portfolio = \sum_{i=1}^n \frac{1}{2} (\mu_i + \lambda \sigma_i) \alpha_i \\ = \frac{1}{2} \times (10\% + 2.33 \times 6\%) \times 40000+ \frac{1}{2} \times (20\% +2.33 \times 8\%) \times 46000 = 13683
> $$
> 99%:2.326  95%:1.645



- **Liquidity-adjusted VaR** is regular VaR plus the cost of liquidation

  - In ==normal market==
    $$
    Liquidity-adjusted \ VaR = VaR + \sum_{i=1}^n \frac{1}{2} s_i \alpha_i
    $$

  - In ==stressed market (assuming spread is normal distribution):==

  $$
  Liquidity - adjusted \ VaR = VaR + \sum_{i=1}^n \frac{1}{2} (\mu_i + \lambda \sigma_i) \alpha_i
  $$

```python
@decorator(param=1)
def f(x):
    """
    Syntax Highlighting Demo
    @param x Parameter

    语义高亮显示:
    生成的光谱为局部变量和参数选择颜色:
     Color#1 SC1.1 SC1.2 SC1.3 SC1.4 Color#2 SC2.1 SC2.2 SC2.3 SC2.4 Color#3
     Color#3 SC3.1 SC3.2 SC3.3 SC3.4 Color#4 SC4.1 SC4.2 SC4.3 SC4.4 Color#5
    """

    def nested_func(y):
        print(y + 1)

    s = ("Test", 2+3, {'a': 'b'}, f'{x!s:{"^10"}}')   # Comment
    f(s[0].lower())
    nested_func(42)

class Foo:
    tags: List[str]

    def __init__(self: Foo):
        byte_string: bytes = b'newline:\n also newline:\x0a'
        text_string = u"Cyrillic Я is \u042f. Oops: \u042g"
        self.make_sense(whatever=1)
    
    def make_sense(self, whatever):
        self.sense = whatever

x = len('abc')
print(f.__doc__)
```




> **Example**
>
> - Suppose a one-day VaR of the stock position is 23,000 dollars and cost of liquidation of the position in normal market and stressed market are 6,600 and 13,683, respectively Calculate the liquidity adjusted VaR in two markets conditions

> **Answer:**
>
> - In normal market: $Liquidity-adjusted \ VaR =    VaR + \sum_{i=1}^n \frac{1}{2} s_i \alpha_i = 23000 + 6600 = 29600 $
> - In stressed market: $liqudity - adjusted \ VaR = VaR+\sum_{i=1}^n \frac{1}{2} (\mu_i + \lambda \sigma_i)  = 23000+13686 =36683$

- **VaR translation considering market liquidity：**

  -  According to previews knowledge

  $$
  T-day \ VaR = \sqrt{T} \times VaR_{1-day}
  $$

  - **Avoid adverse price impact,** the portfolio position equally decreasing every day：

  $$
  Adjusted \ T-day \ VaR = \sqrt{\frac{(1+T)(1+2T)}{6T}} \times VaR_{1-day}
  $$


> **Example**
>
> - Suppose a one-day VaR of the stock position is 23,000 dollars To avoid adverse price impact, the fund manager plans to liquidate the position in 10 days What is the adjusted 10-day VaR?
>
> **Answer**
> $$
> Adjusted \ 10-day \ VaR =  \sqrt{\frac{(1+T)(1+2T)}{6T}} \times VaR_{1-day} \\ = \sqrt{\frac{(1+10)(1+2\times 10)}{6 \times 10}} \times 23000 = 45129.26
> $$



**Funding liquidity risk**

- Funding liquidity risk is the financial institution's ability to **meet its cash needs** as they arise
  - The core function of a commercial bank is to take deposits and provide loans In doing so, it carries out a ==**liquidity**== and ==**maturity**==, as well as ==**credit transformation**== 相当于两个客户的信用转换成了银行的信用，也是流动性的转换

- **Maturity mismatch leads to funding liquidity risk**: Funding liquidity risk arises for market participants who borrow at short term to finance investments that require a longer time to become profitable

- To **manage** funding liquidity risk, bank using asset liability management(ALM)资产负债管理
  - Tracking and forecasting available cash and sources of funding on the one hand, and cash needs on the other
  - Keeping certain ratios of ready cash and readily marketable securities to meet unusual demands by depositors and other short-term lenders for the return of their money

- Financial institutions that are solvent (iez have positive equity) and sometimes fail because of liquidity problems
  - Northern Rock
  - Ashanti Goldfields
  - Metallgesellschaft



**Case of Northern Rock** 即使资产大于负债，也会因为流动性风险破产

- **Case brief**: Northern Rock was a fast-growing medium-sized mortgage bank based in the United Kingdom The bank relied on selling ==short-term debt instruments== for funding Following the ==subprime crisis==, the bank found it ==difficult to roll over the debt even though the bank was solvent==. In November 2011, Northern Rock pic was bought from the British government for £747 million by the Virgin Group

- **Lessons:** Liquidity can lead to serious problems even if the bank is solvent



**Case of Ashanti Goldfields**

- **Case brief: **Ashanti Goldfields had sought to protect its shareholders from gold price declines by ==selling gold forward==. On September 26,1999,15 European central banks announced that they would limit their gold sales over the following 5 years. The price of gold ==jumped up== over 25% Ashanti Goldfields was ==unable to meet margin calls== and this resulted in a major restructuring

- **Lessons:** Liquidity problems can arise when hedging illiquid assets with contracts that are subject to margin requirements



**Case of Metallgesellschaft**

- **Case brief:** Metallgesellschaft sold a huge volume of 5 to 10 year heating oil and gasoline **fixed-price supply** contracts to its customers at six to eight cents above market prices It hedged its exposure with **long positions in futures** As it turned out, ==the price of oil fell== and there were ==margin calls== on the futures positions The outcome was a loss to MG of **$133 billion**

- **Lessons:** Liquidity problems can arise when hedging illiquid assets with contracts that are subject to margin requirements



### 1.2 Liquidity challenges



**Tasks:**

- Describe specific challenges faced by different types of financial institutions in managing liquidity risk

- Evaluate Basel III liquidity risk ratios and BIS principles for sound liquidity risk management

- Explain liquidity black holes and Identify the causes of positive feedback trading




**Challenges faced by different institutions**

- **Commercial banks:**

  - Bank run:挤兑 due to fractional-reserve, if depositors are concerned about banks' liquidity, they will endeavor to redeem before other depositors and lenders

- **Security firms:** 证券公司，需要做一些融资，对一些债券库存

  - Lenders abruptly withdrawing credit 
  - Brokerage and clearing customers withdrawing deposits

- **Money Market Mutual Funds (MMMF):** 货币共同基金

  - Sometimes MMMF had to liquidate assets with loss to meet huge redemption
    - **Break the buck phenomenon** 跌破了

- **Hedge funds:**

  - Hedge fund capital that can be redeemed does not only include which will be expected to experience large losses, but also those profitable or having low losses hedge funds

    - No access to wholesale funding and rely on other tools

      

**Sources of Liquidity**

- Holdings of cash and Treasury securities

- The ability to liquidate trading book positions 交易账户的头寸，banking book是要持有到期的

- The ability to borrow money at short notice

- The ability to offer favorable terms to attract retail and wholesale deposits at short notice

- The ability to securitize assets (such as loans) at short notice

- Borrowings from the central bank



**Regulations**

- Basel III introduced two liquidity risk requirements: the **liquidity coverage ratio **(LCR) and the **net stable funding ratio** (NSFR) 

  - $LCR: \frac{High\ quality \ liquid \ assets}{ Net \ cash \ outflows \ in \ a \ 30-day \ period} \geq 100\%$
  - $NSFR: \frac{Available \ Amount \ of \ stable \ funding}{Required \ amount \ of \ stable \ funding} \geq 100\%$

- BIS issued 17 principles for sound liquidity risk management

  - Identify the responsibilities, procedures, policies, strategies, information disclosure, supervision etc

    

**Liquidity black holes**

- A liquidity black hole describes a situation where liquidity has ==dried up== in a particular market because ==everyone wants to do the same type of trade at the same time.== It is sometimes also referred to as a "**crowded exit"** 

  - **During the sell-oft liquidity dries up:** A liquidity black hole is created when a price decline causes more market participants to want to sell, driving prices well below where they will eventually settle

    

**Positive and negative feedback traders**

- Negative feedback traders ==buy when prices fall== and ==sell when prices rise== 负反馈交易

- Positive feedback traders ==sell when prices fall== and ==buy when prices rise==

  - When ==positive feedback traders== dominate the trading, market prices are liable to be ==unstable== and the market may become ==one-sided and illiquid==

    

**Reasons of positive feedback trading**

- Trend trading

- Stop-loss rules

- Dynamic hedging

- Creating options synthetically

- Margins

- Predatory trading

- Relative value fixed income trade





### 1.3 Collateral and Leverage



**Tasks:**

- Compare transactions used in the collateral market and explain risks that can arise through collateral market transactions

- Describe the relationship between leverage and a firm's return profile (including the leverage effect) and distinguish the impact of different types of transactions on a firm's leverage and balance sheet



**Collateral market**

- Collateral has always played an important role in credit transactions by providing security for lenders and thus ensuring the availability of credit to borrowers

- ransactions in collateral market:

  - Margin loans
  - Repurchase agreements
  - Securities lending
  - Total return swaps

- Risks in collateral market transactions:

  - Market risk: price fluctuation; interest rate fluctuation

  - Credit risk: credit quality of the collateral deteriorates

  - Counterparty risk: counterparty may default

    

**Leverage**

- **Leverage ratio** $L = \frac{A}{E} = \frac{D+E}{E}= 1+\frac{D}{E}$

- **Leverage effect** can be seen by writing out the relationship between asset returns $r_A$, equity returns $r_E$, and the cost of debt $r_D$

  - $r_E = r_A +\frac{D}{E} \times (r_A - r_D)$
  - $r_E = L\times r_A - (L-1)\times r_D = r_D + L \times (r_A - r_D)$

- **Effect of increasing leverage** is $\frac{\part r_E}{\part L} = r_A - r_D$

- Leverage ratios can amplify sensitivity to changes in cash flow

- An economic balance sheet is construct to capture the implicit or embedded leverage in loans, options and derivatives It could provide a reasonable answer to the question of how much borrowed to finance positions

  

**Leverage: margin loans**

- Margin lending has a straightforward impact on leverage

- The haircut determines the amount of the loan that is made:
  - At a haircut of h percent: 1 - h is lent against a given market value of margin collateral
  - The leverage on a position with a haircut of h percent is 1/h



**Leverage: short positions**

- Short positions lengthen the balance sheet, since both the value of the borrowed short securities and the cash generated by their sale appear on the balance sheet

- They increase leverage, because both asset and liability increases the same amount with a constant equity
  - $L = \frac{A}{E} = 1+\frac{D}{E}$



**Leverage: derivatives**

- Derivative securities are a means to gain an economic exposure to some asset or risk factor without buying or selling it outright

- If the derivative creates a synthetic long (short) position, the economic balance sheet entries mimic those of a cash long (short) position

- The implicit assets and liabilities created on the economic balance sheet are vis-a-vis the derivatives counterparties

  

**Leverage: structured credit**

- Seniority ranking: Bond tranche  Mezzanine tranche Equity tranche

- The equity tranches get the remaining of the asset pool
  - For example, asset pool is 50m, financed by 5m equity tranche and 45m bond tranche with required return of 6% When actual asset pool's return is 10% (that is 5m): 
    - Bond tranche receives  27m (=45m X 6%) and equity tranche receives the remaining 23m, reaching a return of 46%







# 2. Managing Deposit Services and Non-deposlt Liabilities (Ch12&13)



### 2.1 Deposit Services Introduction



**Tasks:**

- Differentiate between the various transaction and non transaction deposit types

  

**Deposit Services**

- Deposit accounts are the number one source of funds at most banks. Two key issues：
  - Where can funds be raised at lowest possible cost?
  - How can management ensure that the institution always has enough deposits to support lending and other services the public demands?



**Deposit types**

- Main type of deposit services types:
  - **Transaction (payment or demand) deposits: honor any withdrawals** made by the customer **immediately**

- **Non-transaction (savings or thrift) deposits:** Design to attract funds from customers who wish to set aside money for future expenditures or financial emergencies.

**Transaction deposits**

- **Noninterest-bearing transaction (demand) deposits**
  - Do not earn explicit interest but provide the customer with payment service.
  - Deposits are among the most volatile and least predictable, and with shortest potential maturity since they can be withdrawn without prior notice.

- **Interest-bearing transaction deposits** 
  - Pay at least some interest.
  - **Negotiable order of withdrawal (NOW) accounts**
    - Beginning in New England during the 1970s, hybrid checking-savings deposits
    - NOWs are interest-bearing savings deposits that give the offering depository institution prior notice before the customer withdraws funds
    - Held only by individuals and nonprofit institutions
  - **Money market deposit accounts (MMDAs)**
    - Flexible money market interest rates but accessible via check or preauthorized draft to pay for goods and services
      - Up to six preauthorized drafts and three withdrawals be made by writing checks per month
    - Can be held by businesses as well as individuals
  - **Super NOWs**
    - No limitation on the number of checks depositor write
    - Offers institutions post lower yields on SNOWs than on MMDAs
    - Can be held by individuals and nonprofit institutions.

- **Mobile apps**
  - The hottest item in the transaction deposit field today appears to be the mobile check deposit.



**Non-transaction deposits**

- **Passbook saving deposits**
  - Unlimited withdrawal privileges and low interest rate
  - Tend to be stable with little sensitivity to changes in interest rates 
  - Individuals, nonprofit organizations, governments, and business firms can hold savings deposits, but in the United States businesses could not place more than 150,000 in such a deposit

- **Time deposits**
  - Provide to wealthier depositors with fixed maturity dates and fixed or sometimes fluctuating rates
  - Must carry a minimum maturity of 7 days
  - Most popular of all time deposits is certificates of deposits (CDs), which can be issued in negotiable form (NCD) and nonnegotiable form

- **Retirement savings deposits**
  - Wage earners and salaried individuals are granted the right to make limited contributions each year, tax free, to an **individual retirement account (IRA)**
  - Self-employed persons, **Keogh plan retirement account** is available.
  - Both IRAs and Keoghs are **highly stable** and carries **fixed interest rate**, which are great appeal for managers of depository institutions







### 2.2 Deposits Pricing Methods



**Tasks:**

- Compare the different methods used to determine the pricing of deposits and calculate the price of a deposit account using cost-plus, marginal cost, and conditional pricing formulas
- Explain challenges faced by banks that offer deposit accounts, including deposit insurance, disclosures, overdraft protection, and basic (lifeline) banking.



**Pricing Deposits**

- An important issue remains: How should depository institutions price their deposit and deposit services in order to attract new funds and make a profit?

  - It needs to pay a high enough interest return to attract customer funds but must avoid paying an interest rate so costly that it erodes any potential profit margin

    

**Deposits and Deposit Services Pricing Methods**

- Marginal Cost

- Cost plus profit margin

- Conditional Pricing

- Relationship pricing

  

**Deposits Pricing Methods**

- **Marginal Cost**

  - **Definition:** the added cost of bringing in new funds

    - Compare the marginal cost rate to the expected additional revenue (marginal revenue) to decide the interest rate

  - **Formular**: Marginal cost rate = $\frac{Change \ in \ total \ cost}{Additional \ Funds \ raised}$

    - Change in total cost (Marginal cost) = New interest rate $\times$ Total funds raised at new rate - Old interest rate $\times$ Total funds raised at old rate

      



**Example**

- New Day Bank plans to launch a new deposit campaign next week in hopes of bringing in from 100 million to 600 million new deposit, which it expects to invest at a 4.25 percent yield. The flowing chart is the cost for attracting new deposits

  | New Deposits (in millions) | 100  | 200   | 300  | 400   | 500  | 600   |
  | :------------------------: | ---- | ----- | ---- | ----- | ---- | ----- |
  |       Interest cost        | 2%   | 2.25% | 2.5% | 2.75% | 3%   | 3.25% |

   What interest rate should the institution set to ensure that profit is maximized?

- **Answer**: Marginal Cost rate = $\frac{Change \ in \ total \ cost}{Addtional \ funds \ raised}$





- The institution should set deposit interest rate at 3% to ensure that marginal cost does not exceed marginal revenue





**Deposit Services Pricing Methods** 

- **Cost plus profit margin**

  - Each deposit service may be priced high enough to recover all or most of the cost of providing that service 

  - **Calculate formula:**

    Unit price charged the customer for each deposit service 

    =Operating expense per unit of deposit service 

    +Estimated overhead expense allocated to deposit service 

    +Planned profit margin from each service unit sold

**Example**

- G&F Savings Bank finds that its basic transaction account, which requires a 1000 minimum balance, costs an average of 3.25 per month in servicing costs (including labor and computer expense) and 1.25 per month in overhead expenses. The bank also tries to gain a 0.50 per month profit margin on these accounts. What monthly fee should the bank charge each customer?

- Answer:
  - $3.25+1.25 +0.5 = 5$



- **Conditional Pricing**
  - The customer pays a low fee or no fee if the deposit balance remains above some minimum level but faces a higher fee otherwise
  - Varies among deposits based on one or more factors as follows: 
    - The number of transactions 
    - The average balance 
    - The maturity of the deposit
  - **Flat-rate pricing**
    - The depositor's cost is a fixed charge per check, per time period, or both.
  - **Free pricing**
    - No monthly account maintenance fee or per-transaction charge
    - Unprofitable for institutions because it tends to attract many small, active deposits when market rate is high
  - **Conditionally free pricing**
    - Favors large-denomination deposits because services are free if the account balance stays above some minimum figure
  - **Relationship pricing**
    - Promotes greater customer loyalty and makes the customer less sensitive to the prices posted on services offered by competing financial firms



**Conditionally free pricing Example**





- **Deposit insurance**
  - The Federal Deposit Insurance Corporation (FDIC) provides deposit protection for its membership
  - U.S. government securities, shares in mutual funds, safe deposit boxes, and funds stolen from an insured depository institution are not covered by FDIC
  - The amount of insurance premiums each FDIC-insured depository institution must pay is determined by the volume of deposits and the degree of risk exposure

- **Disclosure of deposit service**
  - Advertising of deposit terms may not be misleading
  - Deposit rates must be quoted as annual percentage yields(APY)
  - The dates and minimum balance required must be explicit
  - The depositor must be warned of penalties or fees that could reduce the yield



**Overdraft protection**

- This service makes sure that clients' incoming checks and draft are paid and clients avoid excessive NSF (not sufficient funds) fees

- It is an important source of income for financial-service provider

- Faced with adverse public and regulators' comments, some financial firms have reduced or eliminated their overdraft fees

- This is a service that has remained popular because this service can make sure their important bills



**Basic (Lifeline) Banking**

- Most financial-service providers are privately owned corporations and responsible to their shareholders to earn competitive returns. Low price cannot cover cost.

- The issue of lifeline banking may not be that simple because entry into the banking industry is regulated.

- How to decide which customers access to low-price services?

- Who should bear the cost of lifeline services?

- Should those benefit from government aid be responsible to offer service to all?







### 2.3 Non-deposit Liabilities Sources



**Tasks:**

- Distinguish between the various sources of non-deposit liabilities at a bank

  

**Sources of Non-deposit Liabilities**

- When deposit is inadequate to support loans and investment, financial institutions need non-deposit liabilities:

  - Federal Funds Market

  - Borrowing from Federal Reserve Banks

  - Advances from Federal Home Loan Banks

  - The large Negotiable CDs

  - The Eurocurrency Deposit Market

  - Commercial Paper market

  - Repurchase Agreements

  - Long-term non-deposit funds

    

- **Federal Funds Market (ZFed Funds"):** Consist exclusively of deposits held at the Federal Reserve banks and can be transferred through Fedwire

  - Meet legal reserve requirements and satisfy loan demand  
  - Large banks play a role similar to funds brokers
  - Short-term borrowings:
    - **Overnight loans**: usually no collateral
    - **Term loans:** longer-term Fed loans contract
    - **Continuing contract: **automatically renewed each day

- **Borrowing from Federal Reserve Banks**: Fed will make the loan through its discount window by crediting the borrower's reserve account. The loan must be backed by acceptable collaterals

  - **Primary credit**: short terms(overnight to 90 days), a higher interest rate than Fed funds interest rate
  - **Secondary credit**: depository institutions not qualifying for primary credit, a higher interest rate than primary credit
  - **Seasonal credit**: longer periods than primary credit, for small and medium-sized institutions experiencing seasonal swings

- **Advances from Federal Home Loan Banks (FHLB)**

  - Allows troubled institutions to use the home mortgages as collateral for emergency loans from FHLB
  - A stable source of funding at below-market interest rates
  - Ranges from overnight to more than 20 years
    - Improves the liquidity of home mortgages
    - Encourages more lenders to provide credit to the housing market

- **The large Negotiable CDs**

  - **A hybrid account**: a deposit or another form of IOU
    - Domestic CDs, Dollar-denominated CDs, Yankee CDs, Thrift CDs
  - **Short maturity:** range from 7 days to 1 or 2 years but concentrated in the 1- to 6-month
  - Amount due CDs customer = Principal + Principal $\times$ $\frac{Days \ to  \ maturity}{360 \ days} \ \times$ Annual rate of interest

- **The Eurocurrency Deposit Market**

  - A domestic financial firm can tap the Euromarkets for funds by contacting one of the major international banks that borrow and lend Eurocurrencies every day
    - The largest U.S. bank use their own overseas branches tap the market.

- **Commercial Paper market**

  - **Short-term notes**: well-known companies issue to raise working capital. 3 or 4 days to 9 months, sell at a discount
    - **Industrial paper: **issued by nonfinancial companies
      - A substantial portion of commercial paper.
    - **Financial paper:** issued by finance companies.

- **Repurchase Agreements**

  - Less popular than Fed funds and more complex
  - **Conventional (fixed-collateral) repurchase agreements**
    - Specific securities to serve as collateral for a loan
  - **General-collateral (GCF) Repo**
    - Low-cost collateral substitution

- **Long-term non-deposit funds**

  - Beyond one year: 5 to 12 years mortgages, capital notes and debentures
  - Favorable leveraging effects of such debt have made it attractive to larger financial firms
  - Tend to be a sensitive barometer of the perceived risk exposure





### 2.4 Non-deposit Funding Choice



**Tasks:**

- Describe and calculate the available funds gap

- Discuss factors affecting the choice of non-deposit funding sources

  

- In using non-deposit funds, funds managers must answer the following key questions:

  1. How much in total must be borrowed from these sources to meet funding needs?
     - **Available Funds Gap**
  2. Which non-deposit sources are best, given the borrowing institution's goals?
     - **The relative costs, risk, length of time, size of the institution, regulations limits**



**Available Funds Gap (AFG)**

- **Calculation formular:** 

  - Available funds gap (AFG)

    =Current and projected loans and investments the lending institution desires to make

    —Current and expected deposit inflows and other available funds

  - A **small amount will be added to AFG **to cover unexpected credit demands or unanticipated shortfalls in inflow funds

    

**Example**

- Suppose a commercial bank has new loan request that meet its quality standards for 150 million, it wishes to purchase 75 million in new Treasury securities and expects drawings on credit lines from its customers of 135 million. Deposit and other customer funds received today total 185 million, and those expected in the coming week will be 100 million.

**Answer:**

- AFG = (150+75+135) - (185+100)  = 75



**Factors of choosing alternative non-deposit sources**

- The relative costs of raising funds from each source

- The risk (volatility and dependability) of each funding source

- The length of time (maturity or term) for which funds are needed

- The size of the institution that requires funds

- Regulations limiting the use of alternative funds sources

- **The relative costs of raising funds**

  - In determining how much each source of borrowed funds costs, we looked at each funding source separately
    - **Effective cost rate**

- **The relative costs of raising funds from each source**

  - Effective cost rate on funds 

    = (Current interest cost on amounts borrowed

    +Noninterest costs incurred to access these funds

    \Net investable funds raised from this source

    - Current interest cost on amounts borrowed

      = Prevailing interest rate in the money market

      x Amount of funds borrowed

  - Noninterest costs to access funds = (Estimated cost rate representing staff time, facilities, and transaction costs) x Amount of funds borrowed

  - Net investable funds = Total amount borrowed less legal reserve requirements (if any), deposit insurance (if any), and funds placed in nonearning assets

  - Deposit insurance = Total deposits received from the public x Insurance fee per dollar



**Example: Effective cost rate**

- Suppose that Fed funds are currently trading at an interest rate of 6.0 percent. Moreover, management estimates that the marginal noninterest cost, in the form of personnel expenses and transactions fees, from raising additional monies in the Fed funds market is 0.25 percent. Suppose that a depository institution will need 25 million to fund the loans it plans to make today, of which only 24 million can be fully invested due to other immediate cash demands. What is the effective cost rate Fed funds ?

**Answer**

- Current interest cost on Federal funds = $0.06 \times 25m = 1.5m$
- Noninterest cost to access Federal funds raised = 0.0025 $\times$ 25m  = 0.063m
- The effective annualized Fed funds cost rate = $\frac{1.5+0.063}{24} = 6.51\%$



**Example: Effective cost rate considering insurance fee**

- Suppose management decides to consider borrowing funds by issuing negotiable CDs that carry a current interest rate of 7.00 percent. Moreover, raising CD money costs 0.75 percent in noninterest costs. An additional expense associated with selling CDs to raise money is the deposit insurance fee, assume the current insurance rate is $0.0027 per dollar of deposits. What is the effective cost rate of negotiable CDs?

**Answer**

- Current interest cost on negotiable CDs = $0.07 \times 25 = 1.75m$

- Noninterest cost to negotiable CDs = $0.0075 \times 25m = 0.1875 m$
- Insurance fee = $25 million \times 0.0027 = 0.0675m$
- Effective cost rate  = $\frac{1.75+0.1875}{24 -0.0675} = 8.1\%$ 



- **The risk (Volatility and dependability) of each funding source**

  - **Interest rate risk:** The volatility of credit costs, the shorter the term of the loan, the more volatile the prevailing market interest rate tends to be
  - **Credit availability risk:** Negotiable CD, Eurodollar, and commercial paper markets are especially sensitive to credit availability risks

- **The length of time (maturity and term) funds are needed:** Some funds sources, such as commercial paper and long-term debt capital may be difficult to access immediately

- **The size of the borrowing institution:** The Fed funds and central bank's discount window can make small denomination loans that are suitable for smaller firms

- **Regulations limiting the use of alternative funds sources: **Federal and state regulations may limit the amount, frequency, and use of borrowed funds

  





### 2.5 Overall cost of fund



**Tasks:**

- Calculate overall cost of funds using both the historical average cost approach and the pooled-funds approach

  

**Overall cost of funds calculation**

- The relative costs of raising funds from various sources including deposits
  - **Historical average cost approach (look at the past)**
    - Weighted average interest expense
    - Break-even cost (cover the operating and interest cost)
    - Weighted average overall cost of capital
  - **Pooled-funds approach (look at the future)**
    - Pooled deposit and nondeposit funds expense rate
    - Hurdle rate



**Example: Historical Average Cost Approach**

- A bank needs to raise fund for future loans, it asks what funds the financial firm has raised to date and what they cost:

| Sources of Funds Drawn                | Average Amount of Funds Raised (millions) | Average Rate of Interest Incurred |
| ------------------------------------- | ----------------------------------------- | --------------------------------- |
| Noninterest-bearing demand deposits   | $100                                      | 0%                                |
| Interest-bearing transaction deposits | $200                                      | 7%                                |
| Savings accounts                      | $100                                      | 5%                                |
| Time deposits                         | $500                                      | 8%                                |
| Money market borrowing                | $100                                      | 6%                                |

- Assumed the operating costs is 10 million and all earning assets is 750 million, what is the weighted average interest expense and break-even cost rate on borrowed funds invested in earning assets? Assumed the required rate of return of $100 million investment from stockholders is 12% after tax (tax rate is 35%), what is the weighted average overall cost of capital?

  

**Answer**
$$
Weighted \ average \ interest \ expense = \frac{All \ interest \ paid}{Total \ funds \ raised} = \frac{65}{1000} = 6.5\% \\
break-even \ cost \  rate = \frac{Interest + Other \ operating \ costs}{All \ earnings assets} = \frac{65+10}{750} = 10\% \\
\text{Weighted average overall cost of capital} \\ = \text{Break-even cost on borrowed funds}\\ + \text{Before-tax cost of the stockholders' investment in the borrowing institution} \\ \text{ =Break-even cost rate } \\ + \frac{\text{After-tax cost of stockholders' investment} }{1-Tax\ rate} \times \frac{\text{Stockholders' investment}}{Earning \ assets} \\= 10\% + \frac{12\%}{1-0.35} \times \frac{100}{750} = 12.5\%
$$


**Example: Pooled-funds approach**

 A bank needs to raise for future loans. Suppose the estimate

for future funding sources and costs is as follows:

| Profitable New Deposits and Nondeposit Borrowings | Dollars of New Deposit & Nondeposit Borrowing (millions) | Portion of New Borrowings Placed in New Earning Assets | Interest Expense & Other Operating Expenses of Borrowing |
| ------------------------------------------------- | -------------------------------------------------------- | ------------------------------------------------------ | -------------------------------------------------------- |
| Interest-bearing transaction deposits             | $100                                                     | 50%                                                    | 8%                                                       |
| Time deposits                                     | $100                                                     | 60%                                                    | 9%                                                       |
| New stockholders' investment                      | $100                                                     | 90%                                                    | 13%                                                      |

What is the Pooled deposit and non-deposit funds expense rate and what is the hurdle rate of return over all earning assets?





**Answer**

-  Pooled deposit and nondeposit funds expense rate = $\frac{\text{All expected operating expenses}}{\text{All new funds expected}} = \frac{30}{300} = 10\%$

-  Hurdle rate of return over all earning assets = $\frac{\text{All expected operating expenses}}{\text{Dollars available to place in earnings assets}} = \frac{30}{200} = 15\%$

**Tips: Hurdle rate of return over all earning assets:** minimum rate of return must be earned on any future loans and investments just to cover the cost of all new funds raised.



