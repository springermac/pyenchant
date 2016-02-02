#
#  Makefile for building pyenchant win32 dependencies.
#
ifdef APPVEYOR
    BUILD_DIR = $(APPVEYOR_BUILD_FOLDER)/tools/mingw-w64-enchant/build
else
    BUILD_DIR = /c/Users/rfk/Documents/GitHub/pyenchant/tools/pyenchant-bdist-win32-sources/build
endif

ENCHANT_DIR = $(BUILD_DIR)/../

all: $(BUILD_DIR)/lib/libenchant.dll $(BUILD_DIR)/share/enchant/myspell/en_GB.dic \
    $(BUILD_DIR)/share/enchant/myspell/en_US.dic $(BUILD_DIR)/share/enchant/myspell/de_DE.dic \
    $(BUILD_DIR)/share/enchant/myspell/en_AU.dic $(BUILD_DIR)/share/enchant/myspell/fr_FR.dic

#  Make enchant.
$(BUILD_DIR)/lib/libenchant.dll:
    cd $(ENCHANT_DIR) && makepgk-mingw
    cp $(ENCHANT_DIR)/src/.libs/libenchant-1.dll $(BUILD_DIR)/lib/
    mkdir -p $(BUILD_DIR)/lib/enchant
    cp $(ENCHANT_DIR)/src/ispell/.libs/libenchant_ispell.dll $(BUILD_DIR)/lib/enchant/
    cp $(ENCHANT_DIR)/src/myspell/.libs/libenchant_myspell.dll $(BUILD_DIR)/lib/enchant/

# Ability to extract MySpell dictionary files
$(BUILD_DIR)/share/enchant/myspell/%.dic: $(BUILD_DIR)/share/enchant/myspell/%.zip
    cd $(BUILD_DIR)/share/enchant/myspell && unzip -n $< '*.dic' '*.aff'


clean:
    rm -fr $(ENCHANT_DIR)

clobber: clean
    rm -f $(BUILD_DIR)/lib/libenchant*
    rm -rf $(BUILD_DIR)/lib/enchant
    rm -f $(BUILD_DIR)/share/enchant/myspell/*.dic
    rm -f $(BUILD_DIR)/share/enchant/myspell/*.aff
    rm -f $(BUILD_DIR)/share/enchant/myspell/*.txt
