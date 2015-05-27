
desc 'Build website'
task :build do
  sh 'jekyll build -q'
  sh 'docker build -t yux-website .'
end

desc 'Push website'
task :push => :build do
  sh 'docker tag -f yux-website registry.docker.yux.ch/yux-website'
  sh 'docker push registry.docker.yux.ch/yux-website'
end
