# CloudFront

## CloudFront - Caching & Caching Policies

- The cache lives at each CloudFront Edge Location
- CloudFront identifies each object in the cache using the Cache Key (see next slide)
- You want to maximize the Cache Hit ratio to minimize requests to the origin
- You can invalidate part of the cache using the CreateInvalidation API

What is CloudFront Cache Key?

- A unique identifier for every object in the cache
- By default, consists of hostname + resource portion of the URL
- If you have an application that serves up content that varies based on user, device, language, location
- You can add other elements (HTTP headers, cookies, query strings) to the Cache Key using CloudFront Cache Policies

## CloudFront Policies - Cache Policy

Cache based on: - HTTP Headers: None - Whitelist - Cookies: None - Include All-Except - All - Query Strings: None - Whitelist - Include All-Except - All

Contorl the TTL (0 seconds to 1 year), can be set by the origin using the Cache-Control header, Expires header

All HTTP headers, cookies, and query strings that you include in the Cache Key are automatically included in origin requests

Cache Policy HTTP Headers - None - Don't include any headers in the Cache Key (except default) - Headers are not forwarded (except default) - Best caching performance

    - Whitelist
    	- only specified headers included in the Cache key
    	- Specified headers are also forwarded to Origin

Origin Request Policy

- Specify values that you want to include in origin requests without including them in the Cache Key (no duplicated cached content)

- You can include:
  - HTTP headers: None - Whitelist - All viewer headers options
  - Cookies: None - Whitelist - All
  - Query Strings: None - Whitelist - All

Ability to add CloudFront HTTP headers and Custom Headers to an origin request that were not included in the viewer request.

## CloudFront - Cache Behaviors

- Configure different settings for a given URL path pattern
- Example: one specific cache behavior to images/\*.jpg files on your origin web server
- Route to different kind of origins/origin groups based on the content type or path pattern
  /images/_
  /api/_
  /\* (default cache behavior)

## CloudFront - Caching & Caching Invalidations - Hands On

## CloudFront - Signed URL / Cookies

You want to distribute paid shared content to premium users over the world
We can use CloudFront Signed URL / Cookie. We attach a policy with: - Includes URL expiration - Includes IP ranges to access the data from - Trusted Signers (Which AWS accounts can create signed URLs)

Signed URL = access to individual files (one signed URL per file)
Signed Cookies = access to multiple files (one signed cookie for many files)

CloudFront Signed URL : - Allow to a path, no matter the origin - Account wide key-pair, only the root can manage it - Can filter by IP, path, date, expiration - Can leverage caching features

S3 Pre-Signed URL: - Issue a request as the person who pre-signed the URL - Users the IAM key of the signing IAM principal - Limited Lifetime

## CloudFront - Signed URL - Key Groups + Hands On

Two types of singers: - Either a trusted key group (recommended) - Can leverage APIs to create and rotate keys(and IAM for API security) - An AWS Account that contains a CloudFront Key Pair - Need to manage keys using the root account and the AWS console - Not recommended because you shouldn't use the root account for this
In your Cloud Front distribution, create one of more trusted key groups

You generate your own public / private key - The private key is used by your applications (e.g. EC2) to sign URLs - The public key (uploaded) is used by CloudFront to verify URLs

## CloudFront - Advanced Concepts

## CloudFront - Real Time Logs
