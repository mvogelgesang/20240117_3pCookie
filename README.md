# 3rd Party Cookie Embed

Purpose of this repo is to test and observe the impact of 3rd party cookie deprecation on Salesforce apps.

## Deployment

- Clone this repo locally
- Create scratch org `sf org create scratch -f config/project-scratch-def.json -a 3pCookie -w 10 -y 30 -v NAME_OF_YOUR_DEVHUB`
- Deploy repo contents to scratch org `sf project deploy start -o 3pCookie`
- Launch org, navigating to 3p Cookie app `sf org open -o 3pCookie -p lightning/n/auraIframe`

## Observing 3rd party cookies

### Writing as 3rd party, reading as first party

- In Chrome, go to `chrome://flags/#test-third-party-cookie-phaseout` check to see if this is enabled or disabled.
- Start by ensuring the setting is disabled.
- Go back to Salesforce app and click Write Cookies and then Read Cookies. A list of cookies should print below the buttons.
- Go to [https://aizazhakro.github.io/3p_connector/](https://aizazhakro.github.io/3p_connector/) and click Read Cookies.
- The cookies set within the Salesforce context should be displayed on the 3p_connector site. These are 3rd party cookies in action.

### Writing as first party, reading as third party

- In both Salesforce and the 3p_connector site, right click the page, go to Inspect > Application and clear all cookies from the github.io site.
- Go to the 3p_connector site and refresh, click Read Cookies. No cookies should print to the page. If so, they have not been cleared.
- Once you verify that no cookies are present, click Write Cookies and then Read Cookies. The list of cookies should print to the page. 
- Navigate over to Salesforce, refresh the page and click Read Cookies. The cookies written on the first party site should now be observed within the iframe on Salesforce.

### Observing changes when 3rd party cookie phaseout is enabled

- In Chrome, go to `chrome://flags/#test-third-party-cookie-phaseout` enable this flag and restart the browser when prompted.
- Repeat steps from above and observe that only partitioned cookies are set and readable with this flag enabled.
