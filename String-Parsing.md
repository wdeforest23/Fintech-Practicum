Automated Data Wrangling
================
William DeForest
11/4/2021

``` r
#set the version of python to be used to your preferred version
#***important note***: the modules 'requests' and 'json' need to be loaded/exist in the python version you choose
#link to a video I used to install 'requests' in python: https://www.youtube.com/watch?v=HdJywzSCGbc
Sys.setenv(RETICULATE_PYTHON = "C:\\Users\\wdd72\\AppData\\Local\\Programs\\Python\\Python310\\python.exe")
library(reticulate)
py_config() #this should match your preferred version of python
```

    ## python:         C:/Users/wdd72/AppData/Local/Programs/Python/Python310/python.exe
    ## libpython:      C:/Users/wdd72/AppData/Local/Programs/Python/Python310/python310.dll
    ## pythonhome:     C:/Users/wdd72/AppData/Local/Programs/Python/Python310
    ## version:        3.10.0 (tags/v3.10.0:b494f59, Oct  4 2021, 19:00:18) [MSC v.1929 64 bit (AMD64)]
    ## Architecture:   64bit
    ## numpy:          C:/Users/wdd72/AppData/Local/Programs/Python/Python310/Lib/site-packages/numpy
    ## numpy_version:  1.21.4
    ## 
    ## NOTE: Python version was forced by RETICULATE_PYTHON

