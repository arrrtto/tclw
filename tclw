#!/bin/bash

# Made by Artto (aka DivineLoveArtto aka Arrrtto)
# Copyleft 2024


# Check currently installed Lite Wallet version

lwbinaryfile=$(which piratewallet-lite)
if [[ "$?" == "1" ]]; then
lwinstalled="no"
fi
if [[ "$?" == "0" ]]; then
lwinstalled="yes"
cat $lwbinaryfile | grep -aoE '.......PirateWallet Lightclient v' | sed 's/PirateWallet Lightclient v//' > /tmp/lwbinver0.txt
tr < /tmp/lwbinver0.txt -d '\000' > /tmp/lwbinver.txt
lwcurrentversionbybin=$(cat /tmp/lwbinver.txt)
dpkg -l | grep -E 'piratewallet-lite' | awk '{print $3}' > /tmp/lwverdpkg.txt
lwcurrentversionbydpkg=$(cat /tmp/lwverdpkg.txt)
fi

# Check currently installed Treasure Chest version

tcbinaryfile=$(which pirate-qt)
if [[ "$?" == "1" ]]; then
tcinstalled="no"
fi
if [[ $tcinstalled != "no" ]]; then
tcinstalled="yes"
cat $tcbinaryfile | grep -aoE 'clientname.v[[:digit:]].[[:digit:]].[[:digit:]]' | sed 's/clientname.v//' > /tmp/tcbinver.txt
tccurrentversionbybin=$(cat /tmp/tcbinver.txt)
dpkg -l | grep -E 'pirate-qt' | awk '{print $3}' > /tmp/tcverdpkg.txt
tccurrentversionbydpkg=$(cat /tmp/tcverdpkg.txt)
fi


# Check versions on GitHub

echo Checking GitHub...
gittc=$(curl "https://github.com/PirateNetwork/pirate")
gitlite=$(curl "https://github.com/PirateNetwork/PirateWallet-Lite")
# curl https://github.com/PirateNetwork/pirate | grep -oP 'releases/tag/v\K[0-9\.]+'
# curl https://github.com/PirateNetwork/PirateWallet-Lite | grep -oP 'releases/tag/\K[0-9\.]+'

delimiter=","
delimiter2=":"
expected=""

echo "$gittc" | grep -oP 'releases/tag/v\K[0-9\.]+' > filteredresult
tcversion=$(cat filteredresult)
echo "$gitlite" | grep -oP 'releases/tag/\K[0-9\.]+' > filteredresult
liteversion=$(cat filteredresult)

clear
echo Treasure Chest info:
if [[ $tcinstalled == "yes" ]]; then
echo "Found version:" $tccurrentversionbybin
fi
if [[ $tcinstalled == "no" ]]; then
echo "Treasure Chest not found."
fi
echo The latest available version is $tcversion

echo
echo Lite Wallet info:
if [[ $lwinstalled == "yes" ]]; then
echo "Found version:" $lwcurrentversionbybin
if [[ $lwcurrentversionbydpkg != $lwcurrentversionbybin ]]; then
echo "DPKG says version is:" $lwcurrentversionbydpkg
fi
fi
if [[ $lwinstalled == "no" ]]; then
echo "Lite Wallet not found."
fi

echo The latest available version is $liteversion
echo

if [[ $tcinstalled == "yes" ]] && [[ $tcversion == $tccurrentversionbybin ]]; then
echo
echo "You have the latest Treasure Chest version" $tcversion "installed."
echo "Location:" $tcbinaryfile
fi

if [[ $lwinstalled == "yes" ]] && [[ $liteversion == $lwcurrentversionbybin ]]; then
echo
echo "You have the latest Lite Wallet version" $liteversion "installed."
echo "Location:" $lwbinaryfile
echo
fi

if [[ $tcversion != $tccurrentversionbybin ]]; then
echo
echo "There is a newer version -" $tcversion "- of Treasure Chest available!"
echo
fi

if [[ $liteversion != $lwcurrentversionbybin ]]; then
echo
"There is a newer version -" $liteversion "- of Lite Wallet available!"
echo
fi


