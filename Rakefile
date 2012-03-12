require 'bundler'
require 'pathname'
require 'logger'

Bundler.require

ROOT = Pathname(File.dirname(__FILE__))
SRC_CSS = ROOT.join('src/stylesheets')
SRC_JS = ROOT.join('src/javascripts')
VENDOR_CSS = ROOT.join('vendor/stylesheets')
VENDOR_JS = ROOT.join('vendor/javascripts')
DEPLOY = ROOT.join('deploy')
LOGGER = Logger.new(STDOUT)

desc 'Generate stylesheets using sass'
task :css do
  sh "mkdir -p #{DEPLOY}/css"
  sh "sass -I#{VENDOR_CSS} #{SRC_CSS}/style.scss #{DEPLOY}/css/style.css"
end

desc 'Generate the javascript file'
task :js do
  sh "mkdir -p #{DEPLOY}/js"

  sprockets = Sprockets::Environment.new(ROOT) do |env|
    env.logger = LOGGER
  end

  sprockets.append_path(SRC_JS)
  sprockets.append_path(VENDOR_JS)

  assets = sprockets.find_asset('script.js')

  assets.write_to(DEPLOY.join('js', 'scripts.js'))
end

desc 'Generate html from haml'
task :html do
  Dir.glob('**/*.haml') do |f|
    out = DEPLOY.to_s + f.sub(/.*\//, '').sub(/.haml$/, '.html')
    sh "haml #{f} #{out}"
  end
end

desc "Move static files into site dir."
task :static do
  sh "cp -r #{ROOT}/static/* #{DEPLOY}"
  sh "cp -r #{ROOT}/vendor/images #{DEPLOY}/img"
end

desc 'Compile everything'
task default: [:css, :js, :html, :static]
