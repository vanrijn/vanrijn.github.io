---
title: "Twenty-Six Years of Blog, Mostly Saved"
date: 2026-05-22 23:30:00 -0700
categories:
- Computer Stuff
- Life in General
tags: []
---

I started blogging in 2000, and I never quite stopped — though there were stretches where I really, really did stop. The blog has lived in WordPress at movingparts.net for all of those twenty-six years, and during that time I've managed to make a few long-term-thinking mistakes.

This week I finally moved the whole thing — 425 posts, 231 images, twenty-six years of excellent fashion choices, hot takes about Linux, notes on family and video games and such — to a static Jekyll site. GitHub-hosted, fully self-contained, no database, no plugins, no server-side anything. Here's a retrospective.

## Flickr sure was great until it wasn't!

I started using Flickr to store all of my personal photos in 2005, way back when Flickr was free and cool. I had 1 Terabyte of storage, for free!!
It was fun! It was neat! It had great features! It was free! I loved old, free Flickr! And I kept literally every photo
our family had ever taken in Flickr.

And heck, since Flickr worked so well, and since they legitimately had really nice
features and functionality like gallery views, photo sets, etc., I also used Flickr for all of my website pictures.
Herein lies the start of my blog mistakes. What I should have done way back then was set up a separate Flickr account
that just hosted my blog graphics, but mistakes were made and I did not think of that.

14 years later, in 2019, after SmugMug bought Flickr, they limited the amount of free photos you could have in your
account to 1000 photos or videos. Then they started actively deleting photos that were above that 1000 photo limit. This
sucked and I started looking for options ASAP.

I at least had the forethought do do a full export of my Flickr library and saved it to my NAS,
around 9,600 photos and 9,600 metadata JSON files. The tools at the time
were pretty bad for doing anything with this export, so it was all I could do to try to go through the export and at
least name the files from the absolutely useless `img_3423_4675736600_o.jpg` format to something more manageable like
`2015-03-07-picture-of-family-dog.jpg`.

Shortly after doing the Flickr export and trying to salvage all the family photos, I cancelled my Flickr account. I had a vague sense that "I should probably make sure my photos aren't only on Flickr," but I lacked a more specific sense of "the previous 19 years of my blog has every single photo embedded as an `<img src="https://farm2.staticflickr.com/.../whatever.jpg">` and the moment your account goes away, every single one of those URLs returns a `410 Gone`."

I did go through some of my more photo-centric blog pages and found those images in the Flickr export and uploaded them
to WordPress's database. But there were so many images missing that I just didn't have the time to deal with.

## The WordPress → Jekyll Import

The export from WordPress was easy. The import via `jekyll-import` was, technically, also easy. It produced 425 HTML files in `_posts/`, each with proper YAML front-matter and permalinks matching my old WP URLs.

What it ALSO produced, on every single post, was this:

```html
<p><!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN" "http://www.w3.org/TR/REC-html40/loose.dtd"><br />
<html><body>
<p>The actual content of my post...</p>
<p></body></html></p>
```

Each post had been silently re-wrapped in a fake-HTML-document shell during import — `<!DOCTYPE>`, `<html>`, `<body>`, all glued to the top inside a stray `<p>` tag, with a deeply confused `<p></body></html></p>` orphan at the bottom. WordPress had also, at some point in its history, replaced every Amazon-affiliate tracking pixel's `<img src>` URL with a local `/assets/YYYY/MM/ir` reference (the importer stripped the `assoc-amazon.com` host but kept the path, ending at just `ir` because the original URL was `.../e/ir?t=...`).

So before I could even look at the content, I had a 425-file regex problem and a strange pile of "404 Not Found: ir" warnings.

## The Cleanup

Working through this over the course of several long evenings, and with the help of our new friendly and amazingly
capable AI/LLM friends, the rough order was:

