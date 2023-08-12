# Final_project
proiectul realizat ca lucrare la finalul cursului de data science de la SDA

proiectul a fost realizat in Google Colaboratory.

Pentru constituirea bazei de date care va fi supusa analizei si procesarii am preluat informatii din urmatoarele surse:
  https://coinmarketcap.com/ - Informatii despre valorile de schimb la inchiderea sesiunilor zilnice de tranzactionare pentru criptomonedele urmatoare: Bitcoin (BTC), LiteCoin (LTC), Monero (XMR), Ethereum (ETH), Binance (BNB).
  https://www.eia.gov/dnav/pet/hist/RBRTED.htm - Informatii despre valoarea de schimb la inchiderea sesiunilor zilnice de tranzactionare pentru barilul de petrol Brent (Londra)
  https://www.kitco.com/londonfix/gold.londonfix10.html - Informatii despre valorile de schimb la inchiderea sesiunilor zilnice de tranzactionare pentru urmatoarele metale pretioase: aur, argint, platina si palladium
  https://www.statista.com/statistics/412794/euro-to-u-s-dollar-annual-average-exchange-rate/ - Informatii despre valoarea de schimb la inchiderea sesiunilor zilnice de tranzactionare pentru dolarul american conform Bancii Centrale Europene
  https://markets.ft.com/data/funds/tearsheet/historical?s=IE00BD87Q831:EUR - Informatii despre valoarea indexului pentru Titluri de Trezorerie protejate împotriva inflației (TIPS) 
  https://www.wsj.com/market-data/quotes/index/SPX/historical-prices - Informatii despre valorile de schimb la inchiderea sesiunilor zilnice de tranzactionare pentru Standard & Poor's 500 Index, care este un indice ponderat în funcție de capitalizarea pieței de 500 de companii de top cotate la bursă din S.U.A.
  https://fred.stlouisfed.org/graph/?g=A2uJ – VIX măsoară așteptările pieței privind volatilitatea pe termen scurt, transmise de prețurile opțiunilor pe indicele bursier
  https://fred.stlouisfed.org/ - DFII30 – Indexul Inflatiei in statele Unite ale Americii pe ultimii 30 de ani, un factor care afecteaza direct bunurile tranzactionate pe orice piata de schimb 
Suplimentar s-a utilizat 2 baze de date cu stiri arhivate despre evolutia criptomonedelor:
  https://www.kaggle.com/code/lindleylawrence/crypto-sentiment
  https://www.kaggle.com/code/muhammedabdulazeem/bitcoin-price-prediction-based-on-headlines?cellIds=2&kernelSessionId=64904096 



In fisierul 'news_analysis.ipynb' au fost procesate stiri legate de criptomoneda bitcoin intre datele de 01.07.2015 si 05.04.2023.
acestea au fost procesate cu ajutorul modulului nltk SentimentIntensityAnalyzer. in urma procesarii s-au creat 3 features (coloane) noi si anume\
Polarity_avg (float64), Subjectivity_avg(float64) si Class (object). acestea au fost salvate intr-un fisier cvs numit 'news_dataset.csv'.

In fisierul 'data_base.ipynb' su fost incarcate fisierele de tip google sheets si excel, urmand a fi preprocesate si transformate intr-o maniera unitara care sa fie usor de utilizat si interpretat. avand in vedere faptul ca sursele de informatii sunt diferite site-uri oficiale care pastreaza inregistrari de date despre pretul petrolului, pretul unor metale pretioanse, indexul inflatiei - 'Treasury Inflation-Protected Securities Index', pretul de tranzactionare Euro - Dolar, informatii tranzactionale legate de criptomonedele: Bitcoin (BTC), BinanceCoin (BNB), LiteCoin (LTC), Ethereum (ETH), Monero (XMR).

In fisierul 'processing_datasets.ipynb' au fost colectate toate informatiile din rezultatul preprocesarii din precedentele fisere si au fost reunite intr-o singura baza de date.
au mai fost adaugate informatii despre evolutia pretului actiunilor 'S&P 500' si 'Treasury Securities at 30-Year Constant Maturity, Quoted on an Investment Basis, Inflation-Indexed'.

In fisierul 'main_file_v6.ipynb' au fost reutie toate informatiile aduante si introduse intr-un DataFrame.

a fost realizata o analiza exploratorie a datelor (EDA) prin care s-au verificat coralarea datelor intre ele si au fost aplicate corectii si procesari acolo unde a fost necesar.