``` python
import requests
import json

API_KEY = '5c05369e4c54f17479afa729d59be1b2dae4149de916fea6fb8deddcbe5d7846'

headers = {
   'X-Api-Key': API_KEY,
   'Content-Type': 'application/json',
}

url_list = ["linkedin.com/in/kevinyamazaki/",
"linkedin.com/in/christopherimann/?miniProfileUrn=urn%3Ali%3Afs_miniProfile%3AACoAABEXtZMBPI5w40UjTKeCA4TI44wCutZldA0",
"linkedin.com/in/ericjj",
"linkedin.com/in/augie-nieto-0a31bb9",
"linkedin.com/in/mcfarlanescott",
"linkedin.com/in/jamesdlevine",
"linkedin.com/in/bkayton",
"crunchbase.com/person/sandy-lerner-e35e",
"linkedin.com/in/pauldekeyser",
"linkedin.com/in/mkleeman",
"linkedin.com/in/mkleeman",
"linkedin.com/in/steve-vollum-9726291a",
"linkedin.com/in/stephen-schaffran-4a806810",
"linkedin.com/in/israel-ben-tzur-1b1201130",
"linkedin.com/in/cyphers",
"linkedin.com/in/bret-jorgensen-11835b4",
"linkedin.com/in/kiphallman",
"linkedin.com/in/keesup-choe-47448a1",
"linkedin.com/in/gordonstitt",
"linkedin.com/in/burkburk",
"linkedin.com/in/cyphers/",
"linkedin.com/in/jeffreykang",
"linkedin.com/in/doug-keislar-258a5729",
"linkedin.com/in/christinemaxwell",
"linkedin.com/in/gregoryroufa",
"linkedin.com/in/ze-ev-rozov-32861",
"linkedin.com/in/israel-ben-tzur-1b1201130",
"linkedin.com/in/evanmargolin",
"linkedin.com/in/markhousley",
"linkedin.com/in/brian-muncaster",
"linkedin.com/in/mark-reiley-a4026865",
"linkedin.com/in/stu-trevelyan-9a691b",
"linkedin.com/in/gregoryroufa",
"linkedin.com/in/charles-naumer",
"linkedin.com/in/kevinfink",
"linkedin.com/in/jamesdlevine",
"crunchbase.com/person/sandy-lerner-e35e",
"linkedin.com/in/cyphers",
"linkedin.com/in/dreamhostmichael",
"linkedin.com/in/sageweil",
"linkedin.com/in/joshjones2",
"linkedin.com/in/gordonstitt",
"linkedin.com/in/scottkurowski",
"linkedin.com/in/dougparent",
"linkedin.com/in/eastling",
"linkedin.com/in/david-rose-49200715",
"linkedin.com/in/suryajayaweera",
"linkedin.com/in/brian-fleming-8445b31a",
"linkedin.com/in/bovine",
"linkedin.com/in/ze-ev-rozov-32861",
"linkedin.com/in/nadia-lee-kollectin",
"linkedin.com/in/steveloyola",
"linkedin.com/in/daveking",
"linkedin.com/in/vadim1",
"linkedin.com/in/scott-green-682bb3b2",
"linkedin.com/in/alarik-myrin-035bab1",
"linkedin.com/in/lornefierbach",
"linkedin.com/in/dean-terry",
"linkedin.com/in/youssef",
"linkedin.com/in/steveiverson",
"linkedin.com/in/christinemaxwell",
"linkedin.com/in/mattmcadams",
"linkedin.com/in/edchang",
"linkedin.com/in/davidblatner",
"linkedin.com/in/holliphant",
"linkedin.com/in/dumars",
"linkedin.com/in/edwardbuck",
"linkedin.com/in/dakotta",
"linkedin.com/in/dakotta",
"linkedin.com/in/dakotta",
"linkedin.com/in/ajstiles",
"linkedin.com/in/gbollinger",
"linkedin.com/in/mark-tennenbaum-8276b240",
"linkedin.com/in/mikep1",
"linkedin.com/in/matt-compton",
"linkedin.com/in/gregoryroufa",
"linkedin.com/in/garymwatson",
"linkedin.com/in/arlobelshee",
"linkedin.com/in/kimwon",
"linkedin.com/in/timmusgrove",
"linkedin.com/in/woodydeguchi",
"linkedin.com/in/ze-ev-rozov-32861",
"linkedin.com/in/nseet",
"linkedin.com/in/billsewell",
"linkedin.com/in/ivo-de-la-rive-box-3b2a71",
"linkedin.com/in/davidphillips",
"linkedin.com/in/stephen-schaffran-4a806810",
"linkedin.com/in/simon-ginsberg-26230658",
"linkedin.com/in/mkleeman",
"linkedin.com/in/youssef",
"linkedin.com/in/adamdaltman",
"linkedin.com/in/charles-naumer",
"linkedin.com/in/randysaaf",
"linkedin.com/in/bencasnocha",
"linkedin.com/in/keith-chugg-44164013",
"linkedin.com/in/robert-judge-ph-d-mba-b244627",
"linkedin.com/in/bardia-pezeshki-b75b2b6",
"linkedin.com/in/ronitmolko",
"linkedin.com/in/mark-reiley-a4026865",
"linkedin.com/in/garyglouner",
"linkedin.com/in/matt-compton",
"linkedin.com/in/markhousley",
"linkedin.com/in/danielbbernstein",
"linkedin.com/in/adamdaltman",
"linkedin.com/in/lloyd-kunimoto-5915584b",
"linkedin.com/in/chrisbissell",
"linkedin.com/in/todd-thomas-52021433",
"linkedin.com/in/ethan-caldwell-12623a",
"linkedin.com/in/hoodken",
"linkedin.com/in/mekka-okereke-05274b5",
"linkedin.com/in/mkleeman",
"linkedin.com/in/mattsponer",
"linkedin.com/in/cyphers",
"linkedin.com/in/scottkurowski",
"linkedin.com/in/gbollinger",
"linkedin.com/in/arinbrahma",
"linkedin.com/in/zac-brandenberg",
"linkedin.com/in/jeffreykang",
"linkedin.com/in/matthew-haines-92073a6",
"linkedin.com/in/edsoehnel",
"linkedin.com/in/raymondmontemayor",
"linkedin.com/in/mary-beth-gonzales-cpa-79745",
"linkedin.com/in/edwardbuck",
"linkedin.com/in/lloyd-kunimoto-5915584b",
"linkedin.com/in/woodyhunt",
"linkedin.com/in/eliza-cooney-061a781",
"linkedin.com/in/mcfarlanescott",
"linkedin.com/in/lornefierbach",
"linkedin.com/in/ilan-sabar",
"linkedin.com/in/ajstiles",
"linkedin.com/in/ashwinnavin",
"linkedin.com/in/christopoulos",
"linkedin.com/in/chris-seib-0242323",
"linkedin.com/in/jamesdlevine",
"linkedin.com/in/jimbrock",
"linkedin.com/in/boyd-macnaughton-b4a1b41",
"linkedin.com/in/benversteeg",
"linkedin.com/in/garrettfristoemiller",
"linkedin.com/in/alexernestszabo",
"linkedin.com/in/ivo-de-la-rive-box-3b2a71",
"linkedin.com/in/adamzbar",
"linkedin.com/in/suryajayaweera",
"linkedin.com/in/dan-michel-194411b",
"linkedin.com/in/heather-callender-potters-62247",
"linkedin.com/in/mattmcadams",
"linkedin.com/in/danshapiro",
"linkedin.com/in/susandoherty",
"linkedin.com/in/jim-nguyen-61b62a3",
"linkedin.com/in/henryalbrecht",
"linkedin.com/public-profile/in/hoodken?challengeId=AQEK0-X4OAaUCQAAAXarB8h1vIC5lQwcrK8rWhvb9i5Ei4QVv6VuW2ysWNtI6JDd0WsX1z6ixSAKOQjjjHJfiF8GmL9K9K8B4A&submissionId=38f85b73-37fb-5416-f81a-7450ef51ef3c",
"linkedin.com/in/mattmcadams",
"linkedin.com/in/jeffreykang",
"linkedin.com/in/michaelmxcarter",
"linkedin.com/in/coryforsyth",
"linkedin.com/in/coryforsyth",
"linkedin.com/in/timmusgrove",
"linkedin.com/in/sishir-reddy-a985826",
"linkedin.com/in/chaine",
"linkedin.com/in/ze-ev-rozov-32861",
"linkedin.com/in/davidphillips",
"linkedin.com/in/coryforsyth",
"linkedin.com/in/cameronfisher",
"linkedin.com/in/phillip-kast-2821833",
"linkedin.com/in/ericpozil",
"linkedin.com/in/tedgrahamdenver",
"linkedin.com/in/justin-garten-7783804",
"linkedin.com/in/ara-vartanian-90a7342",
"linkedin.com/in/chrisrinsch",
"linkedin.com/in/brenda-s-85520726",
"linkedin.com/in/phillip-kast-2821833",
"linkedin.com/in/davidglickman",
"linkedin.com/in/chas-wurster-496a11",
"linkedin.com/in/ryandellis",
"linkedin.com/in/cgenevier",
"linkedin.com/in/claudiocanive",
"linkedin.com/in/abowen",
"linkedin.com/in/steveiverson",
"linkedin.com/in/keesup-choe-47448a1",
"linkedin.com/in/kevin-harrang-6b423550",
"linkedin.com/in/mncuevas",
"linkedin.com/in/alexeiagratchev",
"linkedin.com/in/robiganguly",
"linkedin.com/in/ronda-perks-5a6a2a7",
"linkedin.com/in/tsaibenson",
"linkedin.com/in/jcastelaz",
"linkedin.com/in/addisonraymond",
"linkedin.com/in/osman-kibar-3a45ba",
"linkedin.com/in/pslaats",
"linkedin.com/in/michaelbeebe",
"linkedin.com/in/adamschoenfeld",
"linkedin.com/in/sunilrajaraman",
"linkedin.com/in/woodyhunt",
"linkedin.com/in/mark-reiley-a4026865",
"linkedin.com/in/ndrewlee",
"linkedin.com/in/alexhuf",
"linkedin.com/in/mojombo",
"linkedin.com/in/jacquesnadeau",
"linkedin.com/in/michaelmxcarter",
"linkedin.com/in/fernandorivera",
"linkedin.com/in/woodyhunt",
"linkedin.com/in/lianathompson",
"linkedin.com/in/cameronfisher",
"linkedin.com/in/ashwinnavin",
"linkedin.com/in/zaichang",
"linkedin.com/in/michaelmxcarter",
"linkedin.com/in/desireegolen",
"linkedin.com/in/grannyhacker",
"linkedin.com/in/rgrainger",
"linkedin.com/in/jeff-tarlowe-491100",
"linkedin.com/in/adamzbar",
"linkedin.com/in/joannanaymark",
"linkedin.com/in/stevengchiu",
"linkedin.com/in/asadharoon",
"linkedin.com/in/michael-sailor-60140929",
"linkedin.com/in/mscharf1",
"linkedin.com/in/reavis",
"linkedin.com/in/jimbrock",
"linkedin.com/in/steveiverson",
"linkedin.com/in/mollyhammar",
"linkedin.com/in/william-h-gentry-md-facs-75075419",
"linkedin.com/in/bardia-pezeshki-b75b2b6",
"linkedin.com/in/darrenleva",
"linkedin.com/in/tascher809",
"linkedin.com/in/sarah-douville",
"linkedin.com/in/dinageorgekhoury",
"linkedin.com/in/vadim1",
"linkedin.com/in/zac-brandenberg",
"linkedin.com/in/cyphers",
"linkedin.com/in/george-casey-14803a23",
"linkedin.com/in/leahwald",
"linkedin.com/in/avigeiger",
"linkedin.com/in/shahramseyedinnoor",
"linkedin.com/in/bensuppe",
"linkedin.com/in/bret-jorgensen-11835b4",
"linkedin.com/in/ruwanwelaratna",
"linkedin.com/in/zaichang",
"linkedin.com/in/chadthornton",
"linkedin.com/in/georgerevutsky",
"linkedin.com/in/adamschoenfeld",
"linkedin.com/in/jonathansimkin",
"linkedin.com/in/nategross",
"linkedin.com/in/switkes",
"linkedin.com/in/sontakey",
"linkedin.com/in/andrewwooster",
"linkedin.com/in/rchang",
"linkedin.com/in/jonathancarmel",
"linkedin.com/in/mwitcher",
"linkedin.com/in/jason-farmer-96a1068",
"linkedin.com/in/danshapiro",
"linkedin.com/in/brenthargrave",
"linkedin.com/in/michaelbeebe",
"linkedin.com/in/desireegolen",
"linkedin.com/in/gaiadempsey",
"linkedin.com/in/austinsoldner",
"linkedin.com/in/mishachellam",
"linkedin.com/in/danieldriscoll",
"linkedin.com/in/adamzbar",
"linkedin.com/in/andrew-m-jacobson",
"linkedin.com/in/ze-ev-rozov-32861",
"linkedin.com/in/adam-pelavin-8712a4",
"linkedin.com/in/leslie-mallman-cfp%C2%AE-b4a1773",
"linkedin.com/in/jonathanyedahmlee",
"linkedin.com/in/jamesdlevine",
"linkedin.com/in/davidwinternheimer",
"linkedin.com/in/gallardocm",
"linkedin.com/in/randysaaf",
"linkedin.com/in/jennifer-doudna-79b63527",
"linkedin.com/in/shahramseyedinnoor",
"linkedin.com/in/ashvin-dhingra-0a27863",
"linkedin.com/in/gordon-stott-89997b1b",
"linkedin.com/in/sarahpenna",
"linkedin.com/in/ivantse",
"linkedin.com/in/msaffitz",
"linkedin.com/in/andrewwooster",
"linkedin.com/in/holliphant",
"linkedin.com/in/gordonstitt",
"linkedin.com/in/mark-moehring-20a3822",
"linkedin.com/in/mattholden1",
"linkedin.com/in/alexhuf",
"linkedin.com/in/dannykuo",
"linkedin.com/in/shriverblake",
"linkedin.com/in/yoshi-matsumoto-116b4b24",
"linkedin.com/in/melinda-stahl-nix-70301a6",
"linkedin.com/in/markpneyer",
"linkedin.com/in/farhanbukharimd",
"linkedin.com/in/ryu-suliawan-54436434",
"linkedin.com/in/amy-herzog-98bb6",
"linkedin.com/in/caroline-wilkinson-80b49129",
"linkedin.com/in/justin-busch-5b1461",
"linkedin.com/in/brenda-s-85520726",
"linkedin.com/in/michaelbeebe",
"linkedin.com/in/ivantse",
"linkedin.com/in/victorpenev",
"linkedin.com/in/ericjj",
"linkedin.com/in/robertevans3",
"linkedin.com/in/dhari-alabdulhadi-b132a318",
"linkedin.com/in/matthewgoldman",
"linkedin.com/in/kaleazy",
"linkedin.com/in/pauldekeyser",
"linkedin.com/in/dave-feighan-279b247",
"linkedin.com/in/brianfeth",
"linkedin.com/in/amanda-malone-a0404937",
"linkedin.com/in/benjaminalevy",
"linkedin.com/in/joshresnick1",
"linkedin.com/in/patrick-crowley-b43b131a/?miniProfileUrn=urn%3Ali%3Afs_miniProfile%3AACoAAAQUj6MBL2g9e_vuFcRbOXT3YehWOu5toDo",
"linkedin.com/in/jonathansimkin",
"linkedin.com/in/dmitriskj",
"linkedin.com/in/douglas-fidaleo-b117b11",
"linkedin.com/in/mikemoyer1",
"linkedin.com/in/eugene-aarons-cooke",
"linkedin.com/in/mattsponer",
"linkedin.com/in/israel-ben-tzur-1b1201130",
"linkedin.com/in/nicoleh",
"linkedin.com/in/mfriefeld",
"linkedin.com/in/jmschwartz11",
"linkedin.com/in/joseph-richards-72810956",
"linkedin.com/in/davidglickman",
"linkedin.com/in/erik-norwood-61863819",
"linkedin.com/in/nolanzandi",
"linkedin.com/in/dpaulschultz",
"linkedin.com/in/chrisdavis1",
"linkedin.com/in/avemuri",
"linkedin.com/in/holliphant",
"linkedin.com/in/reavis",
"linkedin.com/in/ozlati",
"linkedin.com/in/ming-cheng-ho-00b28722",
"linkedin.com/in/alex-johnson-79b2301",
"linkedin.com/in/samirakhodai",
"linkedin.com/in/kevinrlloyd",
"linkedin.com/in/adamdaltman",
"linkedin.com/in/danielrgoodwin",
"linkedin.com/in/ryanmdick",
"linkedin.com/in/markhurwitz1",
"linkedin.com/in/edwardvsimpson",
"linkedin.com/in/sarper-gudek-1888557",
"linkedin.com/in/kathryn-hagedorn-a76b0955",
"linkedin.com/in/craigharley",
"linkedin.com/in/michael-franco-405149",
"linkedin.com/in/karakytle",
"linkedin.com/in/delaram-kahrobaei-3445783",
"linkedin.com/in/yochrismurphy",
"linkedin.com/in/iambic",
"linkedin.com/in/jessepollak",
"linkedin.com/in/mark-h-5bb82b1b",
"linkedin.com/in/darrelljonesiii",
"linkedin.com/in/jake-sullivan-460327",
"linkedin.com/in/peter-harding-40384",
"linkedin.com/in/shobhitd",
"linkedin.com/in/georgerevutsky",
"linkedin.com/in/sean-duffy-65120225",
"linkedin.com/in/mkawano",
"linkedin.com/in/markhurwitz1",
"linkedin.com/in/jennykarin",
"linkedin.com/in/lornefierbach",
"linkedin.com/in/dougparent",
"linkedin.com/in/timmusgrove",
"linkedin.com/in/dana-udall",
"linkedin.com/in/karen-albanese-a4b23b10",
"linkedin.com/in/maxgmenke",
"linkedin.com/in/leesherman68",
"linkedin.com/in/sriranga-yarlagadda",
"linkedin.com/in/ajaymukeshshah",
"linkedin.com/in/jennifer-doudna-79b63527",
"linkedin.com/in/nancy-marzouk-82519a",
"linkedin.com/in/davidkatz47",
"linkedin.com/in/demetri-monovoukas-5864aa74",
"linkedin.com/in/arunravimevoked",
"linkedin.com/in/fieldgarthwaite",
"linkedin.com/in/winston-owens-7a17a128",
"linkedin.com/in/berrysj",
"linkedin.com/in/eita-hatayama-703b78ba",
"linkedin.com/in/burke-wise",
"linkedin.com/in/shadiah",
"linkedin.com/in/rickotoole",
"linkedin.com/in/kendiamond02",
"linkedin.com/in/kaleazy",
"linkedin.com/in/jakeheller",
"linkedin.com/in/ajstiles",
"linkedin.com/in/iheidt",
"linkedin.com/in/timothy-brown",
"linkedin.com/in/mishachellam",
"linkedin.com/in/xiaoyinqu",
"linkedin.com/in/christopher-hunter-56262436",
"linkedin.com/in/cgenevier",
"linkedin.com/in/zac-brandenberg",
"linkedin.com/in/bmramirez",
"linkedin.com/in/ben-brostoff-bb815056",
"linkedin.com/in/ze-ev-rozov-32861",
"linkedin.com/in/stephsimon",
"linkedin.com/in/kevinwhsu",
"linkedin.com/in/branden-windle-66415371",
"linkedin.com/in/jennifersvendsen",
"linkedin.com/in/ndrewlee",
"linkedin.com/in/samcorcos",
"linkedin.com/in/mahdi-ali-85a61597",
"linkedin.com/in/holliphant",
"linkedin.com/in/davidjensen",
"linkedin.com/in/danielkan",
"linkedin.com/in/jlin07",
"linkedin.com/in/daniel-pivonka-9b333b16",
"linkedin.com/in/chaine",
"linkedin.com/in/jvchristiansen",
"linkedin.com/in/one-hwang",
"linkedin.com/in/benversteeg",
"linkedin.com/in/david-campbell-40968a51",
"linkedin.com/in/danieldriscoll",
"linkedin.com/in/adamzbar",
"linkedin.com/in/stu-trevelyan-9a691b",
"linkedin.com/in/alarik-myrin-035bab1",
"linkedin.com/in/joeykrug",
"linkedin.com/in/mark-reiley-a4026865",
"linkedin.com/in/jennifer-doudna-79b63527",
"linkedin.com/in/mattryanrich",
"linkedin.com/in/derbali",
"linkedin.com/in/lsotsky",
"linkedin.com/in/robertjlittle",
"linkedin.com/in/chrismcalary",
"linkedin.com/in/clintonpaulus",
"linkedin.com/in/granthosford",
"linkedin.com/in/amit-thakkar",
"linkedin.com/in/joeykrug",
"linkedin.com/in/jonathansimkin",
"linkedin.com/in/alexis-korman",
"linkedin.com/in/jason-soll-73704617",
"linkedin.com/in/jimbrock",
"linkedin.com/in/swaminathanrahul",
"linkedin.com/in/albertoziveri",
"linkedin.com/in/victorchiu",
"linkedin.com/in/stephen-smith-106a1296",
"linkedin.com/in/melissachanna",
"linkedin.com/in/james-durant-02687aa9",
"linkedin.com/in/alvin-ko",
"linkedin.com/in/jkodumal",
"linkedin.com/in/edithharbaugh",
"linkedin.com/in/benjaminhamlin",
"linkedin.com/in/arjunlall",
"linkedin.com/in/trevencornwall",
"linkedin.com/in/alex-groth-a926413a",
"linkedin.com/in/trotolo",
"linkedin.com/in/ritvij-gautam",
"linkedin.com/in/danshapiro",
"linkedin.com/in/storkgoldberg",
"linkedin.com/in/max-fortgang-01534b110",
"linkedin.com/in/heatherluttrell",
"linkedin.com/in/shamilhargovan",
"linkedin.com/in/ljadavji",
"linkedin.com/in/danielcoreyblack",
"linkedin.com/in/cavan-morris",
"linkedin.com/in/brianderfer",
"linkedin.com/in/christopoulos",
"linkedin.com/in/zihao-dennis-song-85570985",
"linkedin.com/in/nkdixit",
"linkedin.com/in/mattryanrich",
"linkedin.com/in/william-koven-3249a893",
"linkedin.com/in/sergey-tsalkov-29205249",
"linkedin.com/in/tom-driscoll-",
"linkedin.com/in/manners",
"linkedin.com/in/nealkemp1",
"linkedin.com/in/susanna-ingalls",
"linkedin.com/in/samcorcos",
"linkedin.com/in/scott-fraser-66b931154",
"linkedin.com/in/joseph-carson-ab929345",
"linkedin.com/in/dwcarroll",
"linkedin.com/in/davidwinternheimer",
"linkedin.com/in/randysaaf",
"linkedin.com/in/craiglytle",
"linkedin.com/in/whereisdoug",
"linkedin.com/in/michaelbeebe",
"linkedin.com/in/fabio-capoferri-5a041822",
"linkedin.com/in/marc-pollack-72aa6313",
"linkedin.com/in/duygualtinsoy",
"linkedin.com/in/dylansaffer",
"linkedin.com/in/leqtri",
"linkedin.com/in/patrickshao",
"linkedin.com/in/mfriefeld",
"linkedin.com/in/jmschwartz11",
"linkedin.com/in/oliverortlieb",
"linkedin.com/in/david-campbell-40968a51",
"linkedin.com/in/ckolmar",
"linkedin.com/in/ckolmar",
"linkedin.com/in/jacquesnadeau",
"linkedin.com/in/peter-zajac",
"linkedin.com/in/abowen",
"linkedin.com/in/albertlopez",
"linkedin.com/in/youssef",
"linkedin.com/in/alexhuf",
"linkedin.com/in/nishagarigarn",
"linkedin.com/in/sburke",
"linkedin.com/in/boris-gorshteyn-53544b19b",
"linkedin.com/in/ihafkenschiel",
"linkedin.com/in/berrysj",
"linkedin.com/in/mojombo",
"linkedin.com/in/danielscurtis",
"linkedin.com/in/danieladomian",
"linkedin.com/in/fabianfernandezhan",
"linkedin.com/in/gabe-audant",
"linkedin.com/in/emilymischel",
"linkedin.com/in/whereisdoug",
"linkedin.com/in/david-campbell-40968a51",
"linkedin.com/in/calebmorse",
"linkedin.com/in/cgenevier",
"linkedin.com/in/branden-windle-66415371",
"linkedin.com/in/mconbere",
"linkedin.com/in/joshhdaniel",
"linkedin.com/in/benpavlik",
"linkedin.com/in/mandalasiddharth",
"linkedin.com/in/rchino",
"linkedin.com/in/mojombo",
"linkedin.com/in/jvchristiansen",
"linkedin.com/in/jake-sullivan-460327",
"linkedin.com/in/tom-vaughan-8484883",
"linkedin.com/in/sontakey",
"linkedin.com/in/vikram-chandra",
"linkedin.com/in/bruce-moore-274a4029",
"linkedin.com/in/kyle-covell-077192",
"linkedin.com/in/david-dickey-phd-1a235952",
"linkedin.com/in/tamir-bechor-7a3991138",
"linkedin.com/in/rishov-chatterjee",
"linkedin.com/in/dorpalen",
"linkedin.com/in/dana-kittrelle-46970714",
"linkedin.com/in/roger-howe-93944353",
"linkedin.com/in/jasontolkin",
"linkedin.com/in/matthewmford",
"linkedin.com/in/meghna-lohia",
"linkedin.com/in/kearneyandy",
"linkedin.com/in/brad-hyslop-56818557",
"linkedin.com/in/amit-thakkar",
"linkedin.com/in/vikram-rangraj",
"linkedin.com/in/debracleaver",
"linkedin.com/in/cobrien2019",
"linkedin.com/in/charles-johnson-36964a6",
"linkedin.com/in/greenprint",
"linkedin.com/in/jonathan-engel-b28aab5",
"linkedin.com/in/sanjaywanand",
"linkedin.com/in/olivia-watkins-a73580bb",
"linkedin.com/in/sergey-tsalkov-29205249",
"linkedin.com/in/tomlockard",
"linkedin.com/in/sridharajay",
"linkedin.com/in/dmitriskj",
"linkedin.com/in/jacob-cohen-23353bb2",
"linkedin.com/in/sharon-hausman-cohen-26185718",
"linkedin.com/in/alexa-bartlett-6800b915",
"linkedin.com/in/laurajanesmith82",
"linkedin.com/in/benwdean",
"linkedin.com/in/kimwon",
"linkedin.com/in/josh-zappacosta-86130527",
"linkedin.com/in/whitmankwok",
"linkedin.com/in/nscottbradley",
"linkedin.com/in/adamschoenfeld",
"linkedin.com/in/jbeda",
"linkedin.com/in/samcorcos",
"linkedin.com/in/mjumbewu",
"linkedin.com/in/heather-bowling-121122a",
"linkedin.com/in/lloyd-kunimoto-5915584b",
"linkedin.com/in/yoichi-sagawa-2530761b",
"linkedin.com/in/julian-buckner-60980027",
"linkedin.com/in/ari-wes-md-ms-4a5aa924",
"linkedin.com/in/solonteal",
"linkedin.com/in/joeykrug",
"linkedin.com/in/arjunlall",
"linkedin.com/in/ryanscarpenter",
"linkedin.com/in/scott-fraser-66b931154",
"linkedin.com/in/ruben-p-c",
"linkedin.com/in/kaleazy",
"linkedin.com/in/rigele",
"linkedin.com/in/trevencornwall",
"linkedin.com/in/nadia-lee-kollectin",
"linkedin.com/in/mahrad-saeedi",
"linkedin.com/in/william-raasch-a267637",
"linkedin.com/in/jennifer-doudna-79b63527",
"linkedin.com/in/marenhotvedt",
"linkedin.com/in/jennifer-doudna-79b63527",
"linkedin.com/in/rossdc",
"linkedin.com/in/lockebrown",
"linkedin.com/in/sarah-mcphee-4298b4b",
"linkedin.com/in/zihao-dennis-song-85570985",
"linkedin.com/in/haoran-yu-884187109",
"linkedin.com/in/kristin-steele-3b9a905",
"linkedin.com/in/vanessacastanedagill",
"linkedin.com/in/robertevans3",
"linkedin.com/in/dantaber",
"linkedin.com/in/claudiocanive",
"linkedin.com/in/seth-l-80313120",
"linkedin.com/in/david-campbell-40968a51",
"linkedin.com/in/robert-mann-2487118",
"linkedin.com/in/laszlobock",
"linkedin.com/in/emilymischel",
"linkedin.com/in/zachry-fragapane",
"linkedin.com/in/vaibhav-viswanathan",
"linkedin.com/in/fsziegler",
"linkedin.com/in/nickchurcher",
"linkedin.com/in/sunilrajaraman",
"linkedin.com/in/jimbrock",
"linkedin.com/in/n-duncan",
"linkedin.com/in/dmitriskj",
"linkedin.com/in/hao-cao",
"linkedin.com/in/alexanderreichert",
"linkedin.com/in/tim-galbraith-8265206",
"linkedin.com/in/ecbftw",
"linkedin.com/in/ivo-de-la-rive-box-3b2a71",
"linkedin.com/in/bimal-kumar-3a368b17",
"linkedin.com/in/matt-m-10336713",
"linkedin.com/in/peterombres",
"linkedin.com/in/keesup-choe-47448a1",
"linkedin.com/in/justin-mugabe-19ba31a5",
"linkedin.com/in/jonathancarmel",
"linkedin.com/in/mncuevas",
"linkedin.com/in/adamdaltman",
"linkedin.com/in/danielomcguinness",
"linkedin.com/in/tomjcleveland",
"linkedin.com/in/sageshelton",
"linkedin.com/in/nicholas-diao-400054122",
"linkedin.com/in/justinwenig",
"linkedin.com/in/qian-jane-xu-29350757",
"linkedin.com/in/davidmarash",
"linkedin.com/in/jeffywu",
"linkedin.com/in/ben-brown-0685a5a",
"linkedin.com/in/benjaminarnoldkraus",
"linkedin.com/in/andrew-m-jacobson",
"linkedin.com/in/steveloyola",
"linkedin.com/in/shujingxu",
"linkedin.com/in/eliotarnold",
"linkedin.com/in/marcrothken",
"linkedin.com/in/arsamesqajar",
"linkedin.com/in/kurtzenzhouse",
"linkedin.com/in/shaundraullman",
"linkedin.com/in/eli-coon",
"linkedin.com/in/sarahpenna",
"linkedin.com/in/rimancuso",
"linkedin.com/in/simon-ginsberg-26230658",
"linkedin.com/in/jason-soll-73704617",
"linkedin.com/in/haoran-yu-884187109",
"linkedin.com/in/kayceelai",
"linkedin.com/in/austinsoldner",
"linkedin.com/in/mark-tennenbaum-8276b240",
"linkedin.com/in/jennifersvendsen",
"linkedin.com/in/kuroshhashemi",
"linkedin.com/in/rachelchai",
"linkedin.com/in/emilyolman",
"linkedin.com/in/ljadavji",
"linkedin.com/in/reikawano",
"linkedin.com/in/darinandersen",
"linkedin.com/in/jerry-chu",
"linkedin.com/in/aryn-sands-1220b14a",
"linkedin.com/in/aschanzg",
"linkedin.com/in/miriamcruz1027",
"linkedin.com/in/shadiah",
"linkedin.com/in/malpanishivam",
"linkedin.com/in/markpneyer",
"linkedin.com/in/malous-kossarian",
"linkedin.com/in/kaleazy",
"linkedin.com/in/danielzakowski",
"linkedin.com/in/leefarretta",
"linkedin.com/in/adriansugandhi",
"linkedin.com/in/rishov-chatterjee",
"linkedin.com/in/yoichi-sagawa-2530761b",
"linkedin.com/in/dlubarov",
"linkedin.com/in/antonybello",
"linkedin.com/in/david-coats-1bb5547",
"linkedin.com/in/gaylerigione",
"linkedin.com/in/anisha-soin",
"linkedin.com/in/anisha-soin",
"linkedin.com/in/kyle-schuster-37365b118",
"linkedin.com/in/mncuevas",
"linkedin.com/in/emilymischel",
"linkedin.com/in/simon-bock",
"linkedin.com/in/tzekin",
"linkedin.com/in/alejandro-mendoza-hmc",
"linkedin.com/in/charlespolk",
"linkedin.com/in/harry-cooke-64453186",
"linkedin.com/in/timothy-brown",
"linkedin.com/in/bartrollert",
"linkedin.com/in/jennifer-good-03b93826",
"linkedin.com/in/kimthanheph2017",
"linkedin.com/in/vikram-rangraj",
"linkedin.com/in/debracleaver",
"linkedin.com/in/leahrappaport",
"linkedin.com/in/matthewgoldman",
"linkedin.com/in/bcolman",
"linkedin.com/in/jefflub",
"linkedin.com/in/sachit-sood-41530057",
"linkedin.com/in/bardia-pezeshki-b75b2b6",
"linkedin.com/in/tsaibenson",
"linkedin.com/in/mahdi-ali-85a61597",
"linkedin.com/in/abasieneobong",
"linkedin.com/in/mkleeman",
"linkedin.com/in/zach-friedman-4945ba1a2",
"linkedin.com/in/davidwinternheimer",
"linkedin.com/in/mjcao",
"linkedin.com/in/davidhmeister",
"linkedin.com/in/ryan-karle",
"linkedin.com/in/ronalee-mann",
"linkedin.com/in/rob-schoening-038b30107",
"linkedin.com/in/chrisbissell",
"linkedin.com/in/kyra-mcandrews",
"linkedin.com/in/walkerevancasey",
"linkedin.com/in/joe-newbry",
"linkedin.com/in/dan-anderson-p-e",
"linkedin.com/in/ali-abramovitz-69458459",
"linkedin.com/in/colleenmkrumwiede",
"linkedin.com/in/willthehawk",
"linkedin.com/in/danivandesande",
"linkedin.com/in/georgekailas",
"linkedin.com/in/bridgetpayne",
"linkedin.com/in/minal-shankar",
"linkedin.com/in/kimwon",
"linkedin.com/in/gregoryroufa",
"linkedin.com/in/yince-loh-md-fncs-b8988936",
"linkedin.com/in/jamil-karriem-he-him-7a504040",
"linkedin.com/in/lsotsky",
"linkedin.com/in/glusman",
"linkedin.com/in/joseph-richards-72810956",
"linkedin.com/in/corey-van-der-wal",
"linkedin.com/in/kirawoods",
"linkedin.com/in/chinogba",
"linkedin.com/in/stephenscoblic",
"linkedin.com/in/mattsponer",
"linkedin.com/in/eliot-frost-214a0163",
"linkedin.com/in/samcorcos",
"linkedin.com/in/xiaoyinqu",
"linkedin.com/in/wyattchang",
"linkedin.com/in/heatherlouiseyoung",
"linkedin.com/in/anakakkar",
"linkedin.com/in/jimbrock",
"linkedin.com/in/dwcarroll",
"linkedin.com/in/skamaal",
"linkedin.com/in/maddie-hall-76293135",
"linkedin.com/in/jordanbonnet",
"linkedin.com/in/bmramirez",
"linkedin.com/in/alberto-ruiz-71786591",
"linkedin.com/in/laszlobock",
"linkedin.com/in/matthewjeffryes",
"linkedin.com/in/danieldriscoll",
"linkedin.com/in/jared-james-grogan-76495b27",
"linkedin.com/in/aliceywen",
"linkedin.com/in/jeffywu",
"linkedin.com/in/devriesjon",
"linkedin.com/in/corey-van-der-wal",
"linkedin.com/in/charles-naumer",
"linkedin.com/in/georgerevutsky",
"linkedin.com/in/aaron-wazana-90036618b",
"linkedin.com/in/jamesearlyrichards",
"linkedin.com/in/ngan-steve-nguyen-38820a149",
"linkedin.com/in/marco-lobba",
"linkedin.com/in/alice-e-chen-3448a712",
"linkedin.com/in/juliaacole",
"linkedin.com/in/wilfred-d-0525504",
"linkedin.com/in/ahmad-alkhatib-023a27171",
"linkedin.com/in/maximillian-bass-241a87161",
"linkedin.com/in/millyfotso",
"linkedin.com/in/manavkohli",
"linkedin.com/in/scottsonneborn",
"linkedin.com/in/jesse-lavine",
"linkedin.com/in/gilvgonzales",
"linkedin.com/in/pete-hellwig-7b01906",
"linkedin.com/in/simmonsjm",
"linkedin.com/in/philmang",
"linkedin.com/in/woodyhunt",
"linkedin.com/in/hannahkent",
"linkedin.com/in/drew-oetting-52463337",
"linkedin.com/in/noah-smith-340737176",
"linkedin.com/in/shifasomji",
"linkedin.com/in/dvtrivedi",
"linkedin.com/in/anshulkam",
"linkedin.com/in/amy-qian8",
"linkedin.com/in/marvin-jessica",
"linkedin.com/in/evancoulson",
"linkedin.com/in/adamzbar",
"linkedin.com/in/ketaki-madaan-5a0343166",
"linkedin.com/in/anthony-madubuonwu",
"linkedin.com/in/milesbernhard",
"linkedin.com/in/aravind-swaminathan-74817787",
"linkedin.com/in/tobe-wood-72646289",
"linkedin.com/in/domenico-ottolia-54007656",
"linkedin.com/in/michaelmxcarter",
"linkedin.com/in/misrarahul20",
"linkedin.com/in/tascher809",
"linkedin.com/in/eliotarnold",
"linkedin.com/in/ericyoungstrom",
"linkedin.com/in/jeffreyrstein",
"linkedin.com/in/joshlewisml",
"linkedin.com/in/prisma-herrera-2220b643",
"linkedin.com/in/mattholden1",
"linkedin.com/in/solonteal",
"linkedin.com/in/liambrennanburke",
"linkedin.com/in/karl-trautwein-77246a32",
"linkedin.com/in/henryengel",
"linkedin.com/in/quinntin-ruiz-90834757",
"linkedin.com/in/sachi-singh-b3b2249",
"linkedin.com/in/dhruvmanchala",
"linkedin.com/in/ellisbutterfield",
"linkedin.com/in/charles-johnson-36964a6",
"linkedin.com/in/jarredyacob",
"linkedin.com/in/maya-kale",
"linkedin.com/in/brendandmcdonald",
"linkedin.com/in/mollieamkraut",
"linkedin.com/in/sageweil",
"linkedin.com/in/john-whitledge-55255ba",
"linkedin.com/in/danjmitchell",
"linkedin.com/in/tomhsieh"]
 
data = {"requests": []}

for url in url_list[0:5]:
    data['requests'].append({
        "params": {
            "profile": [url]
        }
    })


json_responses = requests.post(
   'https://api.peopledatalabs.com/v5/person/bulk',
   headers=headers,
   json=data
).json()

out_data=[]


for response in json_responses:
  if response["status"] == 200:
  
    record = response['data']
    # Save enrichment data to json file
    out_data.append(record)
  else:
    print("Enrichment unsuccessful. See error and try again.")
    print("error:", response)
with open("output_data1.json", "w") as out:
      out.write(json.dumps(out_data))
```

    ## 74100

