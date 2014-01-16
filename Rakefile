namespace :haml do
	require 'haml'
 
	def convert file, destination
		base_name = File.basename(file, '.haml') + '.html'
		html = File.open(file, 'r') { |f| Haml::Engine.new(f.read).render }
		File.open(File.join(destination, base_name), 'w') { |f| f.write html }
	end
 
	desc 'Parse haml layout files'
	task :layouts do
		Dir.glob('_layouts/_haml/*.haml') do |path|
			convert path, '_layouts'
		end
 
		puts 'Parsed haml layout files'
	end
 
	desc 'Parse haml include files'
	task :includes do
		Dir.glob('_includes/_haml/*.haml') do |path|
			convert path, '_includes'
		end
 
		puts 'Parsed haml include files'
	end
 
	desc 'Parse haml index files'
	task :indexes do
		Dir.glob('**/index.haml') do |path|
		  puts 'working on : ' + path
			convert path, File.dirname(path)
		end
 
		puts 'Parsed haml index files'
	end
 
end
 

desc 'Parse all haml items'
task :haml => ['haml:layouts', 'haml:includes', 'haml:indexes']

desc "Parse haml layouts"
task :haml_layouts do
  print "Parsing Haml layouts..."
  system(%{
    cd _layouts/_haml && 
    for f in *.haml; do [ -e $f ] && haml $f ../${f%.haml}.html; done
  })
  puts "done."
end


task :clean do
  system "rm -rf _site/*"
end

#desc "synchronize with S3"
#task :sync do
#  system "s3cmd sync --rr --delete-removed _site/ s3://robin.wenglewski.de"
#end

desc "Launch preview environment"
task :preview => [:haml_layouts, :bootstrap, :clean] do
  system "jekyll --auto --server"
end

desc "Move web site to local server"
task :move do
  # Clean the local webserver folder - make sure permissions have been set to 777
  system "rm -rf /Library/WebServer/Documents/aitu_corporate_site/*"  
  system "cp -R _site/ /Library/WebServer/Documents/aitu_corporate_site/"
  
end




desc "Build site"
task :build => [:haml_layouts, :clean] do |task, args|

  system "jekyll build"
end





desc "Build site and move to local server"
task :build_and_move => [:build, :move] do |task, args|

end

desc "Build site and move to local server"
task :local => [:build, :move] do |task, args|

end









