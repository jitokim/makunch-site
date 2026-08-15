# makunch-site

Static pages for the makunch iOS apps, served by GitHub Pages.

**This repository is public on purpose.** App Store Connect requires a
*publicly reachable* Privacy Policy URL and Support URL for every app, and it
checks them. Nothing sensitive belongs here — the apps' source and their
internal notes live in a separate, private repository.

## Why these pages exist

| URL | App Store Connect | Required? |
|---|---|---|
| `/<app>/privacy/` | Privacy Policy URL | **yes, for every app** |
| `/<app>/support/` | Support URL | **yes, for every app** |
| `/` | Marketing URL | optional |

A custom EULA is *not* required: Apple applies its standard licence agreement
unless you supply your own, and these apps have no subscriptions, which is the
case that would force the issue.

## Publishing

```bash
gh repo create makunch-site --public --source=. --push
# then: Settings → Pages → Source: deploy from branch `main`, folder `/`
```

Pages will serve at `https://<user>.github.io/makunch-site/`. That URL is
perfectly acceptable to App Store Connect — a custom domain is optional.

### Pointing makunch.com at it later

Add a `CNAME` file containing `makunch.com` (or `apps.makunch.com`), then set
the DNS records GitHub asks for. **If you do this, the paths in App Store
Connect change**, so either do it before submitting or update each app's URLs
afterwards. Apple re-checks them at review.

## Keeping the pages honest

Each privacy page says the app collects nothing. That claim has to keep
matching two other things:

1. the **App Store privacy label** ("Data Not Collected") in App Store Connect;
2. the app's own **`PrivacyInfo.xcprivacy`** manifest.

They are three statements of one fact, maintained in three places, and a
reviewer compares them. If any app ever gains networking, analytics or an
account, all three change in the same commit — not afterwards.
