# Rsmangler with Aircrack-ng

Use this tool to crack WPA/WPA2 passwords with aircrack-ng

```bash
# Create a directed wordlist
echo 'donkey' > wordlist.txt
echo 'burro' >> wordlist.txt
echo 'mule' >> wordlist.txt
echo 'ass' >> wordlist.txt
echo 'dumb' >> wordlist.txt

rsmangler --file wordlist.txt --min 12 --max 13 | aircrack-ng -e $SSID $PCAP -w -
```

## References

* [Rsmangler](https://digi.ninja/projects/rsmangler.php)

```text
rsmangler --help

rsmangler v 1.5 Robin Wood (robin@digi.ninja) <https://digi.ninja>

Basic usage:

        rsmangler --file wordlist.txt

To pass the initial words in on standard in do:

        cat wordlist.txt | rsmangler

To send the output to a file:

        rsmangler --file wordlist.txt --output mangled.txt

        All options are ON by default, these parameters turn them OFF

        Usage: rsmangler [OPTION]
        --help, -h: show help
        --file, -f: the input file, use - for STDIN
        --output, -o: the output file, use - for STDOUT
        --max, -x: maximum word length
        --min, -m: minimum word length
        --perms, -p: permutate all the words
        --double, -d: double each word
        --reverse, -r: reverser the word
        --leet, -t: l33t speak the word
        --full-leet, -T: all posibilities l33t
        --capital, -c: capitalise the word
        --upper, -u: uppercase the word
        --lower, -l: lowercase the word
        --swap, -s: swap the case of the word
        --ed, -e: add ed to the end of the word
        --ing, -i: add ing to the end of the word
        --punctuation: add common punctuation to the end of the word
        --years, -y: add all years from 1990 to current year to start and end
        --acronym, -a: create an acronym based on all the words entered in order and add to word list
        --common, -C: add the following words to start and end: admin, sys, pw, pwd
        --pna: add 01 - 09 to the end of the word
        --pnb: add 01 - 09 to the beginning of the word
        --na: add 1 - 123 to the end of the word
        --nb: add 1 - 123 to the beginning of the word
        --force: don't check output size
        --space: add spaces between words
        --allow-duplicates: allow duplicates in the output list
```