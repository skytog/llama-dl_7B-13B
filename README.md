# llama-dl

[<img width="310" alt="image" src="https://user-images.githubusercontent.com/59632/222979421-290299aa-b34f-4f3a-97c7-23332fe12c36.png">](https://twitter.com/anitakirkovska/status/1632447982720131074)

[HN discussion](https://news.ycombinator.com/item?id=35026902) | [Twitter announcement](https://twitter.com/theshawwn/status/1632238214529400832)

## Intro

This repository contains a high-speed download of LLaMA, Facebook's 65B parameter model that was recently made available via torrent. (Discussion: [Facebook LLAMA is being openly distributed via torrents](https://news.ycombinator.com/item?id=35007978))

It downloads all model weights (7B, 13B, 30B, 65B) in less than two hours on a Chicago Ubuntu server.

```
real    98m12.980s
user    8m8.916s
sys     5m7.259s
```
This works out to 40MB/s (235164838073 bytes in 5892 seconds).

Personally, I just wanted to `curl` the weights instead of dealing with a torrent. The fact that it's several times faster was just a nice bonus.

## Download

To download all model weights, `cd` into the directory you want them, then run this:

Linux:

```sh
curl -o- https://raw.githubusercontent.com/shawwn/llama-dl/56f50b96072f42fb2520b1ad5a1d6ef30351f23c/llama.sh | bash
```

Mac:
```sh
brew install bash
brew install wget
```
```sh
curl -o- https://raw.githubusercontent.com/shawwn/llama-dl/56f50b96072f42fb2520b1ad5a1d6ef30351f23c/llama.sh | $(brew --prefix)/bin/bash
```

(Sorry mac users; they use some array syntax in the script that isn't supported on the version of bash that ships with Mac.)

Running random bash scripts generally isn't a good idea, but I'll stake my personal reputation on the fact that this link is safe. (It points to a specific SHA-1 hash rather than https://raw.githubusercontent.com/shawwn/llama-dl/main/llama.sh so that it's still safe even in the event that my repo or account got compromised.)

## How much space do I need?

219G (235164838073 bytes) total. [Here's a file list](https://gist.github.com/shawwn/bddb2f91aa45fbcdc0dd105d88816e75) with sizes for each.

## How do I know this is safe?

I ran this:

```
mkdir LLaMA
cd LLaMA
time curl -o- https://raw.githubusercontent.com/shawwn/llama-dl/56f50b96072f42fb2520b1ad5a1d6ef30351f23c/llama.sh | bash
cd ..
webtorrent 'magnet:?xt=urn:btih:b8287ebfa04f879b048d4d4404108cf3e8014352&dn=LLaMA&tr=udp%3a%2f%2ftracker.opentrackr.org%3a1337%2fannounce'
```

[Webtorrent](https://github.com/webtorrent/webtorrent-cli) began seeding immediately, which means every file is identical to what you would've gotten via the torrent. So this is just a faster version of the torrent.

<img width="310" alt="image" src="https://user-images.githubusercontent.com/59632/222940942-0051a645-b561-4f0b-878c-3d195354d526.png">

<img width="310" alt="image" src="https://user-images.githubusercontent.com/59632/222941107-b4ef0b21-3fa7-40d1-ae56-cbe385e6ac00.png">

## How much faster? (Updated)

Roughly 3.6x. As of March 4 2023, the torrent seems to download at around 11MB/s, which implies a download time of around 6 hours. (Help seed it, if you can.)

<img width="300" alt="image" src="https://user-images.githubusercontent.com/59632/222940992-f037b12c-c077-4136-8960-b2b1667ddc79.png">

## Will I get in trouble for using this download link?

I doubt it. This is using the download link that was leaked in the original torrent. (i.e. the leaker accidentally leaked their own unique download link that Facebook sent them.)

Technically, it may be illegal to knowingly use a private download link that was intended for someone else. Realistically, Facebook would risk their ML reputation by going after people who are merely trying to use what they themselves advertise as "open source."

**Update**: Facebook shut off the link a couple hours after this repo went live. I mirrored everything to R2 and updated the script to point to that instead.

Note that LLaMA was released under a ["non-commercial bespoke license"](https://github.com/facebookresearch/llama/blob/main/MODEL_CARD.md). Interestingly, Nvidia had a similar arrangement for StyleGAN, but that didn't stop Artbreeder from using it anyway. Nvidia never seemed to care enough to go after them. But if you [launch your own OpenAI API](https://github.com/shawwn/openai-server) and start charging money, don't be surprised when Facebook's lawyers come knocking.


