# Cheap Discord Bot Hosting: Is $0 Good Enough, What $1–$3 Buys, and When a $2.99 VPS Wins (Full Evoxt Plan Table)

The cheapest way to keep a Discord bot online is genuinely $0, and it will also be the least reliable part of your setup. Free bot hosts either run on ad revenue or ask you to click a renewal button every day, and the free tier usually gives you 128 MB of RAM, which is close to what discord.js consumes after `npm install` and before you have written a single command. A bot that a community depends on tends to land in the $1 to $3 range, and past that the better value is a small KVM virtual machine: Evoxt's VM-0.5 gives you 1 vCPU, 512 MB RAM and 5 GB SSD for **$2.99 a month**, with root access and a weekly backup included.

This guide to cheap Discord bot hosting compares those three tiers by the numbers that decide whether your bot stays up: RAM, bot count per plan, runtime support, renewal mechanics, and the add-ons and refund rules that only appear after you have paid.

> **One bot, no sysadmin ambitions:** a $1 to $3 bot container is the least work.
> **Several bots, or you want root and a database on the same box:** Evoxt's **VM-0.5 at $2.99/mo** (1 vCPU up to 6.0 GHz, 512 MB RAM, 5 GB SSD, weekly backup) matches the price of a mid-range bot panel and gives you a whole machine.
> 👉 [Check Evoxt's current VM plans and prices](https://bit.ly/EvoXt)

## Evoxt sells virtual machines, not bot panels

There is no one-click Discord preinstall and no panel process manager on Evoxt. You get root on a KVM VM, you install Node or Python, you write a systemd unit, and the machine stays up. That difference matters when you compare prices below, because a $2.99 VM and a $3.00 bot container are not the same product even when the numbers look identical.

The entry plan, VM-0.5, is 1 vCPU with a clock speed Evoxt advertises at up to 6.0 GHz, 512 MB of RAM and 5 GB of SSD for **$2.99/month**. A single discord.py or discord.js bot with a SQLite file fits comfortably. The plan names, specs and monthly prices on the Standard network are:

| Plan | vCPU | RAM | SSD | Price | Order |
| --- | --- | --- | --- | --- | --- |
| VM-0.5 | 1 core | 512 MB | 5 GB | **$2.99/mo** | [Order VM-0.5](https://bit.ly/EvoXt) |
| VM-0.75 | 1 core | 1 GB | 10 GB | $4.99/mo | [Order VM-0.75](https://bit.ly/EvoXt) |
| VM-1 | 1 core | 2 GB | 20 GB | $5.99/mo | [Order VM-1](https://bit.ly/EvoXt) |
| VM-1.5 | 2 cores | 2 GB | 20 GB | $6.95/mo | [Order VM-1.5](https://bit.ly/EvoXt) |
| VM-2 | 2 cores | 4 GB | 30 GB | $11.99/mo | [Order VM-2](https://bit.ly/EvoXt) |
| VM-3 | 4 cores | 4 GB | 30 GB | $14.99/mo | [Order VM-3](https://bit.ly/EvoXt) |
| VM-4 | 4 cores | 8 GB | 60 GB | $23.99/mo | [Order VM-4](https://bit.ly/EvoXt) |
| VM-6 | 8 cores | 8 GB | 60 GB | $29.99/mo | [Order VM-6](https://bit.ly/EvoXt) |
| VM-8 | 8 cores | 16 GB | 80 GB | $47.99/mo | [Order VM-8](https://bit.ly/EvoXt) |
| VM-12 | 16 cores | 16 GB | 80 GB | $60.95/mo | [Order VM-12](https://bit.ly/EvoXt) |
| VM-16 | 16 cores | 32 GB | 100 GB | $95.99/mo | [Order VM-16](https://bit.ly/EvoXt) |

Everything below the entry plan is irrelevant to a single bot. Even VM-1 at $5.99 with 2 GB is more than a Discord bot can use unless you are also running Postgres, a dashboard and a lavalink node on the same box.

A few things that apply to all eleven plans and are worth knowing before you compare them with a bot panel:

- **A weekly backup is included on every plan**, including VM-0.5. Most bot hosts either charge for backups or do not offer them on their cheapest tier.
- One IPv4 and one IPv6 address are included. Extra IPv4 addresses are $3/month each.
- Billing runs from monthly up to a 3-year prepay, and you can top up account credit and let it settle future invoices.
- Payment methods include cards, PayPal, Bitcoin and USDt Tron.
- The Standard network covers the US, UK, Canada, Germany, Poland, Amsterdam, Tokyo, Malaysia and Australia. The same plan names are also sold on the Premium (Hong Kong, Osaka) and Premium Plus (Malaysia) networks with a smaller monthly transfer allowance, so if you are targeting a specific region, check the transfer figure for that location rather than assuming the Standard one.
- Monthly transfer scales with the plan. A Discord bot uses almost none of it, so this is not a number you need to optimise.

## What $0 really costs you

There are two different things being sold as free, and they behave nothing alike.

ENDHOST runs ad-supported free container hosting for Discord and Telegram bots. The core hosting is free with no card and no expiring trial, and you get Node.js, Python, Ruby, Go, PHP and Bun, with dependencies installed from the manifest you already use (`package.json`, `requirements.txt`, `Gemfile`, `go.mod`, `composer.json`). The panel gives you live stdout/stderr logs, a file manager, and automatic restarts after a crash. Two limits matter: the promise is 24/7 operation "while the container is active", and Telegram bots must use long polling because webhook mode is not supported. You also have to create your own Discord application and paste the token in.

FPS.ms takes the opposite approach. Its free c.pico plan is 128 MB of RAM, 25% of one CPU core, 250 MB of SSD, with no database and no backup slot, priced at €0. It requires you to **renew every day**. Skip a renewal and the plan converts to €0.59/month; if you let it lapse, the bot goes offline until you renew, and after 28 days the server and its files are deleted.

That 128 MB is the part people underestimate. After a Node runtime and dependencies, the container is nearly full before your bot joins a guild, and a memory spike during a command handler is enough to kill the process. The daily renewal is a second failure mode that has nothing to do with your code: forget it for two days while travelling and your bot is offline in front of everyone.

Free hosting is a reasonable place to test a bot before you commit to paying. It is a bad place to run ticketing, moderation or economy data for a server with real members, because the failure is public and the recovery is manual.

## The $1–$3 band: what each extra dollar actually buys

Prices below are the entry plans, in the currency each host bills in. FPS.ms prices are in euros, the rest in US dollars, so convert before you decide.

| Provider and plan | Price | RAM | What else you get | What to watch |
| --- | --- | --- | --- | --- |
| Sparked Host Basic | $1.00/mo | 512 MB, 0.5 vCPU, 5 GB | 1 bot, unlimited databases, automatic backups, 2-day refund, 24-hour free trial | Unmanaged; add-ons cost extra |
| Gravel Host Basic | $1.20/mo | 10 GB NVMe (RAM not stated on the plan card) | 1 bot, NA/EU/AS/AU locations, FTP and file manager, auto restart, DDoS protection | 72-hour refund, first purchase only |
| FPS.ms c.micro | €1.29/mo | 512 MB, 50% of a core, 1 GB | 1 database, 1 backup, panel-managed container | Python and Node.js only |
| PebbleHost bot hosting | $3.00/mo | 1024 MB DDR4 ECC, unmetered SSD | 7-day automatic backups, 1 MySQL database, one-click preinstalls, Git, extra ports | North America and Europe only; Java cannot run multiple bots |
| Evoxt VM-0.5 | $2.99/mo | 512 MB, 1 vCPU, 5 GB | Root KVM, weekly backup, IPv4 and IPv6, any runtime you install | You handle setup, updates and process supervision |

Storage is the column that looks most important and decides the least. Ten gigabytes versus five versus unmetered makes no practical difference to a bot that stores a few hundred kilobytes of JSON. The two variables that actually change your experience are RAM and how many bots the plan allows. Sparked Host's $1.00 Basic and $2.00 Advanced both cap you at one bot; you need the $4.00 Advanced+ to host four. Gravel Host's $1.20 Basic is explicitly "one bot, a handful of servers", with multi-bot starting at the $2.95 Diamond plan. PebbleHost gives you 1 GB and lets Python and Node.js run as many bots as you want on that one plan, but Java is excluded from multi-bot entirely, which is only discoverable in the FAQ.

If your bot is one discord.js process in one or two servers, 512 MB is the right amount and the $1–$3 entry plans are all adequate. If you plan to shard or run three bots for three servers, budget for the tier that permits multiple bots, or take a VM where nobody counts processes.

## Add-ons and refund terms change the cheapest answer

Sparked Host's $1.00 sticker price is the most misleading number in this comparison. The Low Traffic IP add-on is **+$1.50/month** and puts your instance on an IP shared with at most nine others, which the company says helps with Cloudflare and Discord rate limiting. A Dedicated IP is **+$7.00/month**. Basic Discord Bot Management is **+$5.00/month**, limited to once or twice a month, and Discord support access is another $3.00. Add the low-traffic IP to the Basic plan and you are at $2.50; add a dedicated IP and you are at $9.50, roughly the price of Evoxt's VM-1.5 with 2 vCPU and 2 GB of RAM.

Refund windows differ enough to affect where you test first. Gravel Host offers 72-hour refunds on a new customer's first hosting purchase only, one refund per account for life, minus processing fees, and excludes renewals, add-ons, upgrades and free-trial products. Sparked Host advertises a 2-day refund guarantee plus a 24-hour free trial. FPS.ms did not publish refund terms in the plan documentation I reviewed, so treat that as unknown rather than generous.

👉 [Compare Evoxt's 512 MB and 1 GB VMs side by side](https://bit.ly/EvoXt)

## When a VPS beats a bot container

A VPS wins in four situations: you run more than one bot, you need a database and a dashboard alongside the bot, you need root to install something the panel does not support, or you are tired of per-bot limits. It also wins on longevity, because a $2.99 VM does not convert into a €0.59 monthly charge when you forget to click a button.

Evoxt's VM-0.5 at **$2.99/month** covers a single bot plus SQLite. VM-0.75 at $4.99 doubles RAM to 1 GB and storage to 10 GB, which is the sensible pick if you want Postgres and a small web dashboard on the same machine. For reference, other low-end VPS options exist around this price point, such as datapasa's VPS-1 at $1.81/month with 1 vCPU and 1 GB RAM on hourly billing, so it is worth pricing two or three providers before you commit to an annual term.

What you give up is real. Evoxt has been operating since 2020, a shorter track record than the established cloud providers, and its support response times get mixed reports, with community channels generally faster than tickets. Dedicated servers are only available in Malaysia. None of that is fatal for a Discord bot, where an hour of downtime while a ticket is answered is annoying rather than expensive, but it does mean you should not treat a $2.99 VM as a production SLA.

The CPU frequency claim is the one spec worth paying attention to here. Discord bot workloads are largely single-threaded, so per-core clock speed matters more than core count, and Evoxt advertises up to 6.0 GHz per core across the range. That is the argument for choosing VM-0.5 over a 4-core budget VPS at the same price.

## Before you order: five things to confirm

1. **Runtime support.** FPS.ms handles Python and Node.js only. ENDHOST adds Ruby, Go, PHP and Bun. PebbleHost supports Java but not multiple Java bots. On a VM, the limit is whatever you can install.
2. **RAM after dependencies.** 128 MB is tight for discord.js, 256 MB is workable for a small discord.py bot, 512 MB is comfortable, and 1 GB is where you add a database without watching memory graphs.
3. **Refund window.** 72 hours once per account at Gravel Host, 2 days at Sparked Host, unpublished at FPS.ms. Evoxt's refund terms were not something I could confirm from the pricing page, so read them before prepaying for a multi-year term.
4. **Currency.** FPS.ms bills in euros; everyone else above bills in US dollars. A €1.29 plan is not a $1.29 plan.
5. **Billing term.** Evoxt goes from monthly to 3-year prepay. Prepaying locks the price and locks you in.

## Which one to pick

One small bot, no Linux experience, no interest in maintaining a server: take a $1 to $3 container plan and accept that the cheapest ones cap you at a single bot. One bot but you want root, a database on the same box, a free weekly backup and no per-bot accounting: **Evoxt VM-0.5 at $2.99/month** is the direct equivalent, and VM-0.75 at $4.99 is the version with headroom. Several bots for several servers: skip the $1 tier entirely, since multi-bot starts at $2.95 to $4.00 on the panel hosts, and price a VM against those tiers before deciding. Testing an idea that may go nowhere: use a free tier, but pick ENDHOST's ad-supported model over a daily-renewal plan if the bot needs to stay online unattended.

Check the runtime list and the RAM figure first, the refund terms second, and the storage number last.

👉 [Start with Evoxt's VM-0.5 at $2.99/month and check the current plan list](https://bit.ly/EvoXt)
