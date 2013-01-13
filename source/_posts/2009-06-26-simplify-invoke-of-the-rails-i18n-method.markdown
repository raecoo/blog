---
layout: post
title: 简化Rails国际化方法的调用
---

Rails 提供的国际化方法在调用时多少书写起来有点麻烦（至少在我看来是这样）I18n.t 'translate key'，我比较懒，而且极度不喜欢大小写键来回切换，找了个方法，用起来不错，记录一下，添加如下内容为一个lib文件，并在启动加载它即可以符号+l的方式调用，比如 :translate_key.l ,看起来是不是不错呢  ：）
<pre><code># Taken from Globalite
class Symbol # :nodoc:
  # Localizes the symbol into the current locale.
  # If there is no translation available, the replacement string will be returned
  def localize(replacement_string = '__localization_missing__', args={})
    I18n.translate(self, {:default => "#{replacement_string}(#{self})"}.merge(args))
  end
  alias :l :localize
  def l_in(locale, args={})
    I18n.translate(self, {:locale => locale, :default => "_localization_missing_(#{self})"}.merge(args)) unless locale.nil?
  end
  # Note that this method takes the replacement string after the args hash unlike other Globalite methods
  def localize_with_args(args={}, replacement_string = '__localization_missing__')
    I18n.translate(self, {:default => "#{replacement_string}(#{self})"}.merge(args))
  end
  alias :l_with_args :localize_with_args
end</code></pre>
