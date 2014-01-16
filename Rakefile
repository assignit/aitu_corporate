desc "Parse haml layouts"
task :haml_layouts do
  print "Parsing Haml layouts..."
  system(%{
    cd _layouts/haml && 
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
task :build => [:haml_layouts,  :clean] do |task, args|
  system "jekyll build"
end





desc "Build site and move to local server"
task :build_and_move => [:build, :move] do |task, args|

end

desc "Build site and move to local server"
task :local => [:build, :move] do |task, args|

end









