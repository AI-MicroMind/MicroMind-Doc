---
description: Learn how to managing API requests in AiMicromind
---

# Rate Limit

***

When you share your chatflow to public with no API authorization through API or embedded chat, anybody can access the flow. To prevent spamming, you can set the rate limit on your chatflow.

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="462"><figcaption></figcaption></figure>

* **Message Limit per Duration**: How many messages can be received in a specific duration. Ex: 20
* **Duration in Seconds**: The specified duration. Ex: 60
* **Limit Message**: What message to return when the limit is exceeded. Ex: Quota Exceeded

Using the example above, that means only 20 messages are allowed to be received in 60 seconds. The rate limitation is tracked by IP-address. If you have deployed aimicromind on cloud service, you'll have to set `NUMBER_OF_PROXIES` env variable.

## Rate Limit Setup

When you are hosting aimicromind on cloud such as AWS, GCP, Azure, etc, most likely there you are behind a proxy/load balancer. Therefore, the rate limit might not be able to work. More info can be found [here](https://github.com/express-rate-limit/express-rate-limit/wiki/Troubleshooting-Proxy-Issues).

To fix the issue:

1. **Set Environment Variable:** Create an environment variable named `NUMBER_OF_PROXIES` and set its value to `0` in your hosting environment.
2. **Restart your hosted aimicromind instance:** This enables aimicromind to apply changes of environment variables.
3. **Check IP Address:** To verify the IP address, access the following URL: `{{hosted_url}}/api/v1/ip`. You can do this either by entering the URL into your web browser or by making an API request.
4. **Compare IP Address** After making the request, compare the IP address returned to your current IP address. You can find your current IP address by visiting either of these websites:
   * [http://ip.nfriedly.com/](http://ip.nfriedly.com/)
   * [https://api.ipify.org/](https://api.ipify.org/)
5. **Incorrect IP Address:** If the returned IP address does not match your current IP address, increase `NUMBER_OF_PROXIES` by 1 and restart your aimicromind instance. Repeat this process until the IP address matches your own.
