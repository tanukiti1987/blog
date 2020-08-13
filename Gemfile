source "https://rubygems.org"

gem "jekyll", "~> 3.8"
gem "kramdown-parser-gfm"

# If you have any plugins, put them here!
group :jekyll_plugins do
  gem 'jekyll-paginate'
  gem 'jekyll-sitemap'
  gem 'jekyll-auto-image'
end

group :production do
  gem "s3_website"
  gem 'jekyll-tfidf-related-posts'
  # FIXME: Use official packable after merging the pull request below.
  #        For solving jekyll-tfidf-related-posts working issue on ruby-alpine docker.
  # https://github.com/SciRuby/packable/pull/6
  gem 'packable', github: 'pocheptsov/packable', ref: 'ee9e18c77a258879e3ad4dbf91a95bda2117f9ac'
end