1. **Strip the WP wrapper junk** from all 425 posts. Two regex patterns covered the standard wrapper, plus an extended variant some posts had picked up (DOCTYPE / html / head / meta / body, all wrapped across two paragraphs) that hit 8 outliers.
2. **Patch orphan `</p>` tags** the wrapper-stripper left behind. About 95 posts had ended up with a closing `</p>` that no longer had a matching `<p>` open — readers saw a literal `</p>` floating in the rendered text.
3. **Strip Amazon affiliate tracking pixels** — 22 of them across 10 posts, all rewritten by the importer to non-existent local paths.
4. **Audit image references** — 95 unique images were referenced in posts but missing from the assets folder. The blog rendered fine for text but had broken-image icons everywhere.
5. **Recover what I could from the Flickr export.** This is the part I'm most relieved about. Flickr embeds the photo ID directly in filenames (`chisel-out-the-rest_192264665_o.jpg` — `192264665` is the Flickr ID), and the export's per-photo JSON sidecars are keyed by ID too. A small Python script extracted candidate IDs from each missing filename, cross-referenced them against the export, and copied the original-resolution files into the matching `assets/YYYY/MM/` folders. **61 of the 95 missing images came back this way**, including two complete photo essays — a vinyl-windows DIY tutorial from 2006 and a 31-photo arcade-fightstick mod walkthrough from 2012 — that had been entirely broken since whenever I cancelled Flickr.
6. **Drop the rest** that couldn't be recovered: small WP UI decorations, hotlinked Wikipedia/KDE icons, Amazon product images, two Flickr photos that had been deleted before my 2019 export. 36 broken `<img>` tags removed across 24 posts.
7. **Clean up dirty filenames.** A previous WP-Photon CDN sync had created files literally named `sk0304_jsh01_18630658_o.jpeg?fit=620%252C622` on disk — the `?` made them HTTP-unreachable, since browsers strip query strings before the file lookup. They were just wasted disk space, scaled-down duplicates of the originals I'd just gotten back from Flickr. Deleted 56 of them and rewrote 154 HTML attribute references to point at the clean originals.
8. **Rewrite the external Photon CDN URLs** (`https://i*.wp.com/movingparts.net/wp-content/uploads/...`) used in lightbox `<a href>` wrappers to local `/assets/...` paths, so clicking an image no longer asks a long-dead WordPress CDN to serve me a copy of a thing I already have on disk.

There were also a handful of secondary cleanups along the way: switching from `jekyll-paginate` (which only paginates `/index.html`) to `jekyll-paginate-v2` (which paginates anything with `pagination: enabled: true`), then chasing down why the sidebar nav broke after the swap (because v2 strips the `path` attribute on paginated pages, which breaks the theme's `where: "path", "blog.md"` lookup), then fixing excerpt extraction (because WordPress-imported posts have one `<p>` per line separated by single `\n`, and Jekyll's default `excerpt_separator` is `\n\n` — which never matched, so every "excerpt" was the whole post).

## Lessons Learned

If you take anything from this, take this:

- **Don't cancel a photo host without searching your blog for `<img src>` references to it first.** The `<img>` tag's silent failure mode — the broken-image icon — is one of the loudest forms of personal-archive rot, and you don't usually notice until years later.
- **Take the export.** Even if you don't use it for seven years. *Especially* if you don't use it for seven years.
- **Filenames are interfaces.** Photo IDs in filenames, machine-readable metadata in sidecars, naming conventions you'll be able to grep five years later — these are gifts from Past You to Future You.
- **Static sites are forgiving.** Once everything is just files in `_posts/` and `assets/`, you can do almost any cleanup with a few hundred lines of Python and some quality time with your computer. Try doing that to a live WordPress database with whatever affiliate plugin you installed in 2008.

The blog's back. The photos are back. I owe most of this rescue to a single one-good-decision-among-many that 2019-Me made — taking that Flickr export — and most of the actual labor to several evenings of regex hygiene. Yay Jason!

Now to go actually post things.
