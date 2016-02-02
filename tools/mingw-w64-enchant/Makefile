#
#  Makefile for building pyenchant win dependencies.
#
BUILD_DIR = $(realpath build)
ENCHANT_DIR = $(realpath src)/enchant-1.6.0-build-x86_64

all: $(BUILD_DIR)/lib/libenchant.dll $(BUILD_DIR)/share/enchant/myspell/en_GB.dic \
	$(BUILD_DIR)/share/enchant/myspell/en_US.dic $(BUILD_DIR)/share/enchant/myspell/de_DE.dic \
	$(BUILD_DIR)/share/enchant/myspell/en_AU.dic $(BUILD_DIR)/share/enchant/myspell/fr_FR.dic

#  Make enchant.
$(BUILD_DIR)/lib/libenchant.dll:
	ifdef APPVEYOR
		exec 0</dev/null
		makepkg-mingw
		exec 0<&-
	else
		makepkg-minw
	endif
	mkdir -p $(BUILD_DIR)/lib
	cp $(ENCHANT_DIR)/src/.libs/libenchant.dll $(BUILD_DIR)/lib/
	mkdir -p $(BUILD_DIR)/lib/enchant
	cp $(ENCHANT_DIR)/src/ispell/.libs/libenchant_ispell.dll $(BUILD_DIR)/lib/enchant/
	cp $(ENCHANT_DIR)/src/myspell/.libs/libenchant_myspell.dll $(BUILD_DIR)/lib/enchant/

# Ability to extract MySpell dictionary files
$(BUILD_DIR)/share/enchant/myspell/%.dic: $(BUILD_DIR)/share/enchant/myspell/%.zip
	cd $(BUILD_DIR)/share/enchant/myspell && unzip $< *.dic *.aff


clean:
	rm -fr src
	rm -rf pkg
	rm -f enchant-1.6.0.tar.gz
	rm -f mingw-w64-x86_64-enchant-1.6.0-1-any.pkg.tar.xz
	rm -f mingw-w64-i686-enchant-1.6.0-1-any.pkg.tar.xz

clobber: clean
	rm -f $(BUILD_DIR)/lib/libenchant*
	rm -rf $(BUILD_DIR)/lib/enchant
	rm -f $(BUILD_DIR)/share/enchant/myspell/*.dic
	rm -f $(BUILD_DIR)/share/enchant/myspell/*.aff
	rm -f $(BUILD_DIR)/share/enchant/myspell/*.txt
