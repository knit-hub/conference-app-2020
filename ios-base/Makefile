GIT_REPO = $(shell git rev-parse --show-toplevel)
GIT_DIR = $(shell git rev-parse --git-dir)

init: swiftgen
	mint run xcodegen
	bundle install --path vendor/bundle
	bundle exec pod install
	@cp $(GIT_REPO)/ios-base/scripts/git-hooks/* $(GIT_DIR)/hooks

xcode:
	mint run xcodegen
	bundle exec pod install

swiftgen:
	mkdir -p $(GIT_REPO)/ios-base/DroidKaigi\ 2020/Generated
	mint run swiftgen swiftgen

test: xcode
	set -o pipefail && \
	xcrun xcodebuild -workspace 'DroidKaigi 2020.xcworkspace' \
	-scheme 'DroidKaigi 2020' \
	-destination 'platform=iOS Simulator,name=iPhone 11' \
	clean test | bundle exec xcpretty
