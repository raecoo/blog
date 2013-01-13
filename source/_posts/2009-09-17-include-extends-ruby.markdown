---
layout: post
title: 再记Ruby的include与extends
---

通常引用模块有以下3种情况：
1.在类定义中引入模块，使模块中的方法成为类的实例方法
这种情况是最常见的
直接 include <module name>即可

2.在类定义中引入模块，使模块中的方法成为类的类方法
这种情况也是比较常见的
直接 extend <module name>即可

3.在类定义中引入模块，既希望引入实例方法，也希望引入类方法
这个时候需要使用 include, 但是在模块中对类方法的定义有不同，定义出现在方法
def self.included(c) ... end 中.
<!--more-->
一个Mix-in的模板
<pre>
<pre><code>module TestModule
  def self.included(recipient)
    recipient.extend(ModelClassMethods)
    recipient.class_eval do
      include ModelInstanceMethods
    end
  end
  #
  module ModelClassMethods
    def class_method
      puts "this is a class method in module"
    end
  end # class methods
  #
  module ModelInstanceMethods
    def instance_method
      puts "this is a instance method in module"
    end
  end # instance methods
end
#
class TestClass
  include TestModule

end
#
TestClass.new.instance_method
#=> this is a instance method in module
TestClass.class_method
#=> this is a class method in module</code></pre>
</pre>
