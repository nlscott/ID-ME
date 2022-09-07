#!/bin/bash

loggedInUser=$(echo "show State:/Users/ConsoleUser" | scutil | awk '/Name :/ && ! /loginwindow/ { print $3 }')

MYDIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"
source "$MYDIR/pashua.sh"

conf="
# Set window title
*.title = ID ME

img.type = image
img.relx = 150
img.maxwidth = 100
img.path = "$MYDIR/icon.png"

# Add a filesystem browser
ob.type = openbrowser
ob.label = Choose a file:
ob.default =
ob.width = 400

# Add a cancel button with default label
cb.type = cancelbutton
cb.tooltip = This is an element of type “cancelbutton”

db.type = defaultbutton
db.tooltip = This is an element of type “defaultbutton” (which is automatically added to each window, if not included in the configuration)
"

if [ -d '/Volumes/Pashua/Pashua.app' ]
then
	# Looks like the Pashua disk image is mounted. Run from there.
	customLocation='/Volumes/Pashua'
else
	# Search for Pashua in the standard locations
	customLocation=''
fi

# Get the icon from the application bundle
locate_pashua "$customLocation"
bundlecontents=$(dirname $(dirname "$pashuapath"))
if [ -e "$bundlecontents/Resources/AppIcon@2.png" ]
then
    conf="$conf
          img.type = image
          img.x = 435
          img.y = 248
          img.maxwidth = 128
          img.tooltip = This is an element of type “image”
          img.path = $bundlecontents/Resources/icon.png"
fi

pashua_run "$conf" "$customLocation"

echo "Pashua created the following variables:"
echo "  ob  = $ob"
echo ""


##------------------------------------------------------------------------------
## Variables
##------------------------------------------------------------------------------
directory="$(dirname "$ob")"
fullfilename="$(basename "$ob")"
filename=$(echo $fullfilename| cut -d"." -f1)
extname=$(echo $fullfilename| cut -d"." -f2)
pathtoApp="$ob"
info="$pathtoApp/Contents/Info.plist"
shortString=$(defaults read "$info" CFBundleShortVersionString)
bundleversion=$(defaults read "$info" CFBundleVersion)
executable=$(codesign -dvvv "$pathtoApp" 2>&1 | grep "Executable" | cut -d "=" -f2)
teamIdentifier=$(codesign -dvvv "$pathtoApp" 2>&1 | grep -w "TeamIdentifier" | cut -d "=" -f2)
identifier=$(codesign -dvvv "$pathtoApp" 2>&1 | grep -w "Identifier" | cut -d "=" -f2)
developer=$(codesign -dvvv "$pathtoApp" 2>&1 | grep -w "Authority=Developer ID Application:" | cut -d "=" -f2 | cut -d ":" -f2 | xargs)

# Sanity Check -----------------------------------------------------------------
# echo $filepath
# echo $fileMode
# echo $fileOwner
# echo $fileGroup

##------------------------------------------------------------------------------
## Second Window
##------------------------------------------------------------------------------
# echo "Current Settings:" >> "/private/tmp/results.txt"
# echo "Mode: $fileMode" >> "/private/tmp/results.txt"
# echo "Owner: $fileOwner" >> "/private/tmp/results.txt"
# echo "Group: $fileGroup" >> "/private/tmp/results.txt"

# results=`perl -p -e 's/\n/[return]/g;' "/private/tmp/results.txt"`

    MYDIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" && pwd )"
    source "$MYDIR/pashua.sh"

    conf="
    # Set window title
    *.title = ID ME

    img.type = image
    img.relx = 225
    img.rely = 250
    img.maxwidth = 100
    img.path = "$MYDIR/icon.png"

    txt1.type = text
    txt1.default = Version: $shortString [return]
    txt1.width = 500
    txt1.x = 50
    txt1.y = 200

    txt2.type = text
    txt2.default = Bundle Version: $bundleversion [return]
    txt2.width = 500
    txt2.x = 50
    txt2.y = 175

    txt4.type = text
    txt4.default = TeamIdentifier: $teamIdentifier [return]
    txt4.width = 500
    txt4.x = 50
    txt4.y = 150

    txt5.type = text
    txt5.default = Identifier: $identifier [return]
    txt5.width = 500
    txt5.x = 50
    txt5.y = 125

    txt6.type = text
    txt6.default = Developer: $developer [return]
    txt6.width = 500
    txt6.x = 50
    txt6.y = 100

    txt3.type = text
    txt3.default = Executable path: $executable [return]
    txt3.width = 500
    txt3.x = 50
    txt3.y = 75

    # Add a cancel button with default label
    cb.type = cancelbutton
    cb.tooltip = This is an element of type “cancelbutton”
    "

    if [ -d '/Volumes/Pashua/Pashua.app' ]
    then
        # Looks like the Pashua disk image is mounted. Run from there.
        customLocation='/Volumes/Pashua'
    else
        # Search for Pashua in the standard locations
        customLocation=''
    fi

    pashua_run "$conf" "$customLocation"
    echo "Pashua created the following variables:"
    echo "  ob  = $ob"
    echo "  cb  = $cb"
    echo ""



