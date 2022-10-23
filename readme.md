# pp-portfolio-classifier


Python script that automatically classifies Funds/ETFs managed in [Portfolio Performance](https://www.portfolio-performance.info/) files by the stock types, countries and industry sectors they are invested in. Furthermore it determines the Top 10 holdings of each fund. The classifier uses the information from morningstar as a data source for classification.
Based on the script by fbuchinger

## Warnings & Known Issues
- Experimental software - use with caution!  

## Installation
requires Python 3, git and Portfolio Performance.
Steps:
1. `git clone` this repository
2. in the install directory run `pip3 install -r requirements.txt`
3. test the script by running `python portfolio-classifier.py test/multifaktortest.xml > classified.xml` to test the script. Then open `classified.xml` in Portfolio Performance.

## How it works:

**Important: Never try this script on your original Portfolio Performance files -> risk of data loss. Always make a copy first that is safe to play around with or create a dummy portfolio like in test folder.**

1. In Portfolio Performance, save a copy of your portfolio file as unencrypted xml. The script won't work with any other format.
1. Optionally, you can add a "secid" attibute to the security. Edit each security (Ctrl + E) and add a "secid" attribute on the attributes tab. The value of the attribute is the code at the end of the morningstar url of the security (the id of length 10 after the  "?id=", something like 0P00012345). If the security does not have the secid attribute, the script will try to get it from the morningstar website, but the script might have to be configured with the domain of your country, since not all securities area available in all countries. The domain is only important for the translation from isin to secid. Once the secid is obtained, the morningstar APIs are country-independent. It also caches the mapping into a file called isin2secid.json in order to reduce the number of requests.
3. Run the script `python portfolio-classifier.py <path to pp.xml> > classified.pp.xml` 
4. open classified.pp.xml in Portfolio Performance and check out the additional classifications.


## Gallery

### Autoclassified stock-style
![Autoclassified Security types](docs/img/autoclassified-stock-style.png){:width="600px"}


### Autoclassified Regions
![Autoclassified Regions](docs/img/autoclassified-regions.png){:width="600px"}


### Autoclassified Sectors
![Autoclassified Sectors](docs/img/autoclassified-sectors.png){:width="600px"}