``` python
import json
import csv
import pandas as pd


with open('output_data1.json') as f:
  data =json.load(f)
data_file = open('data_file01.csv', 'w')

#df_json = pd.read_json('output_data1.json')
#df_json.to_excel('test.xlsx')

csv_writer = csv.writer(data_file)

count = 0
 
for founder in data:
  if count == 0:
 
        
      header = founder.keys()
      csv_writer.writerow(header)
      count += 1
 
   
  csv_writer.writerow(founder.values())
 
```

    ## 1233
    ## 7509
    ## 10652
    ## 14786
    ## 16640
    ## 16296

``` python
data_file.close()
```

``` r
#import raw PDL data
PDL_Data_raw <- read_excel("C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\Superseded\\founder-data1-all data.xlsx")
```

``` r
#separate experience and education strings

Education_Sep <- str_split(PDL_Data_raw$education, "\\}, \\{")
Experience_Sep <- str_split(PDL_Data_raw$experience, "\\}, \\{")
```

``` r
#parse education for school

school <- str_extract_all(Education_Sep,"\\'school': \\{'name': '.{4,100}', 'type'") %>% str_remove_all("', 'type'") %>% str_remove_all("'school': \\{'name': '") %>% str_remove_all("\\n") %>% str_remove_all("c\\(\\\"") %>% str_remove_all("\\\"\\)$") %>% str_split("\\\", \\\"", simplify=TRUE) %>% as.data.frame()
```

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

