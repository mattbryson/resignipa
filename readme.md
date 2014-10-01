resignipa
=======

resignipa digitally re-signs existing .ipa bundles with Apple distribtuion certificates. 

This tool is useful when the person signing and deploying the .ipa may not be the developer.  It is also very useful for re-signing Enterprise applications when the provisioning profile expires - you dont need to re compile the appliciton.

You can update pre defined Plist poperties, such as *CFBundleDisplayName*, *CFBundleIdentifier*, *CFBundleVersion* as well as defining any other key values that you want to update in your plist.


Usage
=======

1) Copy the `resignipa` script to you mac. You could add it to your path if you use it alot.

2) Make it executable `$ chmod +x resignipa`

3) Run it for usage `./resignipa --help`

    usage: resignipa [-i ipa -p  profile -c codesignIdentity [ -v bundleVersion | -b bundleId | -n bundleDisplayName | -k keyValuePairs  | -l plist | -o outfile]] | [-h]

    -i | --ipa                  : The path to the original ipa file to be resigned
    -p | --profile              : The path to the provisioning profile
    -c | --codesignIdentity     : The identiy/name of the signing certifiate installed in keychain
    -v | --bundleVersion        : Optional, A verison to assign to CFBundleVersion
    -b | --bundleId             : Optional, New bundle ID
    -n | --bundleDisplayName    : Optional, New bundle display name
    -k | --keyValuePairs        : Optional, a comma delimted list of extra keys to update in the plist : -k "Foo=123456789, Bar=abcdefg, CFBundleDisplayName=ANF AmB EAME"
    -l | --plist                : Optional, Name of the plist file to edit. Default is Info.plist
    -o | --outfile              : Optional, Name of exported ipa, default is orignalFile_resigned.ipa
    -h | --help                 : Optional, this message


It will output a resigned IPA file in the same dir as the origin file.

Resign with new provisioning profile:

    /resingipa -i test.ipa -p com_domain_app.mobileprovision -c "iPhone Distribution: ACME Ltd"


Resign with new bundle id:

    /resingipa -i test.ipa -p com_domain_app.mobileprovision -c "iPhone Distribution: ACME Ltd" -b "my.new.bundle.id"

Resign with new bundle display name:

    /resingipa -i test.ipa -p com_domain_app.mobileprovision -c "iPhone Distribution: ACME Ltd" -n "My New name"

Resign with new version, where app has a custom plist:

    /resingipa -i test.ipa -p com_domain_app.mobileprovision -c "iPhone Distribution: ACME Ltd" -v "1.9" -p "custom.plist"

Resign and set name of new app:

    /resingipa -i test.ipa -p com_domain_app.mobileprovision -c "iPhone Distribution: ACME Ltd" -o "my_new_app.ipa"

Resign with other key values to set in the Plist:
 
    /resingipa -i test.ipa -p com_domain_app.mobileprovision -c "iPhone Distribution: ACME Ltd" -k "MyCustomKey=my value, MyOtherKey=12, CFBundleDisplayName=A new name"

The above list of Key valu pairs to update in the Plist will run after the other arguments, so setting *CFBundleDisplayName* **AND** *-n* flag, -k settings will take precidence.

License
=======

The MIT License (MIT)

Copyright (c) 2014 Matt Bryson

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.