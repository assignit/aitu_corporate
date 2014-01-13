desc "Parse haml layouts"
task :haml_layouts do
  print "Parsing Haml layouts..."
  system(%{
    cd _layouts/haml && 
    for f in *.haml; do [ -e $f ] && haml $f ../${f%.haml}.html; done
  })
  puts "done."
end

desc "Compile Bootstrap Less"
task :bootstrap do
  require 'less'
  input  = File.join( "bootstrap_less", "bootstrap.less" )
  output = File.join( "css", "bootstrap.css" )
  path = input #File.join(".","css")
  source = File.open( input, "r" ).read
  parser = Less::Parser.new( :paths => [File.dirname(path)] )
  tree = parser.parse( source )

  File.open( output, "w+" ) do |f|
    f.puts tree.to_css( :compress => true )
  end
end 

task :clean do
  system "rm -rf _site"
end

#desc "synchronize with S3"
#task :sync do
#  system "s3cmd sync --rr --delete-removed _site/ s3://robin.wenglewski.de"
#end

desc "Launch preview environment"
task :preview => [:haml_layouts, :bootstrap, :clean] do
  system "jekyll --auto --server"
end

desc "Build site"
task :build => [:haml_layouts,  :clean] do |task, args|
  system "jekyll build"
end














