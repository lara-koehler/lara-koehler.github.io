source "https://rubygems.org"

# Plain Jekyll (not the "github-pages" gem) — this avoids a native
# C-extension dependency (nokogiri/racc) that fails to compile on
# this machine's current Xcode Command Line Tools version.
# We deploy via the GitHub Actions Jekyll workflow (set up in the
# final step), which builds with whatever version is pinned here —
# so there's no downside to not using the github-pages gem.
gem "jekyll", "~> 4.3"

# Needed to run a local server on recent Ruby versions.
gem "webrick"
