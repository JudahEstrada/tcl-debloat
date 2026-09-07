#!/usr/bin/env bash

###

# ==================================================================
# UPDATED TCL TV ADB DEBLOATER & PRIVACY HARDENING SCRIPT
# ==================================================================
# NOTICE: USE AT YOUR OWN RISK
# This script is provided as-is, without warranties of any kind. 
# While tested to safely remove manufacturer bloatware and telemetry, 
# results can vary wildly depending on your specific TV model, regional 
# firmware version, and Android build. 
# 
# Some packages or features (like voice search, home screen widgets, 
# or specific manufacturer integrations) may break or stop working 
# after removal. 
# 
# Always review the code, comment out as needed, use what you want, 
# and modify or adapt it freely for your own use cases.
# ==================================================================

###

# Color codes for user-friendly output
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
BLUE='\033[0;34m'
NC='\033[0m' # No Color

# ------------------------------------------------------------------
# SECTION 1: Legacy Android Editions (Android 7 - 11 Core Bloat)
# ------------------------------------------------------------------
legacy_packages_to_uninstall=(
    "com.tcl.partnercustomizer"
    "com.tcl.smartalexa"
    "com.tcl.gallery"
    "com.tcl.notereminder"
    "com.google.android.videos"
    "com.google.android.play.games"
    "com.tcl.MultiScreenInteraction_TV"
    "com.tcl.ui_mediaCenter"
    "com.tcl.messagebox"
    "tv.wuaki.apptv"
    "com.tcl.guard"
    "com.tcl.tvweishi"
    "com.tcl.t_solo"
    "com.tcl.dashboard"
    "com.tcl.tv.tclhome_master"
    "com.tcl.copydatatotv"
    "com.tcl.initsetup"
    "com.android.camera2"
    "com.android.messaging"
    "com.tcl.usercenter"
    "com.tcl.externaldevice.update"
    "com.tcl.useragreement"
    "com.tcl.appstatecontroller"
    "com.google.android.youtube.tvmusic"
    "com.google.android.leanbacklauncher.recommendations"
    "com.google.android.tvrecommendations"
    "com.google.android.marvin.talkback"
    "com.android.dreams.basic"
    "com.tcl.bi"
    "com.google.android.backdrop"
    "com.google.android.apps.mediashell"
    "com.tvos"
    "com.tcl.videoplayer"
    "com.google.android.apps.nbu.smartconnect.tv"
    "android.autoinstalls.config.tcl.device"
    "com.android.printspooler"
    "com.tcl.esticker"
    "com.google.android.syncadapters.calendar"
    "com.google.android.onetimeinitializer"
    "com.google.android.partnersetup"
    "com.google.android.gsf"
    "com.android.providers.calendar"
    "com.tcl.keyhelp"
    "com.android.providers.contacts"
    "com.google.android.feedback"
    "com.android.providers.userdictionary"
    "com.tcl.miracast"
    "com.tcl.audioplayer"
    "com.tcl.overseasappshow"
    "com.tcl.rc.ota"
    "com.tcl.imageplayer"
    "com.tcl.pvr.pvrplayer"
    "com.tcl.appmarket2"
    "com.google.android.sss.authbridge"
    "com.tcl.xian.StartandroidService"
    "com.tcl.versionUpdateApp"
    "com.tcl.assistant"
    "com.tcl.waterfall.overseas"
    "com.tcl.factory.view"
    "com.tcl.system.server"
    "com.google.android.tv.frameworkpackagestubs"
    "uk.co.freeview.mdsclient"
    "uk.co.freeview.amc_catchup"
    "com.update.appnews"
    "com.tcl.bootadservice"
    "uk.co.freeview.onnow"
    "au.com.stan.and"
    "uk.co.freeview.uktv"
    "uk.co.freeview.fvpconfigauth"
    "uk.co.freeview.systemdistributor"
    "uk.co.freeview.tifbridge"
    "com.linecorp.linetv"
    "uk.co.freeview.explore"
    "uk.co.freeview.bbc"
    "uk.co.freeview.ch5"
    "uk.co.freeview.itv"
    "uk.co.freeview.stv"
    "com.aos.aostv"
    "uk.co.freeview.amc_horror"
    "uk.co.freeview.ch4_vod"
    "com.graymatrix.did"
)

