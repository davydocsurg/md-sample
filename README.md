![LinkedIn Jobs API](https://nft.urbandesignsco.com/public/md-learn/linkedin-api.png)

# <center> LinkedIn Jobs API </center>

LinkedIn is, undoubtedly, a household name in the professional social network space. It has made the process of job hunting and recruitment easy.

Moreso, it continues to find ways to seamlessly deliver this solution; LinkedIn Jobs API, is one of such ways.

<br/>

## What you will learn from this article

-   [What you can use LinkedIn Jobs API for](#what-you-can-use-linkedin-jobs-api-for)
-   [Getting started.](#getting-started)
-   [Getting Access to LinkedIn APIs](#getting-access-to-linkedin-apis)
-   [Fetching a list of jobs](#fetching-a-list-of-jobs)
-   [Getting job details](#getting-job-details)
-   [Limitations of LinkedIn Jobs API](#limitations-of-linkedin-jobs-api)

<br/>
<br/>

## What you can use LinkedIn Jobs API for

The **LinkedIn Jobs API** allows users to automatically post jobs to LinkedIn from their **Applicant Tracking System (ATS)**, instead of manually posting via their LinkedIn Recruiter account. Recruiter clients who currently use a job distribution tool typically use this API.
It enables them to simultaneously post jobs on LinkedIn and other websites.
ATS partners no longer need to be authenticated to post on behalf of clients.

<br/>
<br/>

## Getting Started

The LinkedIn API uses [OAuth 2.0](https://oauth.net/2) for user authorization and API authentication. Applications must be authorized and authenticated before they can fetch data from LinkedIn or get access to member data. Most permissions and partner programs require an explicit approval from LinkedIn. Open Permissions are the only permissions that are available to all developers without special approval. You can find the complete guide on how to access LinkedIn APIs [here](https://docs.microsoft.com/en-us/linkedin/shared/authentication/getting-access?view=li-lms-2022-07).

The **LinkedIn Jobs API** allows authorized third parties such as clients, ATS systems, and job distributors to post jobs directly to LinkedIn on behalf of customers. This article provides instructions for integrating with LinkedIn's Jobs API.

The link below will take you to LinkedIn's Postman's workspace. Select the workspace with the name `LinkedIn Talent Solutions, you will find the `Job Posting` API collection in it.

[**LinkedIn Postman workspace**](https://www.postman.com/linkedin-developer-apis?tab=workspaces)

### Legal Requirements

#### Note:

-   The use of these APIs is restricted to those developers approved by LinkedIn. Please reach out to your LinkedIn Relationship Manager or Business Development contact as you will need to meet certain criteria and sign an API agreement with data restrictions to use this integration.
-   Complete the [LinkedIn Talent Solutions Partner Request Form](https://business.linkedin.com/talent-solutions/ats-partners/partner-application) if you are not yet a LinkedIn Talent Solutions Partner.

<br/>
<br/>

## Getting Access to LinkedIn APIs

#### Request Access

Before beginning development, you will need to be provisioned access to test resources, and your API apps need to be set up to access the job posting API endpoints. These can be done by completing the following steps:

### Create your LinkedIn application

[Create your LinkedIn application](https://www.linkedin.com/developer/apps) for the integration. Two API applications may be created for each integration: one for use in production and the other for testing and development. Please, request to fill out the Partner Onboarding Form by contacting your LinkedIn Business Development point of contact.

> If you've already created your app, you can skip this step. Otherwise, click on the **Create app** button. If creating an app, you will need a LinkedIn page to link the App. You can easily create one through LinkedIn if you do not have one.
> ![LinkedIn's Generate Token button](https://nft.urbandesignsco.com/public/md-learn/create_app_btn.png) > ![LinkedIn's Generate Token button](https://nft.urbandesignsco.com/public/md-learn/create_app_form.png)

### Verify your App

You need to verify your App before moving to the next steps. Actually, without verifying, you won't be able to move forward.

![Verify your App](https://nft.urbandesignsco.com/public/md-learn/verify_app.png)

### Get Your Client ID and Client Secret

Once you have your App ready, it's time to get the Client ID and Client Secret. Click on the App from the dashboard and navigate to the Auth tab. Under Application credentials, the _Client ID_ and _Client Secret_ are present. These are needed for the LinkedIn API.

![Get Your Client ID and Client Secret](https://nft.urbandesignsco.com/public/md-learn/clientid.png)

### Get Your Client ID and Client Secret

LinkedIn has made adding app permissions easier by defining them as products. Go on to the Products tab and click the select button on Sign In with LinkedIn.

![Get Your Client ID and Client Secret](https://nft.urbandesignsco.com/public/md-learn/enable_signin.png)

After the Sign In with the LinkedIn product is successfully added, your **App's OAuth 2.0 scopes** will reflect the new permissions granted. Simply go to the Auth tab and scroll down to the bottom.

![Get Your Client ID and Client Secret](https://nft.urbandesignsco.com/public/md-learn/0auth_creds.png)

### Getting LinkedIn Access Token

You can do this through your browser or an application like Postman. If you decide to use Postman and have never used it before, you can get it on [Postman's](https://postman.com) official website. Now, follow these steps:

-   Create your Collection;
-   Go to the Authorization tab, on the Type selector, select OAuth 2.0, and Add auth data to Request Headers:

![ouath and headers](https://nft.urbandesignsco.com/public/md-learn/give_auth.png)

-   Go to _Configure New Token_, at the bottom of the page. Set _Token Name_ {Whatever you decide} - _Grant Type_: Authorization Code
-   _Auth URL_: [https://www.linkedin.com/oauth/v2/authorization](https://www.linkedin.com/oauth/v2/authorization)
-   _Access Token URL_: [https://www.linkedin.com/oauth/v2/accessToken](https://www.linkedin.com/oauth/v2/accessToken)
-   _Client ID_: (the Client Id on the LinkedIn App you created, you can find in the Auth tab)
-   _Client Secret_: (on the LinkedIn App, Auth tab > Application keys}
-   Scope: _r_emailaddress_ _r_liteprofile_ (based on the LinkedIn App Authorization)
-   State (anything, I used something unique like _DCEeFWf45A53sdfKef424_)
-   Click on **Get New Access Token Button**

![Configure new Token](https://nft.urbandesignsco.com/public/md-learn/config_auth_token.png)

> We are almost done, just a few more steps 😉

After you click the **Get New Access Token Button**, a browser window will open up asking for your LinkedIn credentials. Follow the steps presented in the browser to get your Token in your Postman collection as result.

## And that's it! Let's make sure it's working:

In your collection, create three GET requests to test if your _sign-in_ with LinkedIn is working.

-   Member Profile: https://api.linkedin.com/v2/me

-   Member Profile Picture: https://api.linkedin.com/v2/me?projection=(id,firstName,lastName,profilePicture(displayImage~:playableStreams))

-   Member Email Address: https://api.linkedin.com/v2/emailAddress?q=members&projection=(elements*(handle~))

Remember to set the Authorization for each GET request as _Inherit auth from parent_ (it should be the default). There are many other APIs you can call using your access token. Check out what LinkedIn has to offer in their [documentation](https://docs.microsoft.com/en-us/linkedin/shared/integrations/people/profile-api).

## You're done!

<br/>
<br/>

## Fetching a list of jobs

Firstly, let's take a look at how LinkedIn displays jobs on its website.

![LinkedIn Jobs Sample](https://nft.urbandesignsco.com/public/md-learn/jobs_screenshot.png)

We can easily see from the above image, how we can see jobs and their details on Linkedin. On the left side, we can see the job names, company names, their locations, etc. And on the other side, we can see the job description.

To use the job listings endpoints in LinkedIn's API, go back to [**LinkedIn Postman workspace**](https://www.postman.com/linkedin-developer-apis?tab=workspaces)

### Now, it's code time!

#### Interact with your own profile

To be able to interact with your profile, you need:

-   The Access Token (Who would have thought?)
-   Your _Profile ID_

> To get your profile ID, Let’s bash!

```
curl -H "Authorization: Bearer YOUR_ACCESS_TOKEN" -X GET "https://api.linkedin.com/v2/me"
```

Your output should be in `JSON` format.

This shows that our Access Token is working. So, let's write the code to fetch a list of jobs with **Python**. You can use any text editor of your choice, I'm using [VSCode](https://code.visualstudio.com/)

> Note: You need `r_JYMBII` permission but it is not given to any app by default. You need to manually request for that in Linkedin's developer admin panel.

Create a `job-list.py` file in the root of your project folder, then copy and paste the following codes:

```python
import json

# See http://developer.linkedin.com/documents/profile-fields#fullprofile
# for details on additional field selectors that can be passed in for
# retrieving additional profile information.

# Display your own positions...

jobs = app.get_positions(selectors=['positions'])
print json.dumps(jobs, indent=1)

# Display positions for someone in your network...

# Get an id for a connection. We'll just pick the first one.
connection_id = connections['values'][0]['id']
connection_positions = app.get_profile(member_id=connection_id,
                                       selectors=['positions'])
print json.dumps(connection_positions, indent=1)
```

> Sample output reveals a number of interesting details about each position, including the company name, industry, summary of efforts, and employment dates:

```python
{
 "positions": {
  "_total": 10,
  "values": [
   {

   "FrontEnd Engineer": {
     "industry": "Computer Software",
     "industry": "Computer Software",
     "company_name": "Digital Reasoning Systems"
     ...
    },

   "Senior Full Stack JavaScript Developer":{
     "industry": "Computer Software",
    "location": "Remote",
     "company_name": "Nubela"
     ...
    }
    ...
   },

  ]
 }
}
```

<br />
<br />

## Getting job details

To get a particular job's details, on your browser, navigate to the jobs tab on LinkedIn, open a job and copy the id from your browser's search bar, e.g. `ij2ju487YG`

```python
import json

# Display job details...

job_details = app.get_job_details(selectors=['positions'])
print json.dumps(job_details, indent=1)

```

Output:

```python
{
 "positions": {
  "_total": 10,
  "values": [
    "Senior Full Stack JavaScript Developer":{
     "industry": "Computer Software",
    "location": "Remote",
     "company_name": "Nubela"
     ...
    }
  ]
 }
}
```

## Limitations of LinkedIn Jobs API

As promising and exciting as this feature is, it is far from a one-size-fit-all solution. It is not without its limitations. Below are some of its limitations:

-   Only Applicant Tracking System (ATS) have access to this feature
-   Not all user data can be retrieved, personal information are witheld.
    For example, only name, photo, headline, contact information, experience, education, summary, and location are available. The user's connections, network updates, job listings, groups,companies and other contents are witheld. Other restrictions can be found [here](https://legal.linkedin.com/api-terms-of-use)
