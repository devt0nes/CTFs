# Cryptography

Jump to:
- [substitution0](#substitution0)
- [substitution1](#substitution1)
- [substitution2](#substitution2)
- [la cifra de](#la-cifra-de)
- [Mini RSA](#mini-rsa)
- [Sum-o-Primes](#sum-o-primes)
- [No Padding, No Problem](#no-padding-no-problem)
- [SRA](#sra)

## substitution0
<a name="substitution0"></a>

### Challenge
A message has come in but it seems to be all scrambled. Luckily it seems to have the key at the beginning. Can you crack this substitution cipher?  
Download the message [here](https://artifacts.picoctf.net/c/154/message.txt).

### Solving
The **txt** file given contains:
```
ZGSOCXPQUYHMILERVTBWNAFJDK 

Qctcnrel Mcptzlo ztebc, fuwq z ptzac zlo bwzwcmd zut, zlo gtenpqw ic wqc gccwmc
xtei z pmzbb szbc ul fqusq uw fzb clsmebco. Uw fzb z gcznwuxnm bsztzgzcnb, zlo, zw
wqzw wuic, nlhlefl we lzwntzmubwb—ex sentbc z ptczw rtukc ul z bsuclwuxus reulw
ex aucf. Wqctc fctc wfe tenlo gmzsh brewb lczt elc cjwtciuwd ex wqc gzsh, zlo z
melp elc lczt wqc ewqct. Wqc bszmcb fctc cjsccoulpmd qzto zlo pmebbd, fuwq zmm wqc
zrrcztzlsc ex gntlubqco pemo. Wqc fcupqw ex wqc ulbcsw fzb actd tcizthzgmc, zlo,
wzhulp zmm wqulpb ulwe selbuoctzwuel, U senmo qztomd gmzic Ynruwct xet qub eruluel
tcbrcswulp uw.

Wqc xmzp ub: ruseSWX{5NG5717N710L_3A0MN710L_357GX9XX}
```
From the statement we know the message is encrypted with a simple substitution cipher, and that the key (the substituted alphabet) is at the start of the given message, which would be `ZGSOCXPQUYHMILERVTBWNAFJDK` (Note: in an alphabetical substitution cipher, when encrypting, each letter in the ciphertext is swapped with the letter in the substitution alphabet that is at the same alphabetical position).  

To decode this, we can use the [Cryptii's alphabetical substitution tool](https://cryptii.com/pipes/alphabetical-substitution).  
On putting the key as the Ciphertext Alphabet and entering the rest of the message as the Ciphertext and hitting Decode, we get:
```
Hereupon Legrand arose, with a grave and stately air, and brought me the beetle
from a glass case in which it was enclosed. It was a beautiful scarabaeus, and, at
that time, unknown to naturalists—of course a great prize in a scientific point
of view. There were two round black spots near one extremity of the back, and a
long one near the other. The scales were exceedingly hard and glossy, with all the
appearance of burnished gold. The weight of the insect was very remarkable, and,
taking all things into consideration, I could hardly blame Jupiter for his opinion
respecting it.

The flag is: picoCTF{5UB5717U710N_3V0LU710N_357BF9FF}
```
Flag Obtained!

### Flag
> picoCTF{5UB5717U710N_3V0LU710N_357BF9FF}

## substitution1
<a name="substitution1"></a>

### Challenge
A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again.  
Download the message [here](https://artifacts.picoctf.net/c/183/message.txt).

### Solving
The **txt** file given contains:
```
LKOb (bwvek ove lgqkhej kwj osgx) gej g kyqj vo lvrqhkje bjlhetky lvrqjktktvu. Lvukjbkgukb gej qejbjukjz dtkw g bjk vo lwgssjuxjb dwtlw kjbk kwjte lejgktftky, kjlwutlgs (guz xvvxstux) bitssb, guz qevmsjr-bvsftux gmtstky. Lwgssjuxjb hbhgssy lvfje g uhrmje vo lgkjxvetjb, guz dwju bvsfjz, jglw ytjszb g bketux (lgssjz g osgx) dwtlw tb bhmrtkkjz kv gu vustuj blvetux bjeftlj. LKOb gej g xejgk dgy kv sjgeu g dtzj geegy vo lvrqhkje bjlhetky bitssb tu g bgoj, sjxgs juftevurjuk, guz gej wvbkjz guz qsgyjz my rguy bjlhetky xevhqb gevhuz kwj dvesz ove ohu guz qeglktlj. Ove kwtb qevmsjr, kwj osgx tb: qtlvLKO{OE3AH3ULY_4774LI5_4E3_L001_6J0659OM}
```
From the statement we can tell its another alphabetical substition cipher (which we can confirm by analysing it using [Boxentriq's Cipher Identifier](https://www.boxentriq.com/code-breaking/cipher-identifier)). However this time we haven't been given the key, so we can't decode it directly.  
Now in such a case we can do a frequency analysis of the text (which is also suggested by one of the hints). For which we can use [this tool](https://www.101computing.net/frequency-analysis/) by **101computing.net** (alternatively, we can also use **Cypto Corner**'s [tool](https://crypto.interactive-maths.com/frequency-analysis-breaking-the-code.html) for the same). Using it gives us:  

<br><img src="img/substitution1(1).png" alt="frequency analysis" width="900"/><br><br>

The tool also allows us to try substituting the encoded letters:  
1. `qtlvLKO{OE3AH3ULY_4774LI5_4E3_L001_6J0659OM}` is definitely the flag, which would mean it's in the format of `picoCTF{...}`. So we can substitute-
    - q -> p
    - t -> i
    - l -> c
    - v -> o
    - L -> C
    - K -> T
    - O -> F
2. Since `g` appears as a single-letter word multiple times, we can substitute-
    - g -> a
3. `tb` also appears multiple times, and as `t` is `i`, the word must be `is`, so-
    - b -> s

Continuing this way, we are able to find the substitution for the whole text:  

<br><img src="img/substitution1(2).png" alt="alphabetical substitution" width="900"/><br><br>

The key we finally get is `QS*WRVAUKETCB*F*PMLINOHGYD` (The '*'s indicate unknown letters J, X, and Z which we cannot substitute as they haven't been used in the ciphertext), and the decrypted message:
```
CTFS (SHORT FOR CAPTURE THE FLAG) ARE A TYPE OF COMPUTER SECURITY COMPETITION. CONTESTANTS ARE PRESENTED WITH A SET OF CHALLENGES WHICH TEST THEIR CREATIVITY, TECHNICAL (AND GOOGLING) SKILLS, AND PROBLEM-SOLVING ABILITY. CHALLENGES USUALLY COVER A NUMBER OF CATEGORIES, AND WHEN SOLVED, EACH YIELDS A STRING (CALLED A FLAG) WHICH IS SUBMITTED TO AN ONLINE SCORING SERVICE. CTFS ARE A GREAT WAY TO LEARN A WIDE ARRAY OF COMPUTER SECURITY SKILLS IN A SAFE, LEGAL ENVIRONMENT, AND ARE HOSTED AND PLAYED BY MANY SECURITY GROUPS AROUND THE WORLD FOR FUN AND PRACTICE. FOR THIS PROBLEM, THE FLAG IS: PICOCTF{FR3QU3NCY_4774CK5_4R3_C001_6E0659FB}
```
Flag Obtained!

P.S.: Rather than manually finding all the substitutions, we can also use [DCode's Mono-alphabetic Substitution tool](https://www.dcode.fr/monoalphabetic-substitution) or [Boxentriq's Cryptogram Solver](https://www.boxentriq.com/code-breaking/cryptogram) which would do the bulk of the work for us and help save quite some time.

### Flag
> PICOCTF{FR3QU3NCY_4774CK5_4R3_C001_6E0659FB}

## substitution2
<a name="substitution2"></a>

### Challenge
It seems that another encrypted message has been intercepted. The encryptor seems to have learned their lesson though and now there isn't any punctuation! Can you still crack the cipher?  
Download the message [here](https://artifacts.picoctf.net/c/114/message.txt).

### Solving
The **txt** file given contains:
```
fnjdjjzqsfsjpjdxwmfnjdcjwwjsfxhwqsnjynqensknmmwkmuvafjdsjkadqftkmuvjfqfqmgsqgkwayqgekthjdvxfdqmfxgyaskthjdknxwwjgejfnjsjkmuvjfqfqmgslmkasvdquxdqwtmgstsfjusxyuqgqsfdxfqmglagyxujgfxwscnqknxdjpjdtasjlawxgyuxdojfxhwjsoqwwsnmcjpjdcjhjwqjpjfnjvdmvjdvadvmsjmlxnqensknmmwkmuvafjdsjkadqftkmuvjfqfqmgqsgmfmgwtfmfjxknpxwaxhwjsoqwwshafxwsmfmejfsfayjgfsqgfjdjsfjyqgxgyjzkqfjyxhmafkmuvafjdskqjgkjyjljgsqpjkmuvjfqfqmgsxdjmlfjgwxhmdqmasxllxqdsxgykmujymcgfmdaggqgeknjkowqsfsxgyjzjkafqgekmglqeskdqvfsmlljgsjmgfnjmfnjdnxgyqsnjxpqwtlmkasjymgjzvwmdxfqmgxgyquvdmpqsxfqmgxgymlfjgnxsjwjujgfsmlvwxtcjhjwqjpjxkmuvjfqfqmgfmaknqgemgfnjmlljgsqpjjwjujgfsmlkmuvafjdsjkadqftqsfnjdjlmdjxhjffjdpjnqkwjlmdfjknjpxgejwqsufmsfayjgfsqgxujdqkxgnqensknmmwsladfnjdcjhjwqjpjfnxfxgagyjdsfxgyqgemlmlljgsqpjfjkngqiajsqsjssjgfqxwlmdumagfqgexgjlljkfqpjyjljgsjxgyfnxffnjfmmwsxgykmglqeadxfqmglmkasjgkmagfjdjyqgyjljgsqpjkmuvjfqfqmgsymjsgmfwjxysfayjgfsfmogmcfnjqdjgjutxsjlljkfqpjwtxsfjxknqgefnjufmxkfqpjwtfnqgowqojxgxffxkojdvqkmkflqsxgmlljgsqpjwtmdqjgfjynqensknmmwkmuvafjdsjkadqftkmuvjfqfqmgfnxfsjjosfmejgjdxfjqgfjdjsfqgkmuvafjdskqjgkjxumgenqensknmmwjdsfjxknqgefnjujgmaenxhmafkmuvafjdsjkadqftfmvqiajfnjqdkadqmsqftumfqpxfqgefnjufmjzvwmdjmgfnjqdmcgxgyjgxhwqgefnjufmhjffjdyjljgyfnjqduxknqgjsfnjlwxeqsvqkmKFL{G6D4U_4G41T515_15_73Y10A5_42JX1770}
```
Just like the last two problems, this one is also another alphabetical substition cipher. Except this time we have neither the substitution key nor any idea of the words present in the text as all punctuation has been omitted. This makes finding all the substitions trickier, but not something we can't figure out with a bit more work.  
Performing a frequency analysis using [this tool](https://www.101computing.net/frequency-analysis/) we get:

<br><img src="img/substitution2(1).png" alt="alphabetical substitution" width="900"/><br><br>

Now, on to figuring out the substitions:
1. `vqkmKFL{G6D4U_4G41T515_15_73Y10A5_42JX1770}` present at the end is clearly the flag, which would mean it's in the format of `picoCTF{...}`. So, we can substitute-
    - v -> p
    - q -> i
    - k -> c
    - m -> o
    - K -> C
    - F -> T
    - L -> F
2. Since `J` appears significantly more than all the other letters, we can assume it to be `E` (which is the most frequently appearing letter in the English language, according to [Wikipedia's page on Letter Frequency](https://en.wikipedia.org/wiki/Letter_frequency), amongst other sources)-
    - J -> E

So far, we have:

<br><img src="img/substitution2(2).png" alt="alphabetical substitution" width="900"/><br><br>

For moving forward, I decided to try and decipher the most common digraphs and trigraphs, which are:
- TH,HE,AN,IN,ER,ON,RE,ED,ND,HA,AT,EN
- THE,AND,THA,ENT,ION,TIO,FOR,NDE,HAS,NCE,TIS,OFT,MEN  
([Source](https://crypto.interactive-maths.com/frequency-analysis-breaking-the-code.html))  

3. Since we know `F` & `J` are `T` & `E` respectively, I tried looking for 3-letter combinations that were in the form `F*J` (which we could decipher as `THE`), and the most common combination which turned up was `FNJ` (19 counts). So, we can confidently assume `N` to be `H`-
    - N -> H

Now, we have:

<br><img src="img/substitution2(3).png" alt="alphabetical substitution" width="900"/><br><br>

4. In the last line the text `THEF***I*PICOCTF{` is pretty clearly supposed to be `THEFLAGISPICOCTF{`. So, we can also substitute-
    - W -> L
    - X -> A
    - E -> G
    - S -> S

With these changes, a large chunk of the text has been deciphered at this point:

<br><img src="img/substitution2(4).png" alt="alphabetical substitution" width="900"/><br><br>

The rest of the substitutions are much easier to crack now. `SCIE*CE` should be `SCIENCE`, `CO*PETITIO*` should be `COMPETITION`, and so on.  

Continuing to decipher letters this way, we finally end up with:

<br><img src="img/substitution2(5).png" alt="alphabetical substitution" width="900"/><br><br>

The key we finally get is `U*WRGTNBQECFOHKVI*SYMPLADX` (The '*'s indicate unknown letters J and Z which we cannot substitute as they haven't been used in the ciphertext), and the decrypted message:
```
THEREEXISTSEVERALOTHERWELLESTABLISHEDHIGHSCHOOLCOMPUTERSECURITYCOMPETITIONSINCLUDINGCYBERPATRIOTANDUSCYBERCHALLENGETHESECOMPETITIONSFOCUSPRIMARILYONSYSTEMSADMINISTRATIONFUNDAMENTALSWHICHAREVERYUSEFULANDMARKETABLESKILLSHOWEVERWEBELIEVETHEPROPERPURPOSEOFAHIGHSCHOOLCOMPUTERSECURITYCOMPETITIONISNOTONLYTOTEACHVALUABLESKILLSBUTALSOTOGETSTUDENTSINTERESTEDINANDEXCITEDABOUTCOMPUTERSCIENCEDEFENSIVECOMPETITIONSAREOFTENLABORIOUSAFFAIRSANDCOMEDOWNTORUNNINGCHECKLISTSANDEXECUTINGCONFIGSCRIPTSOFFENSEONTHEOTHERHANDISHEAVILYFOCUSEDONEXPLORATIONANDIMPROVISATIONANDOFTENHASELEMENTSOFPLAYWEBELIEVEACOMPETITIONTOUCHINGONTHEOFFENSIVEELEMENTSOFCOMPUTERSECURITYISTHEREFOREABETTERVEHICLEFORTECHEVANGELISMTOSTUDENTSINAMERICANHIGHSCHOOLSFURTHERWEBELIEVETHATANUNDERSTANDINGOFOFFENSIVETECHNIQUESISESSENTIALFORMOUNTINGANEFFECTIVEDEFENSEANDTHATTHETOOLSANDCONFIGURATIONFOCUSENCOUNTEREDINDEFENSIVECOMPETITIONSDOESNOTLEADSTUDENTSTOKNOWTHEIRENEMYASEFFECTIVELYASTEACHINGTHEMTOACTIVELYTHINKLIKEANATTACKERPICOCTFISANOFFENSIVELYORIENTEDHIGHSCHOOLCOMPUTERSECURITYCOMPETITIONTHATSEEKSTOGENERATEINTERESTINCOMPUTERSCIENCEAMONGHIGHSCHOOLERSTEACHINGTHEMENOUGHABOUTCOMPUTERSECURITYTOPIQUETHEIRCURIOSITYMOTIVATINGTHEMTOEXPLOREONTHEIROWNANDENABLINGTHEMTOBETTERDEFENDTHEIRMACHINESTHEFLAGISPICOCTF{N6R4M_4N41Y515_15_73D10U5_42EA1770}
```
Flag Obtained!

P.S.: Just like in the last challenge, rather than manually finding all the substitutions, we can use [DCode's Mono-alphabetic Substitution tool](https://www.dcode.fr/monoalphabetic-substitution) or [Boxentriq's Cryptogram Solver](https://www.boxentriq.com/code-breaking/cryptogram), which still work surprisingly well, despite the lack of punctuation.

### Flag
> PICOCTF{N6R4M_4N41Y515_15_73D10U5_42EA1770}

## la cifra de
<a name="la-cifra-de"></a>

### Challenge
I found this cipher in an old book. Can you figure out what it says? Connect with `nc jupiter.challenges.picoctf.org 32411`.

### Solving
On connecting to the given port, we receive the following text:
```
Encrypted message:
﻿Ne iy nytkwpsznyg nth it mtsztcy vjzprj zfzjy rkhpibj nrkitt ltc tnnygy ysee itd tte cxjltk

Ifrosr tnj noawde uk siyyzre, yse Bnretèwp Cousex mls hjpn xjtnbjytki xatd eisjd

Iz bls lfwskqj azycihzeej yz Brftsk ip Volpnèxj ls oy hay tcimnyarqj dkxnrogpd os 1553 my Mnzvgs Mazytszf Merqlsu ny hox moup Wa inqrg ipl. Ynr. Gotgat Gltzndtg Gplrfdo

Ltc tnj tmvqpmkseaznzn uk ehox nivmpr g ylbrj ts ltcmki my yqtdosr tnj wocjc hgqq ol fy oxitngwj arusahje fuw ln guaaxjytrd catizm tzxbkw zf vqlckx hizm ceyupcz yz tnj fpvjc hgqqpohzCZK{m311a50_0x_a1rn3x3_h1ah3x7g996649}

Ehk ktryy herq-ooizxetypd jjdcxnatoty ol f aordllvmlbkytc inahkw socjgex, bls sfoe gwzuti 1467 my Rjzn Hfetoxea Gqmexyt.

Tnj Gimjyèrk Htpnjc iy ysexjqoxj dosjeisjd cgqwej yse Gqmexyt Doxn ox Fwbkwei Inahkw.

Tn 1508, Ptsatsps Zwttnjxiax tnbjytki ehk xz-cgqwej ylbaql rkhea (g rltxni ol xsilypd gqahggpty) ysaz bzuri wazjc bk f nroytcgq nosuznkse ol yse Bnretèwp Cousex.

Gplrfdo’y xpcuso butvlky lpvjlrki tn 1555 gx l cuseitzltoty ol yse lncsz. Yse rthex mllbjd ol yse gqahggpty fce tth snnqtki cemzwaxqj, bay ehk fwpnfmezx lnj yse osoed qptzjcs gwp mocpd hd xegsd ol f xnkrznoh vee usrgxp, wnnnh ify bk itfljcety hizm paim noxwpsvtydkse.
```
To identify the cipher with which the text has been encoded, I analyzed it with [DCode's Mono-alphabetic Substitution tool](https://www.dcode.fr/monoalphabetic-substitution) and [Boxentriq's Cryptogram Solver](https://www.boxentriq.com/code-breaking/cryptogram). Both returned a high probability of the *Vigenère* cipher.  
This is confirmed by searching up 'la cifra de' (the name of the challenge) which leads us to 'La Cifra del Sig. Giovan Battista Bellaso', written by Giovan Battista Bellaso, who had invented the Vigenère cipher even before Blaise de Vigenère (who had, for a long time, wrongly been attributed as the inventor).  

Since I didn't know the key, I went for the automatic decryption tool of both sites. However neither of them worked properly, only decrypting parts of the text with the rest still being gibberish. (Later I realized this was because both tools were considering '**è**' (present in the text) as '**e**' and accordingly changing it, when it actually needed to be left as is.)  

I did notice that both sites were trying keys such as 'FLAG', 'AGFL', 'GFLA', 'AGFLAGFL', 'AGFLAGFLAG', etc. So this time I went to [Cryptii's decoder](https://cryptii.com/pipes/vigenere-cipher) and tried to decipher the text with 'FLAG' as the key (since it seemed the most obvious and apt as well). And it worked, giving us the decoded message:

```
﻿It is interesting how in history people often receive credit for things they did not create

During the course of history, the Vigenère Cipher has been reinvented many times

It was falsely attributed to Blaise de Vigenère as it was originally described in 1553 by Giovan Battista Bellaso in his book La cifra del. Sig. Giovan Battista Bellaso

For the implementation of this cipher a table is formed by sliding the lower half of an ordinary alphabet for an apparently random number of places with respect to the upper halfpicoCTF{b311a50_0r_v1gn3r3_c1ph3r7b996649}

The first well-documented description of a polyalphabetic cipher however, was made around 1467 by Leon Battista Alberti.

The Vigenère Cipher is therefore sometimes called the Alberti Disc or Alberti Cipher.

In 1508, Johannes Trithemius invented the so-called tabula recta (a matrix of shifted alphabets) that would later be a critical component of the Vigenère Cipher.

Bellaso’s second booklet appeared in 1555 as a continuation of the first. The lower halves of the alphabets are now shifted regularly, but the alphabets and the index letters are mixed by means of a mnemonic key phrase, which can be different with each correspondent.
```
Flag Obtained!

### Flag
> picoCTF{b311a50_0r_v1gn3r3_c1ph3r7b996649}

## Mini RSA
<a name="mini-rsa"></a>

### Challenge
What happens if you have a small exponent? There is a twist though, we padded the plaintext so that (M ** e) is just barely larger than N. Let's decrypt this: [ciphertext](https://mercury.picoctf.net/static/e7e63a387acc347648918f419d1ae438/ciphertext)

### Solving
The file contains:
```
N: 1615765684321463054078226051959887884233678317734892901740763321135213636796075462401950274602405095138589898087428337758445013281488966866073355710771864671726991918706558071231266976427184673800225254531695928541272546385146495736420261815693810544589811104967829354461491178200126099661909654163542661541699404839644035177445092988952614918424317082380174383819025585076206641993479326576180793544321194357018916215113009742654408597083724508169216182008449693917227497813165444372201517541788989925461711067825681947947471001390843774746442699739386923285801022685451221261010798837646928092277556198145662924691803032880040492762442561497760689933601781401617086600593482127465655390841361154025890679757514060456103104199255917164678161972735858939464790960448345988941481499050248673128656508055285037090026439683847266536283160142071643015434813473463469733112182328678706702116054036618277506997666534567846763938692335069955755244438415377933440029498378955355877502743215305768814857864433151287
e: 3

ciphertext (c): 1220012318588871886132524757898884422174534558055593713309088304910273991073554732659977133980685370899257850121970812405700793710546674062154237544840177616746805668666317481140872605653768484867292138139949076102907399831998827567645230986345455915692863094364797526497302082734955903755050638155202890599808147276605782889813772992918898400408026067642464141885067379614918437023839625205930332182990301333585691581437573708925507991608699550931884734959475780164693178925308303420298715231388421829397209435815583140323329070684583974607064056215836529244330562254568162453025117819569708767522400676415959028292550922595255396203239357606521218664984826377129270592358124859832816717406984802489441913267065210674087743685058164539822623810831754845900660230416950321563523723959232766094292905543274107712867486590646161628402198049221567774173578088527367084843924843266361134842269034459560612360763383547251378793641304151038512392821572406034926965112582374825926358165795831789031647600129008730
```
The public key `(N,e)` as well as the ciphertext have been given, but not the private key or `p` and `q` (primes used to make up `N`). And factorising `N` is certainly not feasible.  
There is, however, additional info given in the problem statement- that `e` is very small (it is usually 65537 and here it is 3 instead), and that the value of `(M ** e)` is just greater than `N`.  

On digging around a bit, looking for what could be done with the two details for this ques, I learnt that a small value of `e` leaves the encryption system vulnerable. This is because if:  
1. the value of M<sup>e</sup> < N, M<sup>e</sup> mod N will just give M<sup>e</sup>, and we can just take the 'e'th root of the ciphertext (c) to get the message (M).
2. the value of M<sup>e</sup> > N, instead of directly taking the 'e'th root, we need to add integral multiples of N to the ciphertext (c) until the root gives us the correct message (M).  

([Source](https://ir0nstone.gitbook.io/crypto/rsa/public-exponent-attacks/small-e))

At first I tried adding `N` to `c` directly and taking the cube root, but it didn't give a valid answer. Neither did using the first few multiples.  
So, I made a loop to try all the possible multiples upto larger and larger numbers (was doubtful about it at first, but checking out one of the hints reassured that the approach was right) until one of them decrypted it to text containing the flag, which I verified for each iteration by searching for 'picoCTF' within the decrypted text.  

The python code for this was:
```py
from Crypto.Util.number import long_to_bytes
from sympy import integer_nthroot

N = 1615765684321463054078226051959887884233678317734892901740763321135213636796075462401950274602405095138589898087428337758445013281488966866073355710771864671726991918706558071231266976427184673800225254531695928541272546385146495736420261815693810544589811104967829354461491178200126099661909654163542661541699404839644035177445092988952614918424317082380174383819025585076206641993479326576180793544321194357018916215113009742654408597083724508169216182008449693917227497813165444372201517541788989925461711067825681947947471001390843774746442699739386923285801022685451221261010798837646928092277556198145662924691803032880040492762442561497760689933601781401617086600593482127465655390841361154025890679757514060456103104199255917164678161972735858939464790960448345988941481499050248673128656508055285037090026439683847266536283160142071643015434813473463469733112182328678706702116054036618277506997666534567846763938692335069955755244438415377933440029498378955355877502743215305768814857864433151287
c = 1220012318588871886132524757898884422174534558055593713309088304910273991073554732659977133980685370899257850121970812405700793710546674062154237544840177616746805668666317481140872605653768484867292138139949076102907399831998827567645230986345455915692863094364797526497302082734955903755050638155202890599808147276605782889813772992918898400408026067642464141885067379614918437023839625205930332182990301333585691581437573708925507991608699550931884734959475780164693178925308303420298715231388421829397209435815583140323329070684583974607064056215836529244330562254568162453025117819569708767522400676415959028292550922595255396203239357606521218664984826377129270592358124859832816717406984802489441913267065210674087743685058164539822623810831754845900660230416950321563523723959232766094292905543274107712867486590646161628402198049221567774173578088527367084843924843266361134842269034459560612360763383547251378793641304151038512392821572406034926965112582374825926358165795831789031647600129008730
e = 3

for i in range(5000):
    ct = c + i * N
    m = integer_nthroot(ct, 3)[0]
    flag = long_to_bytes(m)

    if b'picoCTF' in flag:
        print(flag.decode())
        break
```
Giving a range of 5000 was more than sufficient as it was the 3533rd multiple of `N` that was required to decipher the ciphertext and give us:
```
                                                                                                        picoCTF{e_sh0u1d_b3_lArg3r_85d643d5}
```
Flag Obtained!

### Flag
> picoCTF{e_sh0u1d_b3_lArg3r_85d643d5}

## Sum-O-Primes
<a name="sum-o-primes"></a>

### Challenge
We have so much faith in RSA we give you not just the product of the primes, but their sum as well!
* [gen.py](https://artifacts.picoctf.net/c/97/gen.py)
* [output.txt](https://artifacts.picoctf.net/c/97/output.txt)

### Solving
From the output.txt file, we have:
```
x = 152a1447b61d023bebab7b1f8bc9d934c2d4b0c8ef7e211dbbcf841136d030e3c829f222cec318f6f624eb529b54bcda848f65574896d70cd6c3460d0c9064cd66e826578c2035ab63da67d069fa302227a9012422d2402f8f0d4495ef66104ebd774f341aa62f493184301debf910ab3d1e72e357a99c460370254f3dfccd9ae
n = 6fc1b2be753e8f480c8b7576f77d3063906a6a024fe954d7fd01545e8f5b6becc24d70e9a5bc034a4c00e61f8a6176feb7d35fe39c8c03617ea4552840d93aa09469716913b58df677c785cd7633d1b7d31e2222cab53be235aa412ac5c5b07b500cf3fd5d6b91e2ddc51bff1e6eec2cb68723af668df36e10e332a9cbb7f3e2df9593fa0e553ed58afec2aa3bc4ae8ef1140e4779f61bdeae4c0b46136294cf151622e83c3d71b97c815b542208baa28207225f134c5a4feac998aeb178a5552f08643717819c10e8b5ec7715696c3bf4434fbea8e8a516dfd90046a999e24a0fb10d27291eb29ef3f285149c20189e7d0190417991094948180196543b8c91
c = 16acf84a73cefd321ed491a15c640a495b09050cdce435ec37442faf9a694775e1ebffb6dbad6133cbc54e3f641506b0613f711625594fcb467f915f2708714b4c9936f5f4752c3299157cff4eb68eb82c0054dae351314829974f4feadaf126cda92b97e348dbef2640ec3a729a064e615df73d644700f93bf87579683e253d29622525bea3644f59aac8e0b2553bfea48d99e9b323e03cbf55166659974eb8c51cc7b2c2c5d6aa6c01b056a8ed7283d96656a3496f266726605af1be139d586f208d4d7c59c2771dc8036d490d3672ee4513301002775d7c39eac421c6cb4f01344e061549a4cb11c057accef1726572e447501004c772ec91b4a55811280f
```
From the python code, we have:
```py
x = p + q
n = p * q
```
Since we've been given the sum and product of the two primes, it can be solved as a system of linear equations.  
The values will satisfy the quadratic equation,  
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><mrow><msup><mi>x</mi><mn>2</mn></msup><mo>-</mo><mi>S</mi><mi>x</mi><mo>+</mo><mi>P</mi><mo>=</mo><mn>0</mn></mrow></math>  
(S = Sum, P = Product, x = p & q)


And the roots of the equation can be found using the quadratic formula,  
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><mi>x</mi><mo>=</mo><mfrac><mrow><mi>S</mi><mo>&#x00B1;</mo><msqrt><mrow><msup><mi>S</mi><mn>2</mn></msup><mo>-</mo><mn>4</mn><mi>P</mi></mrow></msqrt></mrow><mn>2</mn></mfrac></math>  
which can be coded as:
```py
disc = x * x - 4 * n
discsq = isqrt(disc)
assert discsq * discsq == disc

p = (x + discsq) // 2
q = (x - discsq) // 2
```
This will give us p and q, which we can then use to find the private key (d):
```py
m = lcm(p - 1, q - 1)
d = pow(e, -1, m)
```
Having the private key, the ciphertext can be easily decoded:
```py
f = pow(c, d, n)
flag = long_to_bytes(f)
print(flag.decode())
```
And the output we get on running:
```
picoCTF{pl33z_n0_g1v3_c0ngru3nc3_0f_5qu4r35_3921def5}
```
Flag Obtained!

*Note*: Or, instead of finding the solutions of the quadratic equation, just substitute the values given in (p-1)(q-1) = pq - (p+q) + 1  
Easier way of solving, as pointed out to me :/

### Flag
> picoCTF{pl33z_n0_g1v3_c0ngru3nc3_0f_5qu4r35_3921def5}

## No Padding, No Problem
<a name="no-padding-no-problem"></a>

### Challenge
Oracles can be your best friend, they will decrypt anything, except the flag's ciphertext. How will you break it? Connect with `nc mercury.picoctf.net 33780`.

### Solving
On connecting to the server, we get the following:
```
devt0nes-picoctf@webshell:~$ nc mercury.picoctf.net 33780
Welcome to the Padding Oracle Challenge
This oracle will take anything you give it and decrypt using RSA. It will not accept the ciphertext with the secret message... Good Luck!


n: 114954424192047696778347260670584624979021151229132655989814598106517003839421825136845953406064270239484702411385168608133157620106929606550044740437239567246712360863615254427936318054541943985195863951725983146295127452009744796380530656625336099629543148294117828516188972215232872787354628581684256067519
e: 65537
ciphertext: 65128192378911476124015663522693489088504162401046305416226275150577698426212961354094092947006674421555509725829916542995422783826472814106363924681653452968928678554886358207000298048792322098873841277945618822889233224313274926519724586041704220983751732264164183440801506492143449639959867798892184570347


Give me ciphertext to decrypt:
```
We've been given the public key `(n,e)` and the ciphertext (flag), as well as the ability to decrypt any encoded data that has been encrypted with the same combination *apart* from the flag.  
Its apparent that this function is what we need to exploit to get the flag. Another hint we have is from the title of the question- that the encryption is done sans padding, which will come handy.  

Looking around about unpadded RSA I found that it is [partially homomorphic](https://en.wikipedia.org/wiki/Homomorphic_encryption#:~:text=.-,Unpadded%20RSA,-If%20the%20RSA), because of which it has a multiplicative property, which is that:  

<math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><mrow><mi mathvariant="script">E</mi><mo>(</mo><msub><mi>m</mi><mn>1</mn></msub><mo>)</mo><mo>&#x22C5;</mo><mi mathvariant="script">E</mi><mo>(</mo><msub><mi>m</mi><mn>2</mn></msub><mo>)</mo><mo>=</mo><msup><msub><mi>m</mi><mn>1</mn></msub><mi>e</mi></msup><msup><msub><mi>m</mi><mn>2</mn></msub><mi>e</mi></msup><mo>mod</mo><mi>n</mi></mrow><mrow><mo>=</mo><msup><mrow><mo>(</mo><msub><mi>m</mi><mn>1</mn></msub><mo>&#x22C5;</mo><msub><mi>m</mi><mn>2</mn></msub><mo>)</mo></mrow><mi>e</mi></msup><mo>mod</mo><mi>n</mi></mrow><mrow><mo>=</mo><mi mathvariant="script">E</mi><mo>(</mo><msub><mi>m</mi><mn>1</mn></msub><mo>&#x22C5;</mo><msub><mi>m</mi><mn>2</mn></msub><mo>)</mo></mrow></math>

where the encryption of the message 'm' is given by
<math xmlns="http://www.w3.org/1998/Math/MathML"><mrow><mi mathvariant="script">E</mi><mo>(</mo><mi>m</mi><mo>)</mo><mo>=</mo><msup><mi>m</mi><mi>e</mi></msup><mo>mod</mo><mi>n</mi></mrow></math>

[//]: # (Homomorphic encryption is a type of encryption that enables computations to be performed on encrypted data, producing results that match those of operations on unencrypted data.)
(*Note:* Unpadded RSA is **partially** homomorphic, as it only supports the multiplicative property and not the additive property)

So what can be done is that we can encrypt another message using the public key, something simple, and then multiply that with the flag ciphertext and get the oracle to decrypt the product, which would give us the plaintext product of the second message and the flag (and since we know the second message we can remove it from the product to get the flag).  

The python code that performs the above is:
```py
n = 114954424192047696778347260670584624979021151229132655989814598106517003839421825136845953406064270239484702411385168608133157620106929606550044740437239567246712360863615254427936318054541943985195863951725983146295127452009744796380530656625336099629543148294117828516188972215232872787354628581684256067519
e = 65537
ciphertext = 65128192378911476124015663522693489088504162401046305416226275150577698426212961354094092947006674421555509725829916542995422783826472814106363924681653452968928678554886358207000298048792322098873841277945618822889233224313274926519724586041704220983751732264164183440801506492143449639959867798892184570347

m2 = 2
c2 = pow(m2, e, n)

print(c2*ciphertext)
```
This gives the output:
```
2761507915534460444072727104534021915331892821921665268952325747434617453869538664611789238783118975578330283545287856623594998648910880668777437073029596229807147090735608486611266683556644746804207351701316871617733703890374921658355266859111719441863013687065377852930770796008533099140211482835164947483628184041662502013546902841303667844184235759837384352308128806815701521099346227875413940391408370662108735194054379629728619258036406215318427148523515680891744272995586953468699668480367714769056007126995925512663284256740414615371346025696495484583746486728715310475420772032983427424908363111226676872500
```
Now, giving the encrypted product to the oracle for decoding, we get:
```
Give me ciphertext to decrypt: 2761507915534460444072727104534021915331892821921665268952325747434617453869538664611789238783118975578330283545287856623594998648910880668777437073029596229807147090735608486611266683556644746804207351701316871617733703890374921658355266859111719441863013687065377852930770796008533099140211482835164947483628184041662502013546902841303667844184235759837384352308128806815701521099346227875413940391408370662108735194054379629728619258036406215318427148523515680891744272995586953468699668480367714769056007126995925512663284256740414615371346025696495484583746486728715310475420772032983427424908363111226676872500
Here you go: 580550060391700078946913236734911770139931497702556153513487440893406629034802718534645538074938502890768709712035489670906
```
Since we multiplied the flag with '2', we first divide the plaintext received by 2 and then decode to get the flag:
```py
m = 580550060391700078946913236734911770139931497702556153513487440893406629034802718534645538074938502890768709712035489670906 // 2
message_bytes = long_to_bytes(m)
message = message_bytes.decode('utf-8')
print(message)
```
Output:
```
picoCTF{m4yb3_Th0se_m3s54g3s_4r3_difurrent_0801973}
```
Flag Obtained!

### Flag
> picoCTF{m4yb3_Th0se_m3s54g3s_4r3_difurrent_0801973}

## SRA
<a name="sra"></a>

### Challenge
I just recently learnt about the SRA public key cryptosystem... or wait, was it supposed to be RSA? Hmmm, I should probably check...  
Connect to the program on our server: `nc saturn.picoctf.net 51248`  
Download the program: [chal.py](https://artifacts.picoctf.net/c/293/chal.py)

### Solving
chal.py contains:
```py
from Crypto.Util.number import getPrime, inverse, bytes_to_long
from string import ascii_letters, digits
from random import choice

pride = "".join(choice(ascii_letters + digits) for _ in range(16))
gluttony = getPrime(128)
greed = getPrime(128)
lust = gluttony * greed
sloth = 65537
envy = inverse(sloth, (gluttony - 1) * (greed - 1))

anger = pow(bytes_to_long(pride.encode()), sloth, lust)

print(f"{anger = }")
print(f"{envy = }")

print("vainglory?")
vainglory = input("> ").strip()

if vainglory == pride:
    print("Conquered!")
    with open("/challenge/flag.txt") as f:
        print(f.read())
else:
    print("Hubris!")
```
Going through this, we can deduce that-  
`pride`     -> original message (string of 16 random letters and numbers)  
`gluttony`  -> p  
`greed`     -> q  
`lust`      -> N  
`sloth`     -> e (65537)  
`envy`      -> d  
`anger`     -> encrypted message  

`vainglory` -> user input, must be the same as pride to get the flag  