au fost realizata o regresie liniara cu urmatorii regresori:
     LinearRegression()
     DecisionTreeRegressor()
     RandomForestRegressor()
     GradientBoostingRegressor()
     LGBMRegressor()
     XGBRegressor()

Au fost efectuate 6 seturi diferite de procesari ale acestor date. 
in fiecare caz din cele 6 au fost inlocuite valorile lipsa din dataset prin metoda interpolarii (cea mai corecta metoda matematica de simulare a datelor lipsa).
in primele 3 variante au fost efectuate scalari ale datelor cu modulul MinMaxScaler().
in cazul coloane categorice 'Class" a fost ales ca valorile lipsa sa fie inlocuite cu clasa "unknown". acesta coloana a fost ulterior encodata cu OrdinalEncoder().
in cazul celei de-a 3-a variante au fost eleimitate informatiile legate de criptomonedele Ethereum (ETH), BinanceCoin (BNB) si datele referitoare la 'Treasury Inflation-Protected Securities Index'.

in fiecare varianta si pentru fiecare regresor listat su fost facute predictiile si au fost listate MAE (mean average error), MSE (mean squared error) si Feature Importance (acolo unde aceste atribute exista).

pentru ca aceasta analiza este una legata de timp, datasetul a fost impartit in setul de antrenament si setul de test. 
pentru acesta setul de antrenament a fost ales sa cuprinda perioada dintre datele de 13.07.2010 si 10.10.2021
setul de test cuprinde datele din perioada 11.10.2021 si 05.04.2023.

pentru aceste 3 variante rezultatele au fost in general slabe, modelele avand o performanta redusa cu un UNDERFIT evident.

de la varianta 4 s-a decis reducerea intervalului de timp suspus analizei, astfel intervalul de timp devine 01.07.2015 si 05.04.2023.
setul de antrenament a fost ales sa cuprinda perioada dintre datele de 01.07.2015 si 17.03.2023
setul de test cuprinde datele din perioada 18.03.2023 si 05.04.2023.

in varianta 4 cel mai bun rezultat a fost obtinut de LinearRegression(), cu MAE = 2965.9995106835695, MSE = 12888684.15606913

in varianta 5 s-a decis eliminare tuturor datelor legate de alte criptomonede (XMR, ETH, BNB, LTC).
rezultatul cel mai bun a fost obtinut in acest caz de LinearRegression(), cu MAE = 6706.630866595477, MSE = 64586587.14649074

in varianta 6 s-a decis eliminare tuturor datelor legate de alte criptomonede (XMR, ETH, BNB, LTC) precum si coloana categorica 'Class'.
rezultatul cel mai bun a fost obtinut in acest caz de DecisionTreeRegressor(random_state=42), cu MAE = 56.41233333333333, MSE = 12080.017089999998

OBESRVATIE: de remarcat faptul ca acest regresor, desi are rezultate extraordinare comparativ cu celelate variante si ceilalati regresori, cel mai probabil este un OVERFIT.

rezultatele celolrlati regresori in acesta varianta au fost:
LinearRegression: MAE = 6924.243325138301, MSE = 48655282.701273255
DecisionTreeRegressor: MAE = 56.41233333333333, MSE = 12080.017089999998
RandomForestRegressor: MAE = 61.35828333333339, MSE = 7016.056664763675
GradientBoostingRegressor: MAE = 760.1480971082303, MSE = 1594509.2076801483
LGBMRegressor: MAE = 267.66052215276346, MSE = 128870.20257239716
XGBRegressor: MAE = 402.4546281585693, MSE = 416365.3674489091

su fost efectuate analize prin 2 retele neuronale (neural Prophet si TensorFlow) dar rezultatele au fost underfit.

la final au fost efectuate cateva analize asupra datelor pentru identificarea trendului, sezonalitatii, valorilor reziduale, autocorelarii si autocorelarii partiale. 

s-a folosit modulul ARIMA pentru o analiza ca TimeSeries. rezultatele sunt dezamagitoare, dar nu neasteptate MAE = 1690.3468107157748, MSE = 6827730.87818348.

la final s-a realizat o reprezentare grafica a evolutiei preturilor in timp pentru Bitcoin, aur, petrol platina si valorile S&P 500.

de asemena, s-au realizat cateva vizualizari.

Nota: unele fisiere au fost eliminate deoarece depasau dimensiunea maxima admisa de 50.0 MB.
