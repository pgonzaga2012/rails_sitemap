# RailsSitemap

## Instalation

Add the gem in your Gemfile

```ruby
gem 'rails_sitemap'
```

It will generate an index sitemap. This sitemap will have a reference to geo-sitemap, attachment-sitemap and location sitemap

```xml
<sitemapindex
  xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <sitemap>
    <loc>http://www.example.com/pages-sitemap.xml</loc>
    <lastmod>2016-09-28T19:02:56+00:00</lastmod>
  </sitemap>
  <sitemap>
    <loc>http://www.example.com/attachment-sitemap.xml</loc>
    <lastmod>2016-09-28T19:02:56+00:00</lastmod>
  </sitemap>
  <sitemap>
    <loc>http://www.example.com/geo-sitemap.xml</loc>
    <lastmod>2016-09-28T19:02:56+00:00</lastmod>
  </sitemap>
```

## Configuration

If you want to generate the particular endpoint for each particular resource (in this case for each article) you have to overwrite the default configuration in initializer file.

```console
touch config/initializers/rails_sitemap.rb
```

```ruby
RailsSitemap.setup do |config|
  config.models_for_sitemap = %w(Article)
  config.updated_at = '2016-09-22T18:11:05-03:00'
  config.priority = 0.5
end
```

To define locations exposed on geo-sitemap

```ruby
RailsSitemap.setup do |config|
  config.locations = [
    {
      name: 'NeonRoots Uruguay Office',
      description: 'Zelmar Michelini 1290 Apto. 401   Esq. San José - Tel.  2909 0655',
      coordinates: '-56.19006872177124,-34.907047903278404,0'
    }
  ]
end
```

To define the hd images to be exposed on attachment-sitemap

```ruby
RailsSitemap.setup do |config|
  config.hd_images = [
    {
      name: 'mario.png',
      title: 'A super fancy mario image',
      coordinates: '12.417700299999979,45.4930475,0'
    }
  ]
end
```

To customize the update frequency

```ruby
RailsSitemap.setup do |config|
  config.update_frequency_for_app = 'always'
  config.update_frequency_for_models = 'weekly'
end
```

To define custom excluded paths

```ruby
RailsSitemap.setup do |config|
  config.excluded_paths = %w(/email_captures /drip-submission /thank-you)
end
```

To define custom domain

```ruby
RailsSitemap.setup do |config|
  config.domain = 'http://www.example.com/'
end
```
