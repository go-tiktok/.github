<p align="center"><img src="https://raw.githubusercontent.com/go-tiktok/brand/main/social/go-tiktok.png" alt="go-tiktok" width="640"></p>

<h1 align="center">go-tiktok</h1>
<p align="center">Pure-Go best-effort read client for public TikTok content.</p>
<p align="center"><a href="https://go-tiktok.github.io/docs/"><img src="https://img.shields.io/badge/docs-mkdocs--material-0A6E96?style=flat-square&logo=materialformkdocs&logoColor=white" alt="docs"></a> <a href="https://pkg.go.dev/github.com/go-tiktok/tiktok"><img src="https://img.shields.io/badge/pkg.go.dev-reference-0079A8?style=flat-square&logo=go&logoColor=white" alt="pkg.go.dev"></a> <img src="https://img.shields.io/badge/Go-1.26-00ADD8?style=flat-square&logo=go&logoColor=white" alt="Go"> <img src="https://img.shields.io/badge/license-BSD--3--Clause-0A6E96?style=flat-square" alt="license"></p>

---

## What is this?

A pure-Go, dependency-free, **best-effort** read client for public TikTok content, talking to TikTok's undocumented web JSON endpoints. The Go API is small and stable with an overridable base URL for network-free testing; the code builds correct requests and parses correct responses, but working end-to-end against live TikTok is not guaranteed.

The client lives in [`go-tiktok/tiktok`](https://github.com/go-tiktok/tiktok):

```go
c := tiktok.New(
	tiktok.WithMSToken("...msToken from a browser session..."),
	tiktok.WithSessionID("...sessionid cookie for authed reads..."),
)

// secUid is TikTok's opaque per-user id; obtain it once from a profile
// page's embedded JSON, then pass it here.
feed, err := c.UserPosts(context.Background(), "MS4wLjABAAAA...", 20, "0")
if err != nil {
	panic(err)
}
for _, v := range feed.Videos {
	fmt.Printf("%s  %d likes  %s\n", v.Permalink, v.Likes, v.Description)
}
fmt.Printf("cursor=%s hasMore=%v\n", feed.Cursor, feed.HasMore)
```

## Install

```sh
go get github.com/go-tiktok/tiktok
```

## ⚠️ Best-effort — read this first

TikTok does not publish or support a public web API. This client calls the same internal endpoints TikTok's own website uses, and TikTok actively defends them.

Requests often need a valid `msToken` and a signed parameter (`X-Bogus` / `_signature`) that this library does not compute; many reads additionally require a logged-in `sessionid` cookie. Expect anti-bot responses (403/429, or a 200 with an empty body) at any time.

## Links

- 📖 Docs — <https://go-tiktok.github.io/docs/>
- 🌐 Site — <https://go-tiktok.github.io/>
- 🧩 Client — <https://github.com/go-tiktok/tiktok>
- 📦 API reference — <https://pkg.go.dev/github.com/go-tiktok/tiktok>
- 🎨 Brand assets — <https://github.com/go-tiktok/brand>

---
<p align="center"><sub>Branding in <a href="https://github.com/go-tiktok/brand">go-tiktok/brand</a>.</sub></p>