``` r
school <- school %>% rename("School 1" = V1) %>% rename("School 2" = V2) %>% rename("School 3" = V3) %>% rename("School 4" = V4) %>% rename("School 5" = V5) %>% rename("School 6" = V6) %>% rename("School 7" = V7) %>% rename("School 8" = V8) %>% rename("School 9" = V9) %>% rename("School 10" = V10) %>% rename("School 11" = V11) %>% rename("School 12" = V12) %>% rename("School 13" = V13) %>% rename("School 14" = V14) %>% rename("School 15" = V15) %>% rename("School 16" = V16) %>% rename("School 17" = V17) %>% rename("School 18" = V18)
```

``` r
#parse education for major

major <- str_extract_all(Education_Sep, "'majors': \\[.{0,50}\\], 'minors':") %>% str_remove_all("'majors': ") %>% str_remove_all(", 'minors':") %>% str_extract_all("\\[.*\\]") %>% str_replace_all("\\[\\]", "NA") %>% str_remove_all("\\['|'\\]|'") %>% str_split("\\\", \\\"", simplify=TRUE) %>% as.data.frame()
```

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

``` r
major <- major %>% rename("Major 1" = V1) %>% rename("Major 2" = V2) %>% rename("Major 3" = V3) %>% rename("Major 4" = V4) %>% rename("Major 5" = V5) %>% rename("Major 6" = V6) %>% rename("Major 7" = V7) %>% rename("Major 8" = V8) %>% rename("Major 9" = V9) %>% rename("Major 10" = V10)
```

