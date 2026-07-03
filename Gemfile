source "https://rubygems.org"

# Jekyll static-site generator
gem "jekyll", "~> 4.3"

# The Minimal Mistakes theme (same theme grahamwatts.co.uk uses)
gem "minimal-mistakes-jekyll", "~> 4.28"

# Plugins the theme expects
group :jekyll_plugins do
  gem "jekyll-paginate"
  gem "jekyll-sitemap"
  gem "jekyll-feed"
  gem "jekyll-include-cache"
end

# Ruby 3.x no longer bundles these as default gems, so pin them explicitly.
gem "webrick", "~> 1.8"   # required for `jekyll serve` on Ruby 3+
gem "csv"
gem "logger"
gem "base64"
gem "bigdecimal"
