guard 'haml', output: 'deploy', input: 'src' do
  watch %r{^src/(.+)\.haml$}
end

guard 'sass', output: 'deploy/css', import_paths: ['vendor/stylesheets'] do
  watch %r{^src/stylesheets/(.*)\.scss$}
end

guard 'sprockets', destination: 'deploy/js', asset_paths: ['src/javascripts','vendor/javascripts'] do
  watch %r{^src/javascripts/(.*js)$}
end

guard 'webrick', docroot: 'deploy', launchy: false