``` r
#parse education for degree

degree <- str_extract_all(Education_Sep, "'degrees': \\[.{0,50}\\], '") %>% str_remove_all("'majors': \\[.{0,50}\\], ") %>% str_remove_all("'degrees': ") %>% str_remove_all("c\\(\\\"") %>% 
  str_remove_all("\\\"\\)$") %>% str_remove(", '$") %>% str_replace_all("\\[\\]", "NA") %>% str_remove_all("\\['|'\\]|'") %>% str_split("\\\", \\\"", simplify=TRUE) %>% as.data.frame()
```

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

``` r
degree <- degree %>% rename("Degree 1" = V1) %>% rename("Degree 2" = V2) %>% rename("Degree 3" = V3) %>% rename("Degree 4" = V4) %>% rename("Degree 5" = V5) %>% rename("Degree 6" = V6) %>% rename("Degree 7" = V7) %>% rename("Degree 8" = V8) %>% rename("Degree 9" = V9) %>% rename("Degree 10" = V10) %>% rename("Degree 11" = V11) %>% rename("Degree 12" = V12) %>% rename("Degree 13" = V13) %>% rename("Degree 14" = V14) %>% rename("Degree 15" = V15) %>% rename("Degree 16" = V16)
```

``` r
#parse education for start date

edu_start <- str_extract_all(Education_Sep, "'start_date': .{0,25}, 'gpa':|'start_date': .{0,25}, 'end_date':") %>% str_remove_all(", 'gpa':") %>% str_remove_all(", 'end_date':") %>% str_remove_all("'start_date': ") %>% str_remove_all("c\\(\\\"") %>% str_remove_all("\\\"\\)$") %>% str_remove_all("'") %>% str_split("\\\", \\\"", simplify=TRUE) %>% as.data.frame()
```

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

``` r
edu_start <- edu_start %>% rename("Edu_start 1" = V1) %>% rename("Edu_start 2" = V2) %>% rename("Edu_start 3" = V3) %>% rename("Edu_start 4" = V4) %>% rename("Edu_start 5" = V5) %>% rename("Edu_start 6" = V6) %>% rename("Edu_start 7" = V7) %>% rename("Edu_start 8" = V8) %>% rename("Edu_start 9" = V9) %>% rename("Edu_start 10" = V10) %>% rename("Edu_start 11" = V11) %>% rename("Edu_start 12" = V12) %>% rename("Edu_start 13" = V13) %>% rename("Edu_start 14" = V14) %>% rename("Edu_start 15" = V15) %>% rename("Edu_start 16" = V16) %>% rename("Edu_start 17" = V17) %>% rename("Edu_start 18" = V18) %>% rename("Edu_start 19" = V19)
```

``` r
# parse education for end date
edu_end <- str_extract_all(Education_Sep, "'end_date': .{0,25}, 'start_date':|'end_date': .{0,25}, 'majors':") %>% str_remove_all(", 'start_date':") %>% str_remove_all(", 'majors':") %>% str_remove_all("'end_date': ") %>% str_remove_all("c\\(\\\"") %>% str_remove_all("\\\"\\)$") %>% str_remove_all("'") %>% str_split("\\\", \\\"", simplify=TRUE) %>% as.data.frame()
```

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

