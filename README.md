cladr
=====

Use Flickr machine tags to create a tree of life based on biological taxonomy


Description
-----------

Using machine tags, it's possible to indicate how your Flickr photos fit
into a tree of life. Cladr uses data from [Wikispecies]
(https://species.wikimedia.org/) and the [Encyclopedia of Life]
(http://eol.org/) to add these tags to your photos based on some initial
tag that you have provided.

For example, if you tag a photo with `taxonomy:binomial=Danaus plexippus`,
cladr will find the [monarch butterfly]
(https://species.wikimedia.org/wiki/Danaus%5fplexippus) on Wikispecies and
add several tags:

    taxonomy:kingdom=Animalia
    taxonomy:phylum=Arthropoda
    taxonomy:class=Insecta
    taxonomy:order=Lepidoptera
    taxonomy:family=Nymphalidae
    taxonomy:genus=Danaus

Clades from the Encyclopedia of Life are not necessarily ranked. Some
taxonomies may have [dozens of clades] (http://eol.org/pages/2682739/names)
representing other branches of life between the seven classical ranks.
Cladr will look up these detailed clades and add tags representing their
heirarchy, along with an EOLID number and a common name:

    taxonomy:eolid=2682739
    taxonomy:common=Monarch
    taxonomy:claderoot=Animalia
    clade:Animalia=Arthropoda
    clade:Arthropoda=Insecta
    clade:Insecta=Lepidoptera
    clade:Lepidoptera=Papilionoidea
    clade:Papilionoidea=Nymphalidae
    clade:Nymphalidae=Danaus
    clade:Danaus=plexippus

Using these tags, you can [browse your photos] (http://cladr.severinghaus.org/)
as a tree of life.

Cladr will take advantage of whatever level of identification you can
provide. For example, if you only know the subject of the photo is a duck,
you can just start with `taxonomy:family=Anatidae`. If it's a dog, you can
go all the way to `taxonomy:trinomial=Canis lupus familiaris`.


Usage
-----

    Usage: cladr [options] [photoids...]

    Options:
        -h --help               Print help and exit
        -b --before-date        Look for photos prior to this date
        -c --skip-clades        Skip tagging with clades
        -r --skip-ranks         Skip tagging with ranks
        -E --skip-eolid         Skip tagging with EOLID
        -C --skip-common        Skip tagging with common name
        -t --tags=foo,bar       Restrict to photos tagged thusly
        -T --threshold=8        Number of tags before assuming photo already tagged
        -e --eolid=31415        Assume this EOLID for the photos
        -B --binomen='Foo bar'  Assume this binomen for the photos
        -G --genus=Foo          Assume this genus for the photos
        -F --family=Foo         Assume this family for the photos
        --from-file             Read Flickr photo IDs from this file
        -t --token              Authentication token if not in ~/.cladrrc
        -u --user               User if not in ~/.cladrrc
        -v --verbosity          How much yammering to do
        -f --force              Force tagging, even if tagged as unidentified
        -y --yes                Answer "yes" to all questions; run non-interactively

