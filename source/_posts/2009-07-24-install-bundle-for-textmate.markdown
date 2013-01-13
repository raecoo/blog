---
layout: post
title: 安装TextMate Bundle
---

<pre><code>mkdir -p ~/Library/Application\ Support/TextMate/Bundles/
cd ~/Library/Application\ Support/TextMate/Bundles
# cucumber
git clone git://github.com/bmabey/cucumber-tmbundle.git Cucumber.tmbundle
# ruby on rails
git clone git://github.com/drnic/ruby-on-rails-tmbundle.git "Ruby on Rails.tmbundle"
# shoulda
git clone git://github.com/drnic/ruby-shoulda-tmbundle.git Shoulda.tmbundle
# haml
git clone git://github.com/textmate/ruby-haml.tmbundle.git Haml.tmbundle
#experimental
git clone git://github.com/textmate/experimental.tmbundle.git

osascript -e 'tell app "TextMate" to reload bundles'

</code></pre>
