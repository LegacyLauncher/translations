# Legacy Launcher Translation Repository
The files `lang_en_US.properties` and `lang_ru_RU.properties` are maintained by the Legacy Launcher-developers.
All new strings are added to these files.

You should use one of these files as the source for your translation.

Edit one of the existing `lang_*_.properties`-files or create a new one.

## Linux shell
Creation of a translation file for your language as a little bash script:

```bash
# change to your desired language code
lang=de_DE

while read LINE; do
  echo "$LINE" | grep -q = && (
    KEY=$(echo "$LINE" | cut -d = -f1 | sed 's/\([^#[:alnum:]]\)/\\\1/g')
    grep "^${KEY}=" lang_${lang}.properties || echo "#TRANSLATE $LINE"
  ) || echo "$LINE"
done < lang_en_US.properties > translateme.txt
```

This creates a file `translateme.txt` with commented lines starting with `#TRANSLATE`, which are not in the current target language file. Edit it by your desire and move it to your targeted language file.
