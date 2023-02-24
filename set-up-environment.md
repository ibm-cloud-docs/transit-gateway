---

copyright:
  years: 2023
lastupdated: "2023-02-24"
keywords: api

subcollection: transit-gateway


---

{{site.data.keyword.attribute-definition-list}}

# Setting up your API environment
{: #set-up-environment}

Before you can use the transit gateway API, you need to setup your environment.
{: shortdesc}

## General prerequisites
{: #general-prerequisites}

Set up your account to access the transit gateway. Make sure that your account is [upgraded to a paid account](/docs/account?topic=account-accountfaqs#changeacct){: external}.

## API prerequisites
{: #api-prerequisites-setup}

Before you can use the API to interact with a transit gateway, you must get an IAM token, store the endpoint as a variable, and verify that you have access to the IBM Cloud Transit Gateway API service.

The following examples use the `transit.cloud.ibm.com` global endpoint.
{: note}

### Step 1: Store your API key as a variable
{: #store-api-key-variable}

Run the following command to store the API key for your account in an environment variable. If you don't have an API key, see [Creating an API key](/docs/account?topic=account-userapikey#create_user_key){: external}.

```sh
apikey="<YOUR_API_KEY>"
```

### Step 2: Get an IBM Identity and Access Management (IAM) token
{: #get-iam-token}

Run the following command to get and parse an IAM token by using the JSON processing utility [jq](https://stedolan.github.io/jq/){: external}. You can modify the command to use another parsing tool, or you can remove the last part of the command if you prefer to manually parse the token.

```sh
IAM_TOKEN=`curl -k -X POST \
  --header "Content-Type: application/x-www-form-urlencoded" \
  --header "Accept: application/json" \
  --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" \
  --data-urlencode "apikey=$apikey" \
  "https://iam.cloud.ibm.com/identity/token"  |jq -r '(.token_type + " " + .access_token)'`
```

To view the IAM token, run ``echo $iam_token``. The result should look like this:

```text
Bearer <your token>
```
{: screen}

The Authorization header expects the token to begin with `Bearer`. If the result doesn't include `Bearer`, update the `iam_token` variable to include it. These examples assume that `Bearer` is included in the `IAM_TOKEN`.

Because the IAM token expires, you must repeat the preceding step to refresh your token every hour.
{: important}

### Step 3: Store the API endpoint as a variable
{: #store-api-endpoint-variable}

Run the following command to store the API endpoint in a variable so that it can be reused later in your session.  

Public endpoint:

```sh
transit_api_endpoint="https://transit.cloud.ibm.com"
```

Virtual private endpoint:

```sh
transit_api_endpoint="https://private.transit.cloud.ibm.com"
```

To verify that the variable was saved, run `echo $transit_api_endpoint` and ensure that the response is not empty.

### Step 4: Store the API version as a variable
{: #store-api-version-variable}

Every API request must include the `version` parameter, in the format `YYYY-MM-DD`. Run the following command to store the version date in a variable so that it can be reused in your session. For more information about setting the `version` parameter, see **Versioning** in the [Transit Gateway API](https://{DomainName}/apidocs/transit-gateway#versioning)

```sh
api_version="2020-03-31"
```

To verify that this variable was saved, run ``echo $api_version`` and make sure that the response is not empty.

### Step 5: Verify that you have API access
{: #verify-api-access}

If you run into unexpected results, add the `--verbose` (debug) flag after the `curl` command to obtain detailed logging information.
{: tip}

* Call the [List Available Locations API](/apidocs/transit-gateway#list-offering-type-locations) to see the locations available for your transit gateway, in JSON format. At least one object should return. 

    ```sh
    curl -X GET "$transit_api_endpoint/v1/offering_types/dedicated/locations?version=$api_version"   -H "Authorization: $IAM_TOKEN"
    ```

* Call the [List gateways](/apidocs/transit-gateway#list-gateways) API to see any gateways that you already created under your account, in JSON format.

    ```sh
    curl -X GET "$transit_api_endpoint/v1/transit_gateways?version=$api_version"   -H "Authorization: $IAM_TOKEN"
    ```
