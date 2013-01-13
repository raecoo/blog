---
layout: post
title: hack truncate in ruby 1.8.7 compability issue
---

add follows code into rails app environment.rb and restart the service
# http://rails.lighthouseapp.com/projects/8994/tickets/867-undefined-method-length-for-enumerable
<pre><code>
class String
  def chars
    ActiveSupport::Multibyte::Chars.new(self)
  end
  alias_method :mb_chars, :chars
end
##
module ActionView
  module Helpers
    module TextHelper
      def truncate(text, length = 30, truncate_string = "...")
        if text.nil? then return end
        l = length - truncate_string.chars.to_a.size
        (text.chars.to_a.size > length ? text.chars.to_a[0...l].join + truncate_string : text).to_s
      end
    end
  end
end</code></pre>
