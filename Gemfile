# frozen_string_literal: true

source "https://rubygems.org"

# Use older Jekyll version for better compatibility
gem "jekyll", "~> 3.9.3"

# Theme
gem "jekyll-theme-chirpy", "~> 5.6.1"

# Required for Jekyll 3.9
gem "kramdown-parser-gfm"
gem "webrick"

group :jekyll_plugins do
  gem "jekyll-paginate"
  gem "jekyll-sitemap"
  gem "jekyll-gist"
  gem "jekyll-feed"
  gem "jekyll-seo-tag"
  gem "jemoji"
  gem "jekyll-include-cache"
  gem "jekyll-remote-theme"
end

# Required for serving
gem "faraday-retry"

platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

gem "wdm", "~> 0.2.0", :platforms => [:mingw, :x64_mingw, :mswin]
