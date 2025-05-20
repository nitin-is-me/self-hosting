# self-hosting
A tutorial to self host website in a custom domain for free. I'm using dedyn.io (or say desec.io) for free custom domain.

### Step 1: Get a domain:
I got a muster.dedyn.io domain for free from dedyn.io

### Step 2: Install pktriot
Download pktriot from https://packetriot.com

### Step 3: Create tunnel
Run `pktriot configure` and it'll create a tunnel for you with a random url

### Step 4: Add custom domain
In packetriot dashboard, add your custom domain. It'll give a TXT record to add in our domain records to verify that. It takes around 2-3 minutes to complete verification.

### Step 4: Add a CNAME record in domain records
In domain records, add CNAME record with hostname: tunnelUrl.pktriot.net, and in subname: chat. So we can visit our site at "chat.muster.dedyn.io"

### Step 5: Add http records locally in pktriot config
In terminal, add two https records. First one for forwarding the tunnel to port 3000. Second record for linking our domain name with that tunnel URL.
```
pktriot tunnel http add --domain randomurl.pktriot.net --destination localhost --http 3000 --letsencrypt
```
and
```
pktriot tunnel http add --domain chat.muster.dedyn.io --destination localhost --http 3000 --letsencrypt
```

NOTE: I'm not sure if the first record is necessary because in the end we just need our website to run at our domain, not the randomurl, but for now let's keep both!
<br>
Edit: Yes I can confirm, the first record isn't necessary because we don't want to run our site on random url, we need to run it on our domain.

### Step 6: Finished!
Now start your tunnel by running `pktriot start`
