# https://hub.docker.com/r/library/python/tags/
FROM python:3-onbuild  

# Coping source in current directory into the image
# python:3-onbuild expects the source in /usr/src/app
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt

# Commands in a list
CMD ["python","main.py"]

Skip to content
Search or jump to…

Pull requests
Issues
Marketplace
Explore
 
@ShivamTripathi21 
schollz
/
progressbar
21
1.1k
64
 Code
 Issues 2
 Pull requests 1 Actions
 Security 0
 Insights
Progressbar in docker container #64
 Open	Bird87ZA opened this issue 21 days ago · 4 comments
Comments
@Bird87ZA
 
Bird87ZA commented 21 days ago
Not so much a bug as a request to see if someone can assist.

I have the progress bar in my app. If I run my app using go run main.go it works fine. However, if I run docker-container up --build it doesn't show the progress bar until it reaches 100%.

Does anyone know how what I should change to make it show the progress bar?

@schollz
 
Owner
schollz commented 21 days ago
@Bird87ZA Do you have a minimal example you can share?

@Bird87ZA
 
Author
Bird87ZA commented 21 days ago
This is how my docker is set up:

#docker-compose.yml
version: "3.4"

services:
  app:
    build:
      context: .
      target: app
    ports:
      - 8080:8080
    env_file:
      - .env
#Dockerfile
### Base
FROM golang AS base

WORKDIR /app

ENV CGO_ENABLED=0 \
    GOOS=linux \
    GOARCH=amd64

### Builder
FROM base as builder

COPY . .

RUN go build -mod=vendor

### App
FROM gcr.io/distroless/static as app
COPY --from=builder /app/so-kafka-migration-tool /so-kafka-migration-tool

ENTRYPOINT ["/so-kafka-migration-tool"]
Then this is my main.go file:

package main

import (
	"github.com/k0kubun/go-ansi"
	"github.com/schollz/progressbar/v3"
	"time"
)

func main() {
	bar := progressbar.NewOptions(
		100,
		progressbar.OptionSetWidth(30),
		progressbar.OptionSetWriter(ansi.NewAnsiStdout()),
		progressbar.OptionEnableColorCodes(true),
		progressbar.OptionSetDescription("[blue]Writing To SO Kafka...[reset]"),
		progressbar.OptionSetTheme(progressbar.Theme{
			Saucer:        "[green]=[reset]",
			SaucerHead:    "[green]>[reset]",
			SaucerPadding: " ",
			BarStart:      "[",
			BarEnd:        "]",
		}),
	)
	for i := 0; i < 100; i++ {
		bar.Add(1)
		time.Sleep(40 * time.Millisecond)
	}
}
If I run it with go run main.go it works perfectly.

If I run it with docker-compose up --build it doesn't show the progress bar until it's 100%.

@schollz
 
Owner
schollz commented 20 days ago
It might be a docker-compose thing. Have you tried in just docker, using the TTY flag?

@schollz
 
Owner
schollz commented 20 days ago
I couldn't get your example to work, but this works fine:

# Dockerfile
FROM golang AS builder

WORKDIR /app

COPY . .

RUN go mod init test.com/m1
RUN go build -v

FROM alpine:latest
COPY --from=builder /app/m1 /m1
ENTRYPOINT ["/m1"]
Using your main.go in the same folder:

