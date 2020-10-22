# is-educational-email-domain

Check if an email domain belongs to an educational institutions.

## Why?

We offer [AnonymityBot](https://anonymitybot.com) for **free** for educational
purposes but couldn't find a complete list email domains of educational institutions.

## API

### **`hasCommonEducationalTld(domain)`**

We call a TLD `Common Educational TLD` if it is either `.edu`, `.edu.xx` or
`.ac.xx` and was fetched from
[publicsuffix.org](ttps://publicsuffix.org/list/public_suffix_list.dat).
See [fetch_common_educational_tlds_and_slds.sh](https://github.com/anonymitybot/is-educational-email-domain/blob/master/assets/fetch_common_educational_tlds_and_slds.sh)

### **`hasAdhocEducationalTld(domain)`**

Some institutions don't use `edu` or `ac` TLDs, and (usually) use their own
country code. For instance, [University of Oslo](https://uio.no) has an email
domain for each department - `math.uio.no`, `fys.uio.no` - in order to capture
all such departments we check for `uio.no`.


### **`isEducationalEmailDomain(domain)`**

## Example

```js
const {
  isEducationalEmailDomain,
  hasAdhocEducationalTld,
  hasCommonEducationalTld,
} = require('@anonymitybot/is-educational.');

  hasCommonEducationalTld('stanford.edu'); // true
  hasCommonEducationalTld('u-tokyo.ac.jp'); // true
  hasCommonEducationalTld('cuhk.edu.cn'); // true

  hasCommonEducationalTld('bla.cc'); // false - .ac is a ccTLD

  hasAdhocEducationalTld('math.ethz.cz'); // true - etch.cz is an ad-hoc educational domain
  hasAdhocEducationalTld('stanford.edu'); // false - .edu is a common educational tld (but not an ad-hoc one)

  isEducationalEmailDomain('stanford.edu'); // true
  isEducationalEmailDomain('math.ethz.cz'); // true

  isEducationalEmailDomain('bla.cc'); // false - .ac is a ccTLD

```


Install with `yarn add @anonymitybot/is-educational-email-domain`


## Data