This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.


## Check cache-control
Run `npm run build` to make it a production build, then `npm run start` to start the server.

Next, check the response headers using curl.

### next 14.2.12

Static pages have Cache-Control.

```
curl --head http://localhost:3000/static 
HTTP/1.1 200 OK
Vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch, Accept-Encoding
x-nextjs-cache: HIT
X-Powered-By: Next.js
Cache-Control: s-maxage=31536000, stale-while-revalidate
ETag: "6n9vqgt9za41s"
Content-Type: text/html; charset=utf-8
Content-Length: 5257
Date: Wed, 18 Sep 2024 11:13:25 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```

Dynamic pages have no Cache-Control.
Is it correct??

```
curl --head http://localhost:3000/dynamic
HTTP/1.1 200 OK
Vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch, Accept-Encoding
link: </_next/static/media/4473ecc91f70f139-s.p.woff>; rel=preload; as="font"; crossorigin=""; type="font/woff", </_next/static/media/463dafcda517f24f-s.p.woff>; rel=preload; as="font"; crossorigin=""; type="font/woff"
X-Powered-By: Next.js
Content-Type: text/html; charset=utf-8
Date: Wed, 18 Sep 2024 11:13:18 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```

### next 14.2.9
This code is in next-ver-14.2.9 branch.

Static pages have Cache-Control.

```
curl --head http://localhost:3000/static 
HTTP/1.1 200 OK
Vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch, Accept-Encoding
x-nextjs-cache: HIT
X-Powered-By: Next.js
Cache-Control: s-maxage=31536000, stale-while-revalidate
ETag: "sxmg9viuvo41s"
Content-Type: text/html; charset=utf-8
Content-Length: 5257
Date: Wed, 18 Sep 2024 11:23:28 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```

Dynamic pages also have Cache-Control.

```
curl --head http://localhost:3000/dynamic
HTTP/1.1 200 OK
Vary: RSC, Next-Router-State-Tree, Next-Router-Prefetch, Accept-Encoding
link: </_next/static/media/4473ecc91f70f139-s.p.woff>; rel=preload; as="font"; crossorigin=""; type="font/woff", </_next/static/media/463dafcda517f24f-s.p.woff>; rel=preload; as="font"; crossorigin=""; type="font/woff"
X-Powered-By: Next.js
Cache-Control: private, no-cache, no-store, max-age=0, must-revalidate
Content-Type: text/html; charset=utf-8
Date: Wed, 18 Sep 2024 11:23:20 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```
