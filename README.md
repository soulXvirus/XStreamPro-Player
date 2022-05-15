# XStreamPro + Cloudflare Workers

Play & Download Doodstream, Streamlare, Google Photo, ZPlayer, XHamster, Hanime videos using JWPlayer and XStreamPro REST API. 

# Supported Hosts

XStreamPro Player supports following video hosts:

1. [Google Photo](https://photos.google.com/)
2. [Doodstream](https://doodstream.com/)
3. [Streamlare](https://streamlare.com/)
4. [ZPlayer](https://v2.zplayer.live/)
5. [Xhamster](https://xhamster.com/)
6. [Hanime](https://hanime.tv/)

We'll adding more to this list. If you have any suggestions on adding any particular host, create an [issue](https://github.com/delivrjs/XStreamPro-Player/issues/new). We'll see if we can add it.

# Features

<ul>
  <li>Ligtning Fast API</li>
  <li>JWPlayer Support</li>
  <li>One Custom Skin</li>
  <li>Fully Customizable Player</li>
  <li>Google Analytics &amp; Microsoft Clarity Integrated</li>
  <li>Completely Written in HTML, CSS, JAVASCRIPT</li>
  <li>CDN Enabled</li>
  <li>Video, Popads, Popunder Ads Supported</li>
  <li>FuckAdBlock</li>
  <li>Simple yet Powerful Admin Panel</li>
  <li>Encryption</li>
  <li>Iframe Restriction</li>
  <li>Download Option</li>
  <li>Clean, minified &amp; Secure Source Code</li>
</ul>

# Usage

XStreamPro Player uses [`cloudflare workers`](https://workers.cloudflare.com/) for fetching streaming & downloading links. In short, we have created an `API` which return all information in `JSON` format. In this [`repo`](https://github.com/delivrjs/xstreampro-player), you'll find a file named [`workers.js`](https://github.com/delivrjs/XStreamPro-Player/blob/main/workers.js). This is our main file which contains `API` code. Follow below steps to set it up:

1. Register & create a [worker](https://workers.cloudflare.com/) on cloudflare
2. Upload [`workers.js`](https://github.com/delivrjs/XStreamPro-Player/blob/main/workers.js) in newly created cloudflare worker
3. Next, go to variable -> environment in worker dashboard and set following:

   Variable Name: `ACCESS_CONTROL_ALLOW_ORIGIN` <br>
   Variable Value: `www.yourdomain.com,www.domain2.com`

Above setting is necessary or worker will throw error. Above setting creates `ACCESS_CONTROL_ALLOW_ORIGIN` header which will block `cross-origin` requests. Add `$` at the end of your `domain hostname`. If you want to add multiple domain, just add `comma (,)` after every domain or just add `.*` to authorize all `cross-origin` requests.
<br><br>
<img width="1302" alt="environment_variable" src="https://user-images.githubusercontent.com/100680713/168439955-cf1b4be8-4954-452e-b117-e02c5963f8f6.png">
<br><br>
4. Copy the `workers url` and open [`config.json`](https://github.com/delivrjs/XStreamPro-Player/blob/main/config.json) file.
5. This file contains configuration setting related to `JW Player`, `Google & Clarity Analytics`, & `cloudflare workers`
6. Find following line:
   
   `"workers": [ "https://api.delivrjs.workers.dev" ]`
   
6. Replace `https://api.delivrjs.workers.dev` with your `personal workers url`. Don't add `/` at the end of url. You can add as many as workers you want as per your traffic. For e.g.

   `"workers": [ "workers_1", "workers_2", "workers_3" ]`
   
7. XStreamPro Player will randomly pick a worker.
8. [`config.json`](https://github.com/delivrjs/XStreamPro-Player/blob/main/config.json) also contains configuration settings for setting up `JW Player`. The `key(s)` of [`config.json`](https://github.com/delivrjs/XStreamPro-Player/blob/main/config.json) JSON file is/are itself explainatory. You can edit those as per your need.
9. Next, Open [`adminCode`](https://github.com/delivrjs/XStreamPro-Player/blob/main/adminCode) and enter any random key `(type: string)`. This code will be entered upon at the time of link creation by admin from XStreamPro Admin Panel. This is so called `security measure` which restricts anyone who is in ignorance of `adminCode`, to generate links. Since, javascript isn't well-suited approach for it, we recommend you that you can come with your own idea and implement it in your code.
10. That's it. Now it's time to upload your script. 
11. Facing any issue, [open one](https://github.com/delivrjs/XStreamPro-Player/issues/new)

# Demo

We have setup a demo of this entire script at following url.

1. Demo Website: [https://xstreampro.pages.dev](https://xstreampro.pages.dev/)
2. API workers.js: [https://api.delivrjs.workers.dev](https://api.delivrjs.workers.dev/)

# API Endpoints

Following is usage of API:

Replace `https://api.delivrjs.workers.dev` with your `worker url`

`GET https://api.delivrjs.workers.dev/api/:host/:id`

| Parameter | Value                                                                | Required |
| --------- | -------------------------------------------------------------------- | -------- |
| host      | doodstream, streamlare, googlephoto, zplayer, hanime, xhamster | Yes      
| id        | ID of the video e.g. p1r85dfb6zgz                                    | Yes      |


## Sample Request:

`GET https://api.delivrjs.workers.dev/api/googlephoto/PvkhtGCRa2UsEhgQ7`

## Response:

<pre class="highlight json"><code><span class="hljs-punctuation">{</span>
  <span class="hljs-attr">&quot;status&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-keyword">true</span><span class="hljs-punctuation">,</span>
  <span class="hljs-attr">&quot;host&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-string">&quot;googlephoto&quot;</span><span class="hljs-punctuation">,</span>
  <span class="hljs-attr">&quot;filecode&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-string">&quot;PvkhtGCRa2UsEhgQ7&quot;</span><span class="hljs-punctuation">,</span>
  <span class="hljs-attr">&quot;download&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-string">&quot;https://video-downloads.googleusercontent.com/AGQNM9L5IfpCHptBkwHOQg-et92YWiBHBsngZ5V5pK4-okrU_RleBxCHfrbZZmFaEKqVhUhLEom5rUj21QSWdnDC7j4LKSYGdyOXL-GgF67W7gKn9hJTsf6g34nJ16CMzyBG4BAWRMNJ5dNjeq-PJIg3yUH2kDi9gd9LH3eSkPXLPTOTPelQ8A72i_mFwOKkkEdqGFrLj3nqiE4yEWGD8yocg1q6ufTezgP4z2wkzjk1SYgq2yK8UVM?authuser=0&quot;</span><span class="hljs-punctuation">,</span>
  <span class="hljs-attr">&quot;image&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-string">&quot;https://lh3.googleusercontent.com/pw/AM-JKLXgFgAPzyh-FtyOsS4DfODuNrsBtbvWgymYCxaF1hS-fJAMpPSWCF0yuEsoyzk_UPowDT0bbdHyYNK6pXba69720RxEYjHfR4nAXowkx9dBBMkxOacqF_lkYSi5dQpxsJZ-tsI_49fzE06RLknUz8s=w1280-h720-no&quot;</span><span class="hljs-punctuation">,</span>
  <span class="hljs-attr">&quot;sources&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-punctuation">[</span>
    <span class="hljs-punctuation">{</span>
      <span class="hljs-attr">&quot;file&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-string">&quot;https://lh3.googleusercontent.com/pw/AM-JKLXgFgAPzyh-FtyOsS4DfODuNrsBtbvWgymYCxaF1hS-fJAMpPSWCF0yuEsoyzk_UPowDT0bbdHyYNK6pXba69720RxEYjHfR4nAXowkx9dBBMkxOacqF_lkYSi5dQpxsJZ-tsI_49fzE06RLknUz8s=m22&quot;</span><span class="hljs-punctuation">,</span>
      <span class="hljs-attr">&quot;label&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-string">&quot;720p&quot;</span><span class="hljs-punctuation">,</span>
      <span class="hljs-attr">&quot;type&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-string">&quot;video/mp4&quot;</span>
    <span class="hljs-punctuation">}</span><span class="hljs-punctuation">,</span>
    <span class="hljs-punctuation">{</span>
      <span class="hljs-attr">&quot;file&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-string">&quot;https://lh3.googleusercontent.com/pw/AM-JKLXgFgAPzyh-FtyOsS4DfODuNrsBtbvWgymYCxaF1hS-fJAMpPSWCF0yuEsoyzk_UPowDT0bbdHyYNK6pXba69720RxEYjHfR4nAXowkx9dBBMkxOacqF_lkYSi5dQpxsJZ-tsI_49fzE06RLknUz8s=m18&quot;</span><span class="hljs-punctuation">,</span>
      <span class="hljs-attr">&quot;label&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-string">&quot;360p&quot;</span><span class="hljs-punctuation">,</span>
      <span class="hljs-attr">&quot;type&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-string">&quot;video/mp4&quot;</span>
    <span class="hljs-punctuation">}</span><span class="hljs-punctuation">,</span>
    <span class="hljs-punctuation">{</span>
      <span class="hljs-attr">&quot;file&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-string">&quot;https://lh3.googleusercontent.com/pw/AM-JKLXgFgAPzyh-FtyOsS4DfODuNrsBtbvWgymYCxaF1hS-fJAMpPSWCF0yuEsoyzk_UPowDT0bbdHyYNK6pXba69720RxEYjHfR4nAXowkx9dBBMkxOacqF_lkYSi5dQpxsJZ-tsI_49fzE06RLknUz8s=m36&quot;</span><span class="hljs-punctuation">,</span>
      <span class="hljs-attr">&quot;label&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-string">&quot;180p&quot;</span><span class="hljs-punctuation">,</span>
      <span class="hljs-attr">&quot;type&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-string">&quot;video/mp4&quot;</span>
    <span class="hljs-punctuation">}</span>
  <span class="hljs-punctuation">]</span><span class="hljs-punctuation">,</span>
  <span class="hljs-attr">&quot;vtt&quot;</span><span class="hljs-punctuation">:</span> <span class="hljs-keyword">null</span>
<span class="hljs-punctuation">}</span></code></pre>

## Important Note

It is important to note that direct access to `API endpoint` will return following response:

<pre class="highlight json"><code><span class="hljs-punctuation">{</span>
  <span class="hljs-attr">&quot;status&quot;</span> <span class="hljs-punctuation">:</span> <span class="hljs-keyword">false</span><span class="hljs-punctuation">,</span>
  <span class="hljs-attr">&quot;msg&quot;</span> <span class="hljs-punctuation">:</span> <span class="hljs-string">&quot;missing origin&quot;</span>
<span class="hljs-punctuation">}</span></code></pre>

Make sure you make a `XMLHttpRequest`, `fetch`, or any other request but not direct `HTTP` request.

# Important Note

It is important that you make `request` from `client or user side` and not from `server side`. Since streaming & downloading links are IP protected, making `server side` request might not generate `client or user side` playable links, which will result in streaming & downloading error.

# Limitations

XStreamPro Player do not impose any limitations on our script. Since nothing is connected to our server, we are not required to create any limitations. However, only limitations those imposed by cloudflare exists. Following limitations are imposed by cloudlfare workers:

  1. `Up to 10ms CPU time per request`
  2. `Up to 100,000 requests per day`

However, you can create as many accounts as you need, since it is a free service and keep adding workers to [`config.json`](https://github.com/delivrjs/XStreamPro-Player/blob/main/config.json). It'll randomly pick a worker.

# Non-Obfuscated workers.js

[`workers.js`](https://github.com/delivrjs/XStreamPro-Player/blob/main/workers.js) file contained in this [respository](https://github.com/delivrjs/XStreamPro-Player) is `obfuscated` using [`obfuscator.io`](https://obfuscator.io/). This is done to protect it from getting debugged and eventually respective hosts blocking them. Hope you all understand. 

However, we are willing to sell `non-obfuscated workers.js` file. Please check pricing below

# Pricing for Non-Obfuscated workers.js

1. `$10 per host`
2. `$7 per host, if two or more hosts are purchased together`
3. `$48 for all hosts purchased together`

You'll get `non-obfuscated workers.js` file. Please note that, `non-obfuscated workers.js` is faster than `obfuscated workers.js` one. So that's a benefit for you.

# Donation

Maintaining this script requires time & effort. Consider donating:

1. BTC: 3JQ3PFTRbhEGa58fHNNgpVqBpZBZPjKSHZ
2. USDT: TBUenWYHtvb7dByBqnnyywEBeeQ8vL2BVe
