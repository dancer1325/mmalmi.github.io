| 03 May 2009 23:32:26

* Satoshi's next feature
  * escrow 
    * == 
      * keep & blocked transaction's coind | special address
      * | meet conditions OR sign MULTIPLE -> share the money

* "(not accepted)" issue 
  * goal
    * being reduced | v0.1.6

* FAQ 
  * 's goal
    * ONLY general simple repeated questions
  * why to set up your firewall / forward port 8333?
    * enable you receive incoming connections
    * OTHERWISE, only to send
  * | UI's 
    * bottom appear: Generating, 4 connections, 4024 blocks, 164 transactions
      * number of transactions == recorded transactions (even failed generation attempts)
      * blocks
        * == total number of blocks | block chain
          * -> display the SAME number | ALL network
          * if someone generates a block -> goes up
          * if your node has been disconnected & you connect your node -> download what was generated
    * status column / next to your transactions
      * blocks number OR confirmations
        * == number of blocks / have come AFTER that transaction
    * sync status bar
      * == progress | download ALL transactions
        * | start, fast
          * Reason: less transactions & MORE simple
        * | right now, slow
          * Reason: MORE transactions, MORE complex


* TODO: 
 &gt; I&#39;m having an unusual run of (block not-accepted) failures, and 
thought I&#39;d let you know in
 &gt; case this was of any significance.

What rate of not-accepted did you see?  I didn&#39;t see anything unusual on 
my end.  If you had more than, say, 4 in a row, that would be abnormal 
and probably a loss of network communication.  If it&#39;s scattered and 
less than 25%, just random bad luck.  It&#39;s normal and harmless to 
randomly get some per cent of not-accepted, and of course randomness can 
sometimes bunch up and look like a pattern.

The idea of an option to View/Hide unaccepted blocks is a good one, as 
well as View/Hide all generated blocks so you can more easily see 
incoming transactions.  Seeing the unaccepted blocks is just annoying 
and frustrating.  Everyone faces the same rate of unaccepted, it&#39;s just 
a part of the process.  It would probably be best to default to hide 
unaccepted blocks, so as not to show giving and taking away something 
that never was, and not show new generated blocks at all until they have 
at least one confirmation.  It would only mean finding out you have a 
generated block 15 minutes later than normal, and then you still have 
119 blocks to go before it matures anyway.  This is on the to-do list 
for v0.1.6.

Satoshi