``` r
edu_end <- edu_end %>% rename("Edu_end 1" = V1) %>% rename("Edu_end 2" = V2) %>% rename("Edu_end 3" = V3) %>% rename("Edu_end 4" = V4) %>% rename("Edu_end 5" = V5) %>% rename("Edu_end 6" = V6) %>% rename("Edu_end 7" = V7) %>% rename("Edu_end 8" = V8) %>% rename("Edu_end 9" = V9) %>% rename("Edu_end 10" = V10) %>% rename("Edu_end 11" = V11) %>% rename("Edu_end 12" = V12) %>% rename("Edu_end 13" = V13) %>% rename("Edu_end 14" = V14) %>% rename("Edu_end 15" = V15) %>% rename("Edu_end 16" = V16) %>% rename("Edu_end 17" = V17) %>% rename("Edu_end 18" = V18) %>% rename("Edu_end 19" = V19)
```

``` r
#parse experience for company

company <- Experience_Sep %>% str_extract_all("'company': \\{'name': .{0,50}, 'size':") %>% str_remove_all("'company': \\{'name': '") %>% str_remove_all("', 'size':") %>% str_remove_all("\\n") %>% str_remove_all("c\\(\\\"") %>% str_remove_all("\\\"\\)$") %>% str_split("\\\", \\\"", simplify=TRUE) %>% as.data.frame()
```

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

``` r
company <- company %>% rename("Company 1" = V1) %>% rename("Company 2" = V2) %>% rename("Company 3" = V3) %>% rename("Company 4" = V4) %>% rename("Company 5" = V5) %>% rename("Company 6" = V6) %>% rename("Company 7" = V7) %>% rename("Company 8" = V8) %>% rename("Company 9" = V9) %>% rename("Company 10" = V10) %>% rename("Company 11" = V11) %>% rename("Company 12" = V12) %>% rename("Company 13" = V13) %>% rename("Company 14" = V14) %>% rename("Company 15" = V15) %>% rename("Company 16" = V16) %>% rename("Company 17" = V17) %>% rename("Company 18" = V18) %>% rename("Company 19" = V19) %>% rename("Company 20" = V20) %>% rename("Company 21" = V21) %>% rename("Company 22" = V22) %>% rename("Company 23" = V23) %>% rename("Company 24" = V24) %>% rename("Company 25" = V25) %>% rename("Company 26" = V26) %>% rename("Company 27" = V27) %>% rename("Company 28" = V28) %>% rename("Company 29" = V29) %>% rename("Company 30" = V30) %>% rename("Company 31" = V31) %>% rename("Company 32" = V32) %>% rename("Company 33" = V33) %>% rename("Company 34" = V34) %>% rename("Company 35" = V35) %>% rename("Company 36" = V36) %>% rename("Company 37" = V37) %>% rename("Company 38" = V38) %>% rename("Company 39" = V39) %>% rename("Company 40" = V40) %>% rename("Company 41" = V41) %>% rename("Company 42" = V42) %>% rename("Company 43" = V43) %>% rename("Company 44" = V44) %>% rename("Company 45" = V45) %>% rename("Company 46" = V46)
```

``` r
#parse experience for industry

industry <- Experience_Sep %>% str_extract_all("'industry': .{0,50}, 'location':") %>% str_remove_all(", 'location':") %>% str_remove_all("'industry': ") %>% str_remove_all("\\n") %>% str_remove_all("c\\(\\\"") %>% str_remove_all("\\\"\\)$") %>% str_remove_all("'") %>% str_split("\\\", \\\"", simplify = TRUE) %>% as.data.frame()
```

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

``` r
industry <- industry %>% rename("Industry 1" = V1) %>% rename("Industry 2" = V2) %>% rename("Industry 3" = V3) %>% rename("Industry 4" = V4) %>% rename("Industry 5" = V5) %>% rename("Industry 6" = V6) %>% rename("Industry 7" = V7) %>% rename("Industry 8" = V8) %>% rename("Industry 9" = V9) %>% rename("Industry 10" = V10) %>% rename("Industry 11" = V11) %>% rename("Industry 12" = V12) %>% rename("Industry 13" = V13) %>% rename("Industry 14" = V14) %>% rename("Industry 15" = V15) %>% rename("Industry 16" = V16) %>% rename("Industry 17" = V17) %>% rename("Industry 18" = V18) %>% rename("Industry 19" = V19) %>% rename("Industry 20" = V20) %>% rename("Industry 21" = V21) %>% rename("Industry 22" = V22) %>% rename("Industry 23" = V23) %>% rename("Industry 24" = V24) %>% rename("Industry 25" = V25) %>% rename("Industry 26" = V26) %>% rename("Industry 27" = V27) %>% rename("Industry 28" = V28) %>% rename("Industry 29" = V29) %>% rename("Industry 30" = V30) %>% rename("Industry 31" = V31) %>% rename("Industry 32" = V32) %>% rename("Industry 33" = V33) %>% rename("Industry 34" = V34) %>% rename("Industry 35" = V35) %>% rename("Industry 36" = V36) %>% rename("Industry 37" = V37) %>% rename("Industry 38" = V38) %>% rename("Industry 39" = V39) %>% rename("Industry 40" = V40) %>% rename("Industry 41" = V41) %>% rename("Industry 42" = V42) %>% rename("Industry 43" = V43) %>% rename("Industry 44" = V44) %>% rename("Industry 45" = V45) %>% rename("Industry 46" = V46)
```

``` r
#parse experience for size

size <- Experience_Sep %>% str_extract_all("'size': .{0,25}, 'id':") %>% str_remove_all(", 'id':") %>% str_remove_all("'size': ") %>% str_remove_all("\\n") %>% str_remove_all("c\\(\\\"") %>% str_remove_all("\\\"\\)$") %>% str_remove_all("'") %>% str_split("\\\", \\\"", simplify = TRUE) %>% as.data.frame()
```

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

``` r
size <- size %>% rename("Size 1" = V1) %>% rename("Size 2" = V2) %>% rename("Size 3" = V3) %>% rename("Size 4" = V4) %>% rename("Size 5" = V5) %>% rename("Size 6" = V6) %>% rename("Size 7" = V7) %>% rename("Size 8" = V8) %>% rename("Size 9" = V9) %>% rename("Size 10" = V10) %>% rename("Size 11" = V11) %>% rename("Size 12" = V12) %>% rename("Size 13" = V13) %>% rename("Size 14" = V14) %>% rename("Size 15" = V15) %>% rename("Size 16" = V16) %>% rename("Size 17" = V17) %>% rename("Size 18" = V18) %>% rename("Size 19" = V19) %>% rename("Size 20" = V20) %>% rename("Size 21" = V21) %>% rename("Size 22" = V22) %>% rename("Size 23" = V23) %>% rename("Size 24" = V24) %>% rename("Size 25" = V25) %>% rename("Size 26" = V26) %>% rename("Size 27" = V27) %>% rename("Size 28" = V28) %>% rename("Size 29" = V29) %>% rename("Size 30" = V30) %>% rename("Size 31" = V31) %>% rename("Size 32" = V32) %>% rename("Size 33" = V33) %>% rename("Size 34" = V34) %>% rename("Size 35" = V35) %>% rename("Size 36" = V36) %>% rename("Size 37" = V37) %>% rename("Size 38" = V38) %>% rename("Size 39" = V39) %>% rename("Size 40" = V40) %>% rename("Size 41" = V41) %>% rename("Size 42" = V42) %>% rename("Size 43" = V43) %>% rename("Size 44" = V44)
```

