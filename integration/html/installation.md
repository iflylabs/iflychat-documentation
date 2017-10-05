iFlyChat can be easily installed on any HTML website. Just follow the steps given below:

Step 1: Generate APP ID and API Key from [iflychat.com](https://iflychat.com/dashboard).

Step 2: Copy and paste the code given below into your HTML page where you want to load chat.

```
<script type="text/javascript">
var iflychat_app_id="PASTE_YOUR_APP_ID_HERE";
var iflychat_external_cdn_host="cdn.iflychat.com",iflychat_bundle=document.createElement("SCRIPT");iflychat_bundle.src="//"+iflychat_external_cdn_host+"/js/iflychat-v2.min.js?app_id="+iflychat_app_id,iflychat_bundle.async="async",document.body.appendChild(iflychat_bundle);var iflychat_popup=document.createElement("DIV");iflychat_popup.className="iflychat-popup",document.body.appendChild(iflychat_popup);
</script>
```

Replace PASTE_YOUR_APP_ID_HERE with the APP ID from the Step 1. That's it!

Step 3: To configure your chat app, go to [iFlyChat Dashboard](https://iflychat.com/dashboard).