docker build -t test1 .
docker run test`
and it shows the progress.

@ShivamTripathi21
 
 
Leave a comment

Attach files by dragging & dropping, selecting or pasting them.
Remember, contributions to this repository should follow our GitHub Community Guidelines.
Assignees
No one assigned
Labels
None yet
Projects
None yet
Milestone
No milestone
Linked pull requests
Successfully merging a pull request may close this issue.

None yet
Notifications
Customize
You’re not receiving notifications from this thread.
2 participants
@Bird87ZA
@schollz
© 2020 GitHub, Inc.
Terms
Privacy
Security
Status
Help
Contact GitHub
Pricing
API
Training
Blog
About


Wikipedia:Wikipedia logos
From Wikipedia, the free encyclopedia
Jump to navigationJump to search
Not to be confused with Wikimedia logos.
Not to be confused with Using logos on Wikipedia.
	This page in a nutshell: Wikipedia had a series of logos before the current puzzle ball was created.	Shortcuts
WP:WPLOGO
WP:WPLOGOS

The current Wikipedia logo, "v2", was unveiled in May 2010
Wikipedia had a series of logos in its history before arriving at the current puzzle logo.


Contents
1	The first official logo
2	The second logo
2.1	International adaptations
3	The third logo (the puzzle ball)
3.1	The international contest
3.2	The variants
3.3	The finalized logo
3.3.1	Alphabets represented in the logo
3.4	The May 2010 redesign
3.4.1	The characters of the v2 logo
4	10th anniversary logo
5	3D versions
5.1	Physical versions
6	See also
7	Notes and references
8	External links
The first official logo

The first Wikipedia logo
Wikipedia's first true logo was an image that was originally submitted by Bjørn Smestad[1] for a Nupedia logo competition which took place in 2000.[2] Jimmy Wales (Jimbo) thought it would be a much better logo than the flag,[citation needed] and it remained for the next eight months, until the end of 2001. It continued to be used after this time on Special Pages, such as search results.

The logo included a quote from the preface of Euclid and his Modern Rivals by Lewis Carroll; due to the fisheye effect, only part of the text can be read:

In one respect this book is an experiment, and may chance to prove a failure: I mean that I have not thought it necessary to maintain throughout the gravity of style which scientific writers usually affect, and which has somehow come to be regarded as an ‘inseparable accident’ of scientific teaching. I never could quite see the reasonableness of this immemorial law: subjects there are, no doubt, which are in their essence too serious to admit of any lightness of treatment – but I cannot recognise Geometry as one of them. Nevertheless it will, I trust, be found that I have permitted myself a glimpse of the comic side of things only at fitting seasons, when the tired reader might well crave a moment’s breathing-space, and not on any occasion where it could endanger the continuity of the line of argument.

The second logo

The second Wikipedia logo
In November 2001, Wikipedians began suggesting new logos. A short list of 24 leading candidates was chosen in the first Wikipedia logo contest, which took place from November to December 2001. The winner was the last logo (#24), contributed by The Cunctator.

The logo included the following quote, taken from Thomas Hobbes's Leviathan, Part I, Chapter VI:

Desire to know why, and how, curiosity; such as is in no living creature but man: so that man is distinguished, not only by his reason, but also by this singular passion from other animals; in whom the appetite of food, and other pleasures of sense, by predominance, take away the care of knowing causes; which is a lust of the mind, that by a perseverance of delight in the continual and indefatigable generation of knowledge, exceedeth the short vehemence of any carnal pleasure.

International adaptations
Because of its English text, this logo was not ideal for the Wikipedias in other languages. Some wikis chose a similar design with text in their own languages (e.g. the Dutch Wikipedia that used a text from the classic book Max Havelaar). Others used the English logo but added the color of a national flag (most of the Nordic language projects, Danish, for example) or simply a translation of "The Free Encyclopedia" (e.g. German). Still others designed a completely different logo (e.g. the French Wikipedia).

The third logo (the puzzle ball)
The international contest

Paul Stansifer's contest-winning puzzle ball logo
Following a suggestion by Erik Möller, an International logo contest was conducted to find a new logo that was suitable for all languages. After a two-stage vote, a design by Paul Stansifer (at the time known as Paullusmagnus) won with considerable support. The English Wikipedia switched to it on September 26, 2003.

Stansifer's logo depicted a globe constructed of puzzle pieces, of multiple colors. Covered by text with links, the logo was to symbolize the continuous construction and development of the project. The logo was made in POV-Ray, using a puzzle image wrapped around a sphere. The .pov file is available here.

The variants

David Friedland's "silver ball" logo.

Typeball of an IBM Selectric electric typewriter.
A ratification vote was held soon after, to confirm community consensus. As a result, twelve direct adaptations of the design were created by members of the community.

One of David Friedland's (Nohat) modifications, occasionally referred to as the "silver ball", was soon chosen. The revision of Stansifer's concept removed the color and changed the overlaid text into one letter or symbol per puzzle piece. Both Friedland and Stansifer have assigned copyrights to the logo to the Wikimedia Foundation.

Whilst symbolizing a globe the new logo also loosely resembled a typeball as used in some electric typewriters, a former metaphor for the liberation of the process of professional writing.

The finalized logo
Main article: Wikipedia logo

The third Wikipedia logo, with a caption in Hoefler Text Small caps.
There was some controversy over switching the English Wikipedia to this logo for several reasons, one of which was the fact Wikipedia's servers were flickering throughout most of the process.

Before being released to all Wikipedias, the logo was lightened up slightly.

After the John Seigenthaler, Sr. Wikipedia biography controversy, a column in The Times[3] insinuated the logo as being a metaphor for the entire project. Rosemary Righter wrote "Just above the omega, at the point where, on human heads, they used to perform frontal lobotomies, bits of the jigsaw are missing."

Alphabets represented in the logo

The symbols in the Wikipedia logo, without the background.
The puzzle logo includes 16 letters from 16 different alphabets, many of which—but not all—represent a letter from that alphabet that most closely resembles the English "W", as in "Wikipedia". The alphabets represented are as follows:

Code2000 Armenian ini.svg
Armenian ini
(Ի)	N/A	N/A	N/A
Code2000 Khmer lo.svg
Khmer lô
(ល)	N/A	Code2000 Japanese wa+i.svg
Japanese Katakana wa + i
(ワィ)[4]	Code2000 Klingon r.svg
Klingon r
()[5]
Tibetan wa + (i).svg
Tibetan wa + i
(ཝི)	Code2000 Greek omega.svg
Greek omega or omega+tonos
(Ω or Ώ)	Wikipedia's W.svg
Latin W
(W)	Code2000 Arabic yeh.svg
Arabic yeh
(ي)
Code2000 Devanagari va+i.svg
Devanagari va + i
(वि)[6]	Code2000 Chinese radical 145+5.svg
Chinese radical 145 (衣/衤)+5 more strokes in 且
(袓)	Code2000 Cyrillic i.svg
Cyrillic I or Short I
(И or Й)[7]	Hangul wi.svg
Korean Hangul wi
(위)
Code2000 Mongolian Todo I.svg
Mongolian Todo I (rotated 90 degrees)
(ᡅ)	Code2000 Kannada va+i.svg
Kannada va + i
(ವಿ)[8]	Code2000 Hebrew resh.svg
Hebrew resh
(ר)	Code2000 Thai cho ching.svg
Thai cho ching
(ฉ)
There have, over the years, been suggestions that some of these characters should be changed to reflect the actual spellings of "Wikipedia" in various languages.[9]

The May 2010 redesign

The current logo with the new typeface, Linux Libertine.
In late 2009, the Wikimedia Foundation undertook to fix some errors that had been noted in the design of the puzzle globe. In particular, it did not scale well and some letters appeared distorted.[10] For the new logo, the Wikimedia Foundation defined which characters appear on the "hidden" puzzle pieces, and had a three-dimensional computer model of the globe created to allow the generation of other views.

The new logo was unveiled in May 2010. It is commonly referred to as "v2" or "2.0", since it represents the second (official) version of the puzzle globe logo to be adopted. It features the new 3D rendering of the puzzle globe, with corrected characters (and the Klingon character replaced by a Geʿez character). The wordmark has been modified from the Hoefler Text font to the open-source Linux Libertine font, and the subtitle is no longer italicized.

The Wikimedia blog has more information on the unveiling, and the WMF Wiki has more detailed information on the new logo.

The characters of the v2 logo
N/A	N/A	N/A	
N/A	N/A	N/A	
N/A	N/A	N/A	N/A	Վ.svg
Armenian vev
(Վ)	N/A	N/A	N/A	N/A	N/A
N/A	N/A	N/A	Telugu va + (i).svg
Telugu va + (i)
(వి)	Khmer vo+i.svg
Khmer vo + i
(វិ)	N/A	Katakana u and small i serif 1.svg
Katakana u + small i
(ウィ)	ው.svg
Gəʿəz wə
(ው)	N/A	N/A
Javanese wa + i.svg
Javanese wa + i
(ꦮꦶ)	Gujarati va + i.svg
Gujarati va + i
(વિ)	Gothic winja.svg
Gothic vinja
(𐍅)	Hoeffler É.svg
Latin E-acute
(É)	Bengali rhoshsho u.svg
Bengali short u
(উ)	Greek uc Omega.svg
Greek omega
(Ω)	Wikipedia's W.svg
Latin W
(W)	و.svg
Arabic wāw
(و)	Gurmukhi vava + sihari.svg
Gurmukhī vava + sihari
(ਵਿ)	the last LETTER of most Wikipedias using the Cyrillic Alphabet [citation needed]
Cyrillic ya
(Я)
Syriac waw.svg
Syriac wāw
(ܘ)	Lontara w + i.svg
Lontara w + i
(ᨓᨗ)	Odia character ଉ.svg
Oriya U
(ଉ)	Burmese v + i.svg
Burmese script v + i
(ဝီ)	वि.svg
Devanagari va + i
(वि)	維 GungSeo.svg
Traditional Chinese
(維)	Cyrillic И.svg
Cyrillic i
(И)	Hangul wi serif.svg
Hangul/Chosongul wi
(위)	Tāna vaavu + vowel i.svg
Tāna vaavu + (i)
(ވި)	Laotian w + i.svg
Laotian w + i
(ວິ)
Cyrillic В.svg
Cyrillic ve
(В)	Glagolitic vede.svg
Glagolitic vědě
(Ⰲ)	Malayalam va + short i.svg
Malayalam va + short i
(വി)	Inuktitut u.svg
Inuktitut short u
(ᐅ)	Georgian ვ.svg
Georgian vin
(ვ)	Kannada va + (i).svg
Kannada va + (i)
(ವಿ)	Hebrew vav.svg
Hebrew vav
(ו)	Thai wo waen.svg
Thai wo waen + sara i
(วิ)	used in Nahuatl wikipedia
Latin H
(H)	Cyrillic У.svg
Cyrillic u
(У)
Tagalog wi
Tagalog Baybayin wi
(ᜏᜒ)	Hoeffler U.svg
Latin U
(U)	Mongolian wa.svg
Mongolian wa
(ᠸ)	Limbu wi
Limbu wa + i
(ᤘᤡ)	Cherokee wi.svg
Cherokee wi
(Ꮻ)	Tibetan wa + (i).svg
Tibetan wa + (i)
(ཝི)	Tamil va + (i).svg
Tamil va + (i)
(வி)	Sinhala va + i.svg
Sinhala va + i
(වි)	Hoeffler Ä.svg
Latin A-umlaut
(Ä)	Classical 典.svg
Chinese character
(典)
Tai Le wa
Tai Nüa wa
(ᥝ)	Hoeffler V.svg
Latin V
(V)	Cyrillic Д.svg
Cyrillic de
(Д)	
Greek pi.svg
Greek pi
(Π)	Arabic yodh aleph.svg
Arabic yāʾ + ʾalif
(يا)	Hoeffler İ.svg
Latin dotted I
(İ)	
10th anniversary logo

Tenth anniversary logo, which replaced the puzzle ball logo across Wikipedia on January 15, 2011.
On January 15, 2011, a special logo replaced the standard globe in order to mark the tenth anniversary of Wikipedia's founding. The logo depicts a single jigsaw piece, representing the addition of another piece to the puzzle.

3D versions
File:Wikipedia logo puzzle globe spins horizontally and vertically, revealing the contents of all of its puzzle pieces (4K resolution) (VP9).webm
3D Wikipedia puzzle ball rotating along its axes (GIF version)
The first two versions of the logo were made to resemble a globe by the use of the fish-eye effect.

The third version (puzzle ball logo) was made in POV-Ray, a ray tracing program which generates 2D images from a 3D scene description. The original 3D scene consisted of a sphere on which a puzzle image was projected, as described here. Nohat's version introduced a bump map to the setup, to provide 3D relief and simulate separate puzzle pieces.

A truly tridimensional model has been created, with each puzzle piece sculpted independently, to allow alternative renderings. It is available on GitHub in an animated version and a 3D printable version.

See also the thread What is on the back of the logo? at the foundation-l mailing list.

Physical versions

A concrete version of the logo being lowered into Lake Sevan in Armenia to create an artificial reef

 

Wikipedia jack-o-lantern

 

Puzzle ball distributed to Wikimania 2007 attendees

 

A 3D printed globe

A very large puzzle globe, dubbed the Wikiball, featured in Wikimania 2007, depicted an approximation of the Wikipedia logo. A smaller version was distributed to the participants. The large ball was dismantled after the closing ceremony, and many participants kept a piece or more of the puzzle.

The Wikipedia logo has also been carved into a jack-o-lantern.

In 2017, a concrete version of the logo was submerged in Lake Sevan to create an artificial reef.[11]

See also
Wikipedia logo
commons:Category:Characters in the Wikipedia logo
meta:Logo history
meta:Errors in the Wikipedia logo
meta:Logos
User talk:Nohat/archive_2005-02-22#Logo
Wikipedia:Banners and buttons
Wikipedia:Slogans
List of writing systems
Content guideline: using logos on Wikipedia
Notes and references
 Bjørn Smestad created the first Wikipedia logo according to this archived page of submitted logos from Nupedia site - as is seen in that page at the bottom "Logo ideas posted with permission of their designers. Click on a logo to go to its designer's website." Image link in that page is pointing to this archived page: "Assistant Professor Bjørn Smestad".
 "User talk:Mosca: Difference between revisions". wikipedia.org.
 Righter, Rosemary (9 December 2005). "Unreliable (adj): log on and see". Times Online.
 Apparently a typing error for u & small i (ウィ). This should be ウィ(pronounced as wi): ウ(u) and ワ(wa) are different letters. ヰ in David Friedland's puzzle ball logo is an old Japanese Kana character pronounced as wi, but this letter is not used now. See also: commons:Category:Japanese character for Wikipedia logo
 This character is in the Private Use Area area of Unicode and may not display without the correct fonts. It is registered in the ConScript Unicode Registry, thus fonts which follow the CSUR should function correctly.
 Due to a formatting error, the characters are reversed on the globe image, showing as (व​ि). There are problems with this in some web browsers as well.
 Given as capital i (И) in some logos; see User talk:Nohat for more information.
 This is a Kannada va with a i diacritic vowel on top. The diacritic was attached to the wrong place by the font used. It should have been rendered as ವಿ. See http://bachodi.wordpress.com/2007/06/30/a-typo-in-wikipedia-logo-fractures-the-kannada-too/
 m:Talk:Errors in the Wikipedia logo
 UnderConsideration LLC. "Brand New: Around the World in 51 Characters". underconsideration.com.
 "CEE/Newsletter/October 2017/Full - Meta". meta.wikimedia.org. Retrieved 22 April 2020.
External links
	Wikimedia Commons has media related to Wikipedia logos.
Some Errors Defy Fixes: A Typo in Wikipedia’s Logo Fractures the Sanskrit — June 25, 2007. The New York Times.
Categories: Wikipedia images
Navigation menu
Not logged inTalkContributionsCreate accountLog in
Project pageTalk
ReadEditView historySearch
Search Wikipedia
Main page
Contents
Featured content
Current events
Random article
Donate to Wikipedia
Wikipedia store
Interaction
Help
About Wikipedia
Community portal
Recent changes
Contact page
Tools
What links here
Related changes
Upload file
Special pages
Permanent link
Page information
Wikidata item
In other projects
Wikimedia Commons
Wikiversity
Print/export
Download as PDF
Printable version

Languages
العربية
Bahasa Indonesia
Jawa
日本語
Русский
اردو
中文
5 more
Edit links
This page was last edited on 22 April 2020, at 06:45 (UTC).
Text is available under the Creative Commons Attribution-ShareAlike License; additional terms may apply. By using this site, you agree to the Terms of Use and Privacy Policy. Wikipedia® is a registered trademark of the Wikimedia Foundation, Inc., a non-profit organization.
Privacy policyAbout WikipediaDisclaimersDevelopersStatisticsCookie statementMobile viewContact WikipediaWikimedia FoundationPowered by MediaWiki