``` r
#parse experience for title

title <- Experience_Sep %>% str_extract_all("'title': \\{'name': .{0,100}, 'role':") %>% str_remove_all(", 'role':") %>% str_remove_all("'title': \\{'name': ") %>% str_remove_all("\\n") %>% str_remove_all("c\\(\\\"") %>% str_remove_all("\\\"\\)$") %>% str_replace_all("\\\\\\\\\\\\\\\"", "'") %>% str_remove_all("'") %>% str_split("\\\", \\\"", simplify = TRUE) %>% as.data.frame()
```

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

``` r
title <- title %>% rename("Title 1" = V1) %>% rename("Title 2" = V2) %>% rename("Title 3" = V3) %>% rename("Title 4" = V4) %>% rename("Title 5" = V5) %>% rename("Title 6" = V6) %>% rename("Title 7" = V7) %>% rename("Title 8" = V8) %>% rename("Title 9" = V9) %>% rename("Title 10" = V10) %>% rename("Title 11" = V11) %>% rename("Title 12" = V12) %>% rename("Title 13" = V13) %>% rename("Title 14" = V14) %>% rename("Title 15" = V15) %>% rename("Title 16" = V16) %>% rename("Title 17" = V17) %>% rename("Title 18" = V18) %>% rename("Title 19" = V19) %>% rename("Title 20" = V20) %>% rename("Title 21" = V21) %>% rename("Title 22" = V22) %>% rename("Title 23" = V23) %>% rename("Title 24" = V24) %>% rename("Title 25" = V25) %>% rename("Title 26" = V26) %>% rename("Title 27" = V27) %>% rename("Title 28" = V28) %>% rename("Title 29" = V29) %>% rename("Title 30" = V30) %>% rename("Title 31" = V31) %>% rename("Title 32" = V32) %>% rename("Title 33" = V33) %>% rename("Title 34" = V34) %>% rename("Title 35" = V35) %>% rename("Title 36" = V36) %>% rename("Title 37" = V37) %>% rename("Title 38" = V38) %>% rename("Title 39" = V39) %>% rename("Title 40" = V40) %>% rename("Title 41" = V41) %>% rename("Title 42" = V42) %>% rename("Title 43" = V43) %>% rename("Title 44" = V44) %>% rename("Title 45" = V45)
```

``` r
#parse experience for start date

exp_start <- Experience_Sep %>% str_extract_all("'start_date': .{0,25}, 'title':") %>% str_remove_all(", 'title':") %>% str_remove_all(", 'end_date': .{0,5}") %>% str_remove_all("'start_date': ") %>% str_remove_all("\\n") %>% str_remove_all("c\\(\\\"") %>% str_remove_all("\\\"\\)$") %>% str_remove_all("'") %>% str_split("\\\", \\\"|, \\\"", simplify=TRUE) %>% as.data.frame()
```

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

``` r
exp_start <- exp_start %>% rename("Exp_start 1" = V1) %>% rename("Exp_start 2" = V2) %>% rename("Exp_start 3" = V3) %>% rename("Exp_start 4" = V4) %>% rename("Exp_start 5" = V5) %>% rename("Exp_start 6" = V6) %>% rename("Exp_start 7" = V7) %>% rename("Exp_start 8" = V8) %>% rename("Exp_start 9" = V9) %>% rename("Exp_start 10" = V10) %>% rename("Exp_start 11" = V11) %>% rename("Exp_start 12" = V12) %>% rename("Exp_start 13" = V13) %>% rename("Exp_start 14" = V14) %>% rename("Exp_start 15" = V15) %>% rename("Exp_start 16" = V16) %>% rename("Exp_start 17" = V17) %>% rename("Exp_start 18" = V18) %>% rename("Exp_start 19" = V19) %>% rename("Exp_start 20" = V20) %>% rename("Exp_start 21" = V21) %>% rename("Exp_start 22" = V22) %>% rename("Exp_start 23" = V23) %>% rename("Exp_start 24" = V24) %>% rename("Exp_start 25" = V25) %>% rename("Exp_start 26" = V26) %>% rename("Exp_start 27" = V27) %>% rename("Exp_start 28" = V28) %>% rename("Exp_start 29" = V29) %>% rename("Exp_start 30" = V30) %>% rename("Exp_start 31" = V31) %>% rename("Exp_start 32" = V32) %>% rename("Exp_start 33" = V33) %>% rename("Exp_start 34" = V34) %>% rename("Exp_start 35" = V35) %>% rename("Exp_start 36" = V36) %>% rename("Exp_start 37" = V37) %>% rename("Exp_start 38" = V38) %>% rename("Exp_start 39" = V39) %>% rename("Exp_start 40" = V40)
```

``` r
#parse experience for end date

exp_end <- Experience_Sep %>% str_extract_all("'end_date': .{0,25}, 'start_date':|'end_date': .{0,25}, 'title':") %>% str_remove_all(", 'start_date':") %>% str_remove_all(", 'title':") %>% str_remove_all("'end_date': ") %>% str_remove_all("\\n") %>% str_remove_all("c\\(\\\"") %>% str_remove_all("\\\"\\)$") %>% str_remove_all("'") %>% str_split("\\\", \\\"", simplify=TRUE) %>% as.data.frame()
```

    ## Warning in stri_extract_all_regex(string, pattern, simplify = simplify, :
    ## argument is not an atomic vector; coercing

    ## Warning in stri_replace_all_regex(string, pattern,
    ## fix_replacement(replacement), : argument is not an atomic vector; coercing

``` r
exp_end <- exp_end %>% rename("Exp_end 1" = V1) %>% rename("Exp_end 2" = V2) %>% rename("Exp_end 3" = V3) %>% rename("Exp_end 4" = V4) %>% rename("Exp_end 5" = V5) %>% rename("Exp_end 6" = V6) %>% rename("Exp_end 7" = V7) %>% rename("Exp_end 8" = V8) %>% rename("Exp_end 9" = V9) %>% rename("Exp_end 10" = V10) %>% rename("Exp_end 11" = V11) %>% rename("Exp_end 12" = V12) %>% rename("Exp_end 13" = V13) %>% rename("Exp_end 14" = V14) %>% rename("Exp_end 15" = V15) %>% rename("Exp_end 16" = V16) %>% rename("Exp_end 17" = V17) %>% rename("Exp_end 18" = V18) %>% rename("Exp_end 19" = V19) %>% rename("Exp_end 20" = V20) %>% rename("Exp_end 21" = V21) %>% rename("Exp_end 22" = V22) %>% rename("Exp_end 23" = V23) %>% rename("Exp_end 24" = V24) %>% rename("Exp_end 25" = V25) %>% rename("Exp_end 26" = V26) %>% rename("Exp_end 27" = V27) %>% rename("Exp_end 28" = V28) %>% rename("Exp_end 29" = V29) %>% rename("Exp_end 30" = V30) %>% rename("Exp_end 31" = V31) %>% rename("Exp_end 32" = V32) %>% rename("Exp_end 33" = V33) %>% rename("Exp_end 34" = V34) %>% rename("Exp_end 35" = V35) %>% rename("Exp_end 36" = V36) %>% rename("Exp_end 37" = V37) %>% rename("Exp_end 38" = V38) %>% rename("Exp_end 39" = V39) %>% rename("Exp_end 40" = V40) %>% rename("Exp_end 41" = V41) %>% rename("Exp_end 42" = V42) %>% rename("Exp_end 43" = V43) %>% rename("Exp_end 44" = V44) %>% rename("Exp_end 45" = V45)
```

``` r
#merge data frames

PDL_Data <- cbind(PDL_Data_raw, school, major, degree, edu_start, edu_end, company, industry, size, title, exp_start, exp_end)
```

``` r
#output data into Excel
write.csv(PDL_Data,"C:\\Users\\wdd72\\OneDrive\\Documents\\Junior Fall\\Fintech Practicum\\Fintech_Data\\PDL_Data_Parsed.csv", row.names = FALSE)
```
