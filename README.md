# detect-missing-translations
This is a sample to showcase a Python script, to detect missing translations in a mobile project.  
Here is how it works.

### Retrieve Base Translation Keys:
Start by retrieving all translation keys from the base (English) file.  
Store these keys in an array for comparison.  

### Process each Language:
For each language, create an array of all translation keys available.  
Compare this array with the base array using the export_empty_as=skip parameter in Lokalise. This helps identify keys that are not translated for the current language.  
Check each untranslated key against a whitelist:  
  If the key is on the whitelist and the language is also whitelisted, add it to a dictionary.  
  If not, skip the key.  

### Formulate Untranslated Keys Dictionary:
The result is a dictionary, untranslated_keys, structured like this:
```
untranslated_keys = {
  'key1': ['de', 'fr', 'es', 'it'],
  'key2': ['fr', 'es'],
   etc...
}
```

### Parse the Project:
Parse the entire project, starting from one or more root folders defined in the constants.  
To optimize speed, you can exclude certain folders and focus only on files of specific formats (e.g., .swift, .kt, .xml for mobile development).  

### Identify Used Keys:
In each parsed file, check for the presence of keys from the untranslated_keys list.  
If a key is found, add it to a used_keys set.

### Clean Up:
After parsing, you will have a list of keys that are actually used in the project.  
Use this list to clean your untranslated_keys dictionary, removing any keys that are not used.

### Output Results:
Finally, print the cleaned list of untranslated keys to a file and display it in the console for review.

## Usage:
`python detect_missing_translations.py --platform ANDROID|IOS --lokalise_api_key YOUR_KEY --lokalise_project_id YOUR_PROJECT_ID`  
or  
`python detect_missing_translations.py --platform ANDROID|IOS --skip-whitelist`  
Other options available:
```
--verbose
--strict_mode : should it fail if some tier2 translations are missing
```