[note: I have some improvements in 0.1.6 to reduce this problem somewhat,
and it&#39;ll also improve when the network is larger]







 &gt; For some reason your transfer to me shows up as &#34;From: unknown&#34; even
 &gt; though I added you to my address book.
 &gt;
 &gt; I have a &#34;Generated (not accepted)&#34; line in my transaction list, it
 &gt; seems like an attempt to generate a coin went wrong somehow. Not sure
 &gt; what happened here - presumably my node successfully solved a block
 &gt; but then I went offline before it was sent to the network?

Transactions sent to a bitcoin address will always say &#34;from: unknown&#34;. 
  The transaction only tells who it&#39;s to.  Sending by bitcoin address 
has a number of problems, but it&#39;s so nice having the fallback option to 
be able to send to anyone whether they&#39;re online or not.  There are a 
number of ideas to try to improve things later.  For now, if things work 
out like the real world where the vast majority of transactions are with 
merchants, they&#39;ll pretty much always make sure to set up to receive by 
IP.  The P2P file sharing networks seem fairly successful at getting a 
large percentage of their users to set up their firewalls to forward a port.

I badly wanted to find some way to include a comment with indirect
transfers, but there just wasn&#39;t a way to do it.  Bitcoin uses EC-DSA, which
was essential for making the block chain compact enough to be practical with
today&#39;s technology because its signatures are an order of magnitude smaller
than RSA.  But EC-DSA can&#39;t encrypt messages like RSA, it can only be used
to verify signatures.

The &#34;Generated (not accepted)&#34; normally happens if two nodes find a 
block at close to the same time, one of them will not be accepted.  It&#39;s 
normal and unavoidable.  I plan in v0.1.6 to hide those, since they&#39;re 
just confusing and annoying and there&#39;s no reason for users to have to 
see them.  While the network is still small like it is now, if you can&#39;t 
receive incoming connections you&#39;re at more of a disadvantage because 
you can&#39;t receive block announcements as directly.




 &gt; ...So far it has two &#34;Generated&#34; messages, however the
 &gt; &#34;Credit&#34; field for those is 0.00 and the balance hasn&#39;t changed.  Is
 &gt; this due to the age/maturity requirement for a coin to be valid?

Right, the credit field stays 0.00 until it matures, then it&#39;ll be
50.00.  BTW, you can doubleclick on a line for details.





 &gt; ...understand correctly, there is only one (or maybe a few) global
 &gt; chain[s] into which all transactions are hashed. If there is only one
 &gt; chain recording &#34;the story of the economy&#34; so to speak, how does this
 &gt; scale? In an imaginary planet-wide deployment there would be millions
 &gt; of even billions of transactions per hour being hashed into the chain...

 &gt; ...I found the section on incentives hard to follow. In particular, I&#39;m
 &gt; not clear on what triggers the transition from minting new coins as a
 &gt; reason to run a node, to charging transaction fees (isn&#39;t the point of
 &gt; BitCoin largely to zero transaction costs anyway?). Presumably there&#39;s
 &gt; some human in charge of the system...

 &gt; ...How did you decide on the inflation schedule for v1? Where did 21
 &gt; million coins come from? What denominations are these coins? You
 &gt; mention a way to combine and split value but I&#39;m not clear on how this
 &gt; works. For instance are bitcoins always denominated by an integer or
 &gt; can you have fractional bitcoins?...

 &gt; ...it&#39;s rare that I encounter truly
 &gt; revolutionary ideas. The last time I was this excited about a new
 &gt; monetary scheme was when I discovered Ripple. If you have any thoughts
 &gt; on Ripple, I&#39;d also love to hear them.

There is only one global chain.

The existing Visa credit card network processes about 15 million 
Internet purchases per day worldwide.  Bitcoin can already scale much 
larger than that with existing hardware for a fraction of the cost.  It 
never really hits a scale ceiling.  If you&#39;re interested, I can go over 
the ways it would cope with extreme size.

By Moore&#39;s Law, we can expect hardware speed to be 10 times faster in 5 
years and 100 times faster in 10.  Even if Bitcoin grows at crazy 
adoption rates, I think computer speeds will stay ahead of the number of 
transactions.

I don&#39;t anticipate that fees will be needed anytime soon, but if it 
becomes too burdensome to run a node, it is possible to run a node that 
only processes transactions that include a transaction fee.  The owner 
of the node would decide the minimum fee they&#39;ll accept.  Right now, 
such a node would get nothing, because nobody includes a fee, but if 
enough nodes did that, then users would get faster acceptance if they 
include a fee, or slower if they don&#39;t.  The fee the market would settle 
on should be minimal.  If a node requires a higher fee, that node would 
be passing up all transactions with lower fees.  It could do more volume 
and probably make more money by processing as many paying transactions 
as it can.  The transition is not controlled by some human in charge of 
the system though, just individuals reacting on their own to market forces.

A key aspect of Bitcoin is that the security of the network grows as the 
size of the network and the amount of value that needs to be protected 
grows.  The down side is that it&#39;s vulnerable at the beginning when it&#39;s 
small, although the value that could be stolen should always be smaller 
than the amount of effort required to steal it.  If someone has other 
motives to prove a point, they&#39;ll just be proving a point I already concede.

My choice for the number of coins and distribution schedule was an 
educated guess.  It was a difficult choice, because once the network is 
going it&#39;s locked in and we&#39;re stuck with it.  I wanted to pick 
something that would make prices similar to existing currencies, but 
without knowing the future, that&#39;s very hard.  I ended up picking 
something in the middle.  If Bitcoin remains a small niche, it&#39;ll be 
worth less per unit than existing currencies.  If you imagine it being 
used for some fraction of world commerce, then there&#39;s only going to be 
21 million coins for the whole world, so it would be worth much more per 
unit.  Values are 64-bit integers with 8 decimal places, so 1 coin is 
represented internally as 100000000.  There&#39;s plenty of granularity if 
typical prices become small.  For example, if 0.001 is worth 1 Euro, 
then it might be easier to change where the decimal point is displayed, 
so if you had 1 Bitcoin it&#39;s now displayed as 1000, and 0.001 is 
displayed as 1.

Ripple is interesting in that it&#39;s the only other system that does 
something with trust besides concentrate it into a central server.

Satoshi






 &gt; If we assume that 0.1% is a good risk rate, then z=5 thus
 &gt; any transaction must wait a bit less than an hour before being
 &gt; solidified in the chain. As micropayments for things like web content
 &gt; or virtual goods are by definition something that requires low
 &gt; overhead, waiting an hour seems like quite a significant hurdle.

For the actual risk, multiply the 0.1% by the probability that the buyer 
is an attacker with a huge network of computers.

For micropayments, you can safely accept the payment immediately.  The 
size of the payment is too small for the effort to steal it. 
Micropayments are almost always for intellectual property, where there&#39;s 
no physical loss to the merchant.  Anyone trying to steal a micropayment 
would probably not be a paying customer anyway, and if they want to 
steal intellectual property they can use the file sharing networks.

Currently, businesses accept a certain chargeoff rate.  I believe the 
risk with 1 or even 0 confirming blocks will be much less than the rate 
of chargebacks on verified credit card transactions.

The usual scam against a merchant that doesn&#39;t wait for confirming 
blocks would be to send a payment to a merchant, then quickly try to 
propagate a double-spend to the network before the merchant&#39;s copy. What 
the merchant can do is broadcast his transaction and then monitor the 
network for any double-spend copies.  The thief would not be able to 
broadcast during the monitoring period or else the merchant&#39;s node would 
receive a copy.  The merchant would only have to monitor for a minute or 
two until most of the network nodes have his version and it&#39;s too late 
for the thief&#39;s version to catch up and reach many nodes.  With just a 
minute or two delay, the chance of getting away without paying could be 
made much too low to scam.  A thief usually needs a high probability of 
getting an item for free to make it worthwhile.  Using a lot of CPU 
power to do the brute force attack discussed in the paper in addition to 
the above scam would not increase the thief&#39;s chances very much.

Anything that grants access to something, like something that takes a 
while to download, access to a website, web hosting, a subscription or 
service, can be cancelled a few minutes later if the transaction is 
rejected.


 &gt; How is the required difficulty of each block communicated through the
 &gt; network and agreed upon?

It&#39;s not communicated.  The formula is hardcoded in the program and 
every node does the same calculation to know what difficulty is required 
for the next block.  If someone diverged from the formula, their block 
would not be accepted by the majority.





 &gt; Is the code free/open source or just open source?

It&#39;s free open source.  It&#39;s the MIT license, which just requires some 
disclaimer text be kept with the source code, other than that you can do 
just about anything you want with it.  The source is included in the 
main download.

Satoshi





 &gt; Is there a way to be told of new versions? Does the app auto update
 &gt; itself?  Some kind of mailing list would be excellent.

The list is:
bitcoin-list@lists.sourceforge.net
Subscribe/unsubscribe page:
http://lists.sourceforge.net/mailman/listinfo/bitcoin-list
Archives:
http://sourceforge.net/mailarchive/forum.php?forum_name=bitcoin-list

I&#39;ll always announce new versions there.  Automatic update, or at least 
notification of new versions, is definitely on the list.





[this inflation discussion was before the transaction fee mechanism and 
fixed plan of 21 million coins was posted, so it may not be as 
applicable anymore]

 &gt; Since they can be created for free (or at the cost
 &gt; of computer power people have anyway for other reasons),
 &gt; monetizing them means simply giving away money.

You&#39;re still thinking as if the difficulty level will be so easy that 
people will be able to generate all the bitcoins they want.

Imagine you have to run your computer 24/7 for a month to generate 1 
cent.  After a year, you could generate 12 cents.  That&#39;s not going to 
make it so people can just generate all the bitcoin they want for spending.

The value of bitcoins would be relative to the electricity consumed to 
produce them.  All modern CPUs save power when they&#39;re idle.  If you run 
a computational task 24/7, not letting it idle, it uses significantly 
more power, and you&#39;ll notice it generates more heat.  The extra wattage 
consumed goes straight to your power bill, and the value of the bitcoins 
you produce would be something less than that.


 &gt; Why would they, when they make money by generating
 &gt; new ones

No, they can&#39;t make money that way.  It would cost them more in 
electricity than they&#39;d be selling the bitcoins for.






Historically, people have taken up scarce commodities as money, if 
necessary taking up whatever is at hand, such as shells or stones.  Each 
has a kernel of usefulness that helped bootstrap the process, but the 
monetary value ends up being much more than the functional value alone. 
  Most of the value comes from the value that others place in it.  Gold, 
for instance, is pretty, non-corrosive and easily malleable, but most of 
its value is clearly not from that.  Brass is shiny and similar in 
colour.  The vast majority of gold sits unused in vaults, owned by 
governments that could care less about its prettiness.

Until now, no scarce commodity that can be traded over a communications 
channel without a trusted third party has been available.  If there is a 
desire to take up a form of money that can be traded over the Internet 
without a TTP, then now that is possible.

Satoshi






 &gt; As more capable
 &gt; computer hardware comes out, the natural supply per user
 &gt; doubles at every cycle of Moore&#39;s law.

Actually, that is handled.  There&#39;s a moving average that compensates 
for the total effort being expended so that the total production is a 
constant.  As computers get more powerful, the difficulty increases to 
compensate.


 &gt; I do not recall any economic history of a commodity subject
 &gt; to natural inflation ever being used as money

There&#39;s gold for one.  The supply of gold increases by about 2%-3% per 
year.  Any fiat currency typically averages more inflation than that.



 &gt; Won&#39;t there be massive inflation as computers get faster and are able 
to solve the proof-of-work problem faster?

The difficulty is controlled by a moving average that compensates for 
the total effort being expended to keep the total production constant. 
As computers get more powerful, the difficulty increases to compensate.






 &gt; If someone double spends, then the transaction record
 &gt; can be unblinded revealing the identity of the cheater?

Identities are not used, and there&#39;s no reliance on recourse.  It&#39;s all 
prevention.





 &gt; ...You&#39;re saying
 &gt; there&#39;s no effort to identify and exclude nodes that don&#39;t
 &gt; cooperate? I suspect this will lead to trouble and possible DOS
 &gt; attacks.

There is no reliance on identifying anyone.  As you&#39;ve said, it&#39;s
futile and can be trivially defeated with sock puppets.

The credential that establishes someone as real is the ability to
supply CPU power.






 &gt; But in the absence of identity, there&#39;s no downside to them
 &gt; if spends become invalid, if they&#39;ve already received the
 &gt; goods they double-spent for (access to website, download,
 &gt; whatever). The merchants are left holding the bag with
 &gt; &#34;invalid&#34; coins, unless they wait that magical &#34;few blocks&#34;
 &gt; (and how can they know how many?) before treating the spender
 &gt; as having paid.
 &gt;
 &gt; The consumers won&#39;t do this if they spend their coin and it takes
 &gt; an hour to clear before they can do what they spent their coin on.
 &gt; The merchants won&#39;t do it if there&#39;s no way to charge back a
 &gt; customer when they find the that their coin is invalid because
 &gt; the customer has doublespent.

This is a version 2 problem that I believe can be solved fairly
satisfactorily for most applications.

The race is to spread your transaction on the network first.  Think 6
degrees of freedom -- it spreads exponentially.  It would only take
something like 2 minutes for a transaction to spread widely enough
that a competitor starting late would have little chance of grabbing
very many nodes before the first one is overtaking the whole network.
During those 2 minutes, the merchant&#39;s nodes can be watching for a
double-spent transaction.  The double-spender would not be able to
blast his alternate transaction out to the world without the merchant
getting it, so he has to wait before starting.

If the real transaction reaches 90% and the double-spent tx reaches
10%, the double-spender only gets a 10% chance of not paying, and 90%
chance his money gets spent.  For almost any type of goods, that&#39;s
not going to be worth it for the scammer.

Information based goods like access to website or downloads are
non-fencible.  Nobody is going to be able to make a living off
stealing access to websites or downloads.  They can go to the file
sharing networks to steal that.  Most instant-access products aren&#39;t
going to have a huge incentive to steal.

If a merchant actually has a problem with theft, they can make the
customer wait 2 minutes, or wait for something in e-mail, which many
already do.  If they really want to optimize, and it&#39;s a large
download, they could cancel the download in the middle if the
transaction comes back double-spent.  If it&#39;s website access,
typically it wouldn&#39;t be a big deal to let the customer have access
for 5 minutes and then cut off access if it&#39;s rejected.  Many such
sites have a free trial anyway.

Satoshi






[in response to a question about scale]

100,000 block generating nodes is a good ballpark large-scale size
to think about.  Propagating a transaction across the whole network
twice would consume a total of US$ 0.02 of bandwidth at today&#39;s
prices.  In practice, many would be burning off excess allocated
bandwidth or unlimited plans with one of the cheaper backbones.
There could be millions of SPV clients.  They only matter in how
many transactions they generate.  If they pay 1 or 2 cents
transaction fees, they pay for themselves.  I&#39;ve coded it so you
can pay any optional amount of transaction fees you want.  When the
incentive subsidy eventually tapers off, it may be necessary to put
a market-determined transaction fee on your transactions to make
sure nodes process them promptly.

To think about what a really huge transaction load would look like,
I look at the existing credit card network.  I found some more
estimates about how many transactions are online purchases.  It&#39;s
about 15 million tx per day for the entire e-commerce load of the
Internet worldwide.  At 1KB per transaction, that would be 15GB of
bandwidth for each block generating node per day, or about two DVD
movies worth.  Seems do-able even with today&#39;s technology.

Important to remember, even if Bitcoin caught on at dot-com rates
of growth, it would still take years to become any substantial
fraction of all transactions.  I believe hardware has already
recently become strong enough to handle large scale, but if there&#39;s
any doubt about that, bandwidth speeds, prices, disk space and
computing power will be much greater by the time it&#39;s needed.

Satoshi






 &gt; One other question I had... What prevents the single node with the most
 &gt; CPU power from generating and retaining the majority of the BitCoins?
 &gt; If every node is working independently of all others, if one is
 &gt; significantly more powerful than the others, isn&#39;t it probable that this
 &gt; node will reach the proper conclusion before other nodes? An
 &gt; underpowered node may get lucky once in a while, but if they are at a
 &gt; significant horsepower advantage I would expect the majority of BitCoins
 &gt; to be generated by the most powerful node.

It&#39;s not like a race where if one car is twice as fast, it&#39;ll always
win.  It&#39;s an SHA-256 that takes less than a microsecond, and each guess
has an independent chance of success.  Each computer&#39;s chance of finding
a hash collision is linearly proportional to it&#39;s CPU power.  A computer
that&#39;s half as fast would get half as many coins.






[question about what to backup]

The files are in &#34;%appdata%\Bitcoin&#34;, that&#39;s the directory to
backup.

%appdata% is per-user access privilege.  Most new programs like
Firefox store their settings files there, despite the headwind of
Microsoft changing the directory name with every Windows release
and being full of spaces and so long it runs off the screen.





[question about what to backup]

The directory is &#34;%appdata%\Bitcoin&#34;
It has spaces in it so you need the quotes
cd &#34;%appdata%\bitcoin&#34;

On XP it would typically be:
C:\Documents and Settings\[username]\Application Data\Bitcoin

Backup that whole directory.  All data files are in that
directory.  There are no temporary files.





[question about what to backup]

The crucial file to backup is wallet.dat.  If bitcoin is running
then you have to backup the whole %appdata%\bitcoin directory
including the database subdirectory, but even if it&#39;s not running
it certainly feels safer to always backup the whole directory.

The database unfortunately names its files &#34;log.0000000001&#34;.  To
the rest of the world, &#34;log&#34; means delete-at-will, but to database
people it means delete-and-lose-everything-in-your-other-files.  I
tried to put them out of harm&#39;s way by putting them in the
database subdirectory.  Later I&#39;ll write code to flush the logs
after every wallet change so wallet.dat will be standalone safe
almost all the time.







 &gt; &gt; You know, I think there were a lot more people interested in the 90&#39;s,
 &gt; &gt; but after more than a decade of failed Trusted Third Party based 
systems
 &gt; &gt; (Digicash, etc), they see it as a lost cause. I hope they can make the
 &gt; &gt; distinction that this is the first time I know of that we&#39;re trying a
 &gt; &gt; non-trust-based system.
 &gt;
 &gt; Yea, that was the primary feature that caught my eye. The real trick
 &gt; will be to get people to actually value the Bitcoins so that they become
 &gt; currency.

Hal sort of alluded to the possibility that it could be seen as a
long-odds investment.  I would be surprised if 10 years from now
we&#39;re not using electronic currency in some way, now that we know
a way to do it that won&#39;t inevitably get dumbed down when the
trusted third party gets cold feet.

Once it gets bootstrapped, there are so many applications if you
could effortlessly pay a few cents to a website as easily as dropping
coins in a vending machine.

[this next bit turned out to be very controversial.  there is extreme
prejudice against spam solutions, especially proof-of-work.]

It can already be used for pay-to-send e-mail.  The send dialog is
resizeable and you can enter as long of a message as you like.
It&#39;s sent directly when it connects.  The recipient doubleclicks
on the transaction to see the full message.  If someone famous is
getting more e-mail than they can read, but would still like to
have a way for fans to contact them, they could set up Bitcoin and
give out the IP address on their website.  &#34;Send X bitcoins to my
priority hotline at this IP and I&#39;ll read the message personally.&#34;

Subscription sites that need some extra proof-of-work for their
free trial so it doesn&#39;t cannibalize subscriptions could charge
bitcoins for the trial.




[again, I don&#39;t know why I&#39;m including this, as it&#39;s best to stay
away from claims about spam.  people automatically react violently
against any suggestion of a spam solution.]

 &gt; Spammer botnets could burn through pay-per-send email filters
 &gt; trivially (as usual, the costs would fall on people other than the
 &gt; botnet herders &amp; spammers).

Then you could earn a nice profit by setting up pay-per-send
e-mail addresses and collecting all the spam money.  You could
sell it back to spammers who don&#39;t have big enough botnets to
generate their own, helping bootstrap the currency&#39;s value.  As
more people catch on, they&#39;ll set up more and more phony addresses
to harvest it.  By the time the book &#34;How I got rich exploiting
spammers and you can too&#34; is coming out, there&#39;ll be too many fake
addresses and the spammers will have to give up.




 &gt; &gt; * Spammer botnets could burn through pay-per-send email filters
 &gt; &gt;   trivially
 &gt; If POW tokens do become useful, and especially if they become money,
 &gt; machines will no longer sit idle. Users will expect their computers to
 &gt; be earning them money (assuming the reward is greater than the cost to
 &gt; operate). A computer whose earnings are being stolen by a botnet will
 &gt; be more noticeable to its owner than is the case today, hence we might
 &gt; expect that in that world, users will work harder to maintain their
 &gt; computers and clean them of botnet infestations.

One more factor that would mitigate spam if POW tokens have value:
there would be a profit motive for people to set up massive
quantities of fake e-mail accounts to harvest POW tokens from
spam.  They&#39;d essentially be reverse-spamming the spammers with
automated mailboxes that collect their POW and don&#39;t read the
message.  The ratio of fake mailboxes to real people could become
too high for spam to be cost effective.

The process has the potential to establish the POW token&#39;s value
in the first place, since spammers that don&#39;t have a botnet could
buy tokens from harvesters.  While the buying back would
temporarily let more spam through, it would only hasten the
self-defeating cycle leading to too many harvesters exploiting the
spammers.

Interestingly, one of the e-gold systems already has a form of
spam called &#34;dusting&#34;.  Spammers send a tiny amount of gold dust
in order to put a spam message in the transaction&#39;s comment field.
  If the system let users configure the minimum payment they&#39;re
willing to receive, or at least the minimum that can have a
message with it, users could set how much they&#39;re willing to get
paid to receive spam.





 &gt; The last thing we need is to deploy a system designed to burn all
 &gt; available cycles, consuming electricity and generating carbon dioxide,
 &gt; all over the Internet, in order to produce small amounts of bitbux to
 &gt; get emails or spams through.
 &gt;
 &gt; Can&#39;t we just convert actual money in a bank account into bitbux --
 &gt; cheaply and without a carbon tax?  Please?

Ironic if we end up having to choose between economic liberty and
conservation.

Unfortunately, proof of work is the only solution I&#39;ve found to
make p2p e-cash work without a trusted third party.  Even if I
wasn&#39;t using it secondarily as a way to allocate the initial
distribution of currency, PoW is fundamental to coordinating the
network and preventing double-spending.

If it did grow to consume significant energy, I think it would
still be less wasteful than the labour and resource intensive
conventional banking activity it would replace.  The cost would be
an order of magnitude less than the billions in banking fees that
pay for all those brick and mortar buildings, skyscrapers and junk
mail credit card offers.

Satoshi






 &gt; BTW I don&#39;t remember if we talked about this, but the other day some
 &gt; people were mentioning secure timestamping. You want to be able to
 &gt; prove that a certain document existed at a certain time in the past.
 &gt; Seems to me that bitcoin&#39;s stack of blocks would be perfect for this.

Indeed, Bitcoin is a distributed secure timestamp server for
transactions.  A few lines of code could create a transaction with
an extra hash in it of anything that needs to be timestamped.
I should add a command to timestamp a file that way.






 From a thread on p2presearch which starts with my rant about trust 
being the root weakness of all conventional financial systems.
http://listcultures.org/pipermail/p2presearch_listcultures.org/2009-February/thread.html

I&#39;ve developed a new open source P2P e-cash system called Bitcoin.  It&#39;s
completely decentralized, with no central server or trusted parties,
because everything is based on crypto proof instead of trust.  Give it a
try, or take a look at the screenshots and design paper:

Download Bitcoin v0.1 at http://www.bitcoin.org

The root problem with conventional currency is all the trust that&#39;s
required to make it work.  The central bank must be trusted not to
debase the currency, but the history of fiat currencies is full of
breaches of that trust.  Banks must be trusted to hold our money and
transfer it electronically, but they lend it out in waves of credit
bubbles with barely a fraction in reserve.  We have to trust them with
our privacy, trust them not to let identity thieves drain our accounts.
Their massive overhead costs make micropayments impossible.

A generation ago, multi-user time-sharing computer systems had a similar
problem.  Before strong encryption, users had to rely on password
protection to secure their files, placing trust in the system
administrator to keep their information private.  Privacy could always
be overridden by the admin based on his judgment call weighing the
principle of privacy against other concerns, or at the behest of his
superiors.  Then strong encryption became available to the masses, and
trust was no longer required.  Data could be secured in a way that was
physically impossible for others to access, no matter for what reason,
no matter how good the excuse, no matter what.

It&#39;s time we had the same thing for money.  With e-currency based on
cryptographic proof, without the need to trust a third party middleman,
money can be secure and transactions effortless.

One of the fundamental building blocks for such a system is digital
signatures.  A digital coin contains the public key of its owner.  To
transfer it, the owner signs the coin together with the public key of
the next owner.  Anyone can check the signatures to verify the chain of
ownership.  It works well to secure ownership, but leaves one big
problem unsolved: double-spending.  Any owner could try to re-spend an
already spent coin by signing it again to another owner.  The usual
solution is for a trusted company with a central database to check for
double-spending, but that just gets back to the trust model.  In its
central position, the company can override the users, and the fees
needed to support the company make micropayments impractical.

Bitcoin&#39;s solution is to use a peer-to-peer network to check for
double-spending.  In a nutshell, the network works like a distributed
timestamp server, stamping the first transaction to spend a coin.  It
takes advantage of the nature of information being easy to spread but
hard to stifle.  For details on how it works, see the design paper at
http://www.bitcoin.org/bitcoin.pdf

The result is a distributed system with no single point of failure.
Users hold the crypto keys to their own money and transact directly with
each other, with the help of the P2P network to check for double-spending.

Satoshi Nakamoto
http://www.bitcoin.org





Martien van Steenbergen Martien at AardRock.COM
Thu Feb 12 08:40:53 CET 2009

Very interesting. Is this akin to David Chaum&#39;s anonymous digital
money? His concept makes sure money is anonymous unless it is
compromised, i.e. the same money spent more than once. As soon as it&#39;s
compromised, the ‘counterfeiter’ is immediately publicly exposed.

Also, in bitcoin, is there a limited supply of money (that must be
managed)? Or is money created exaclty at the moment of transaction?

Succes en plezier,

Martien.





Martien van Steenbergen wrote:
 &gt; Very interesting. Is this akin to David Chaum&#39;s anonymous digital money?
 &gt; His concept makes sure money is anonymous unless it is compromised, i.e.
 &gt; the same money spent more than once. As soon as it&#39;s compromised, the
 &gt; ‘counterfeiter’ is immediately publicly exposed.

It&#39;s similar in that it uses digital signatures for coins, but different
in the approach to privacy and preventing double-spending.  The
recipient of a Bitcoin payment is able to check whether it is the first
spend or not, and second-spends are not accepted.  There isn&#39;t an
off-line mode where double-spenders are caught and shamed after the
fact, because that would require participants to have identities.

To protect privacy, key pairs are used only once, with a new one for
every transaction.  The owner of a coin is just whoever has its private key.

Of course, the biggest difference is the lack of a central server.  That
was the Achilles heel of Chaumian systems; when the central company shut
down, so did the currency.

 &gt; Also, in bitcoin, is there a limited supply of money (that must be
 &gt; managed)? Or is money created exaclty at the moment of transaction?

There is a limited supply of money.  Circulation will be 21,000,000
coins.  Transactions only transfer ownership.

Thank you for your questions,

Satoshi





Martien van Steenbergen wrote:
 &gt; Reminds me of:
 &gt;
 &gt;     * AardRock » Wizard Rabbit Treasurer
 &gt;       &lt;http://wiki.aardrock.com/Wizard_Rabbit_Treasurer&gt;; and
 &gt;     * AardRock » Pekunio &lt;http://wiki.aardrock.com/Pekunio&gt;

Indeed, it is much like Pekunio in the concept of spraying redundant
copies of every transaction to a number of peers on the network, but the
implementation is not a reputation network like Wizard Rabbit Treasurer.
   In fact, Bitcoin does not use reputation at all.  It sees the network
as just a big crowd and doesn&#39;t much care who it talks to or who tells
it something, as long as at least one of them relays the information
being broadcast around the network.  It doesn&#39;t care because there&#39;s no
way to lie to it.  Either you tell it crypto proof of something, or it
ignores you.

 &gt; Are you familiar with Ripple?

As trust systems go, Ripple is unique in spreading trust around rather
than concentrating it.

[I&#39;ve been asked at least 4 other times &#34;have you heard of Ripple?&#34;]




Michel Bauwens wrote:
 &gt; how operational is your project? how soon do you think people will be
 &gt; able to use it in real life?

It&#39;s fully operational and the network is growing.  If you try the
software, e-mail me your Bitcoin address and I&#39;ll send you a few coins.

We just need to spread the word and keep getting more people interested.





Here&#39;s a link to the original introduction of the paper on the 
Cryptography mailing list.  (Inflation issues were superseded by changes 
I made later to support transaction fees and the limited circulation 
plan.  This link is a moving target, this archive page is just a certain 
number of days back and the discussion will keep scrolling off to the 
next page.)
http://www.mail-archive.com/cryptography@metzdowd.com/mail3.html

A little follow up when the software was released.
http://www.mail-archive.com/cryptography@metzdowd.com/mail2.html

My description of how Bitcoin solves the Byzantine Generals&#39; problem:
http://www.bitcoin.org/byzantine.html