# ------------------------------------------------------------------
# SECTION 2: Android 12 Editions (New Telemetry & Ad Engines)
# ------------------------------------------------------------------
android12_packages_to_uninstall=(
    "com.tcl.tv.plus"
    "com.tcl.hotelmenu"
    "com.tcl.UpdatePeripheral"
    "com.tcl.ocean.instructions"
    "com.tcl.gamebar"
    "com.tcl.suspension"
    "com.tcl.channelplus"
    "com.tcl.airplay2"
    "com.tcl.logkit"
    "com.tcl.systemserver"
    "com.tcl.repairguide"
    "com.tcl.interactive"
    "com.tcl.globalkeyoverlay"
    "com.tcl.smartlink.core"
    "com.tcl.tv.tclhome_passive"
    "com.tcl.tv"
    "com.tcl.autopair"
    "com.tcl.ttvs"
    "com.tcl.exhibit"
)

# ------------------------------------------------------------------
# Execution & Interactive Logic
# ------------------------------------------------------------------
connect_tv(){
    echo -e "${BLUE}=== TCL TV ADB Debloater & Hardening Tool ===${NC}"
    read -p "[?] Enter TV IP address (leave blank if connected via USB): " IP

    if [ -n "$IP" ]; then
        echo -e "${YELLOW}[*] Pinging ${IP}...${NC}"
        if ping -c 1 ${IP} >/dev/null 2>&1; then
            echo -e "${GREEN}[+] Connecting via ADB to ${IP}...${NC}"
            adb connect ${IP} >/dev/null 2>&1
        else
            echo -e "${RED}[x] Error: Cannot reach target IP address.${NC}"
            connect_tv
            return
        fi
    fi

    if adb devices | grep -w "device" >/dev/null 2>&1; then
        echo -e "${GREEN}[+] ADB Device Connected Successfully!${NC}\n"
        show_menu
    else
        echo -e "${RED}[x] Error: No active ADB device found. Check debugging settings.${NC}"
        connect_tv
    fi
}

show_menu(){
    echo -e "${BLUE}Select an action profile:${NC}"
    echo "1) Full Debloat (Legacy Android 7-11 + Android 12 Apps)"
    echo "2) Legacy Debloat Only (Android 7-11)"
    echo "3) Android 12 Debloat Only"
    echo "4) Privacy Hardening & Ad-Blocking Only"
    echo "5) Exit"
    read -p "Select option [1-5]: " choice

    case $choice in
        1)
            run_debloat "${legacy_packages_to_uninstall[@]}" "${android12_packages_to_uninstall[@]}"
            run_hardening
            ;;
        2)
            run_debloat "${legacy_packages_to_uninstall[@]}"
            ;;
        3)
            run_debloat "${android12_packages_to_uninstall[@]}"
            ;;
        4)
            run_hardening
            ;;
        5)
            echo "Exiting."
            exit 0
            ;;
        *)
            echo -e "${RED}Invalid choice. Try again.${NC}"
            show_menu
            ;;
    esac
}

run_debloat(){
    local pkgs=("$@")
    echo -e "${YELLOW}[+] Running package removal profile (User 0)...${NC}"
    
    for pkg in "${pkgs[@]}"; do
        echo -n " > Removing $pkg: "
        result=$(adb shell pm uninstall --user 0 "$pkg" 2>&1)
        if [[ "$result" == *"Success"* ]]; then
            echo -e "${GREEN}Removed${NC}"
        else
            echo -e "${YELLOW}Skipped / Not Found${NC}"
        fi
    done
    echo -e "${GREEN}[+] Debloat batch completed.${NC}\n"
    ask_continue
}

run_hardening(){
    echo -e "${YELLOW}[+] Applying System Privacy & Anti-Tracking Hardening...${NC}"
    adb shell settings put secure upload_diagnostics 0
    adb shell settings put secure limit_ad_tracking 1
    
    echo " > Configuring secure AdGuard DNS..."
    adb shell settings put global private_dns_mode hostname
    adb shell settings put global private_dns_specifier dns.adguard-dns.com

    echo -e "${GREEN}[+] Privacy hardening complete! Please restart your TV manually to apply settings.${NC}"
    ask_continue
}

ask_continue(){
    read -p "[?] Return to menu? (y/n): " cont
    if [[ "$cont" =~ ^[Yy]$ ]]; then
        show_menu
    else
        echo "Goodbye!"
        exit 0
    fi
}

connect_tv
