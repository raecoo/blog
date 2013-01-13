---
layout: post
title: custom exceptions in merb
---

在开发应用过程中难免需要根据实际情况自定义一些异常处理机制，这方面Merb已经将底部的架子为我们准备好了，我们只需要简单的在此基础上进行扩展就可以搞的很舒服。
Merb默认生成的Application会提供一个Exception的Controller，并包含了两个样版异常NotFound和NotAcceptable。现在我们添加一个自定义的异常在这里，假定名称为NotExists，并为其创建对应的View。
在Action中调用
<pre><code> def show
product = Product.find(params[:id])
raise NotExists unless product
[...]
end</code></pre>
这时会报错，称并不存在NotExists常量，Google了一下并没有找到合理的解释，直接看了Merb的源代码才发现，自定义异常不是这样的用法。

在Merb里如果要自定义异常，需要将自定义异常继承自一个Merb自身已存的异常，比如这样
<pre><code>class NotExists &lt; Merb::ControllerExceptions::NotFound ; end</code></pre>
并且需要在使用该异常的Controller里进行声明（放在Application里自然会是一个不错的选择），再跑一下上面报错的程序应该就可以得到正确的结果啦~ BTW:为了这个我可查了好一会资料 ：）
<!--more-->
以下是Merb对标准Http异常的封装
<pre><code> class Informational                 &lt; Merb::ControllerExceptions::Base; end
class Continue                    &lt; Merb::ControllerExceptions::Informational; self.status = 100; end
class SwitchingProtocols          &lt; Merb::ControllerExceptions::Informational; self.status = 101; end
class Successful                    &lt; Merb::ControllerExceptions::Base; end
class OK                          &lt; Merb::ControllerExceptions::Successful; self.status = 200; end
class Created                     &lt; Merb::ControllerExceptions::Successful; self.status = 201; end
class Accepted                    &lt; Merb::ControllerExceptions::Successful; self.status = 202; end
class NonAuthoritativeInformation &lt; Merb::ControllerExceptions::Successful; self.status = 203; end
class NoContent                   &lt; Merb::ControllerExceptions::Successful; self.status = 204; end
class ResetContent                &lt; Merb::ControllerExceptions::Successful; self.status = 205; end
class PartialContent              &lt; Merb::ControllerExceptions::Successful; self.status = 206; end
class Redirection                   &lt; Merb::ControllerExceptions::Base; end
class MultipleChoices             &lt; Merb::ControllerExceptions::Redirection; self.status = 300; end
class MovedPermanently            &lt; Merb::ControllerExceptions::Redirection; self.status = 301; end
class MovedTemporarily            &lt; Merb::ControllerExceptions::Redirection; self.status = 302; end
class SeeOther                    &lt; Merb::ControllerExceptions::Redirection; self.status = 303; end
class NotModified                 &lt; Merb::ControllerExceptions::Redirection; self.status = 304; end
class UseProxy                    &lt; Merb::ControllerExceptions::Redirection; self.status = 305; end
class TemporaryRedirect           &lt; Merb::ControllerExceptions::Redirection; self.status = 307; end
class ClientError                   &lt; Merb::ControllerExceptions::Base; end
class BadRequest                  &lt; Merb::ControllerExceptions::ClientError; self.status = 400; end
class MultiPartParseError         &lt; Merb::ControllerExceptions::BadRequest; end
class Unauthorized                &lt; Merb::ControllerExceptions::ClientError; self.status = 401; end
class PaymentRequired             &lt; Merb::ControllerExceptions::ClientError; self.status = 402; end
class Forbidden                   &lt; Merb::ControllerExceptions::ClientError; self.status = 403; end
class NotFound                    &lt; Merb::ControllerExceptions::ClientError; self.status = 404; end
class ActionNotFound              &lt; Merb::ControllerExceptions::NotFound; end
class TemplateNotFound            &lt; Merb::ControllerExceptions::NotFound; end
class LayoutNotFound              &lt; Merb::ControllerExceptions::NotFound; end
class MethodNotAllowed            &lt; Merb::ControllerExceptions::ClientError; self.status = 405; end
class NotAcceptable               &lt; Merb::ControllerExceptions::ClientError; self.status = 406; end
class ProxyAuthenticationRequired &lt; Merb::ControllerExceptions::ClientError; self.status = 407; end
class RequestTimeout              &lt; Merb::ControllerExceptions::ClientError; self.status = 408; end
class Conflict                    &lt; Merb::ControllerExceptions::ClientError; self.status = 409; end
class Gone                        &lt; Merb::ControllerExceptions::ClientError; self.status = 410; end
class LengthRequired              &lt; Merb::ControllerExceptions::ClientError; self.status = 411; end
class PreconditionFailed          &lt; Merb::ControllerExceptions::ClientError; self.status = 412; end
class RequestEntityTooLarge       &lt; Merb::ControllerExceptions::ClientError; self.status = 413; end
class RequestURITooLarge          &lt; Merb::ControllerExceptions::ClientError; self.status = 414; end
class UnsupportedMediaType        &lt; Merb::ControllerExceptions::ClientError; self.status = 415; end
class RequestRangeNotSatisfiable  &lt; Merb::ControllerExceptions::ClientError; self.status = 416; end
class ExpectationFailed           &lt; Merb::ControllerExceptions::ClientError; self.status = 417; end
class ServerError                   &lt; Merb::ControllerExceptions::Base; end
class InternalServerError         &lt; Merb::ControllerExceptions::ServerError; self.status = 500; end
class NotImplemented              &lt; Merb::ControllerExceptions::ServerError; self.status = 501; end
class BadGateway                  &lt; Merb::ControllerExceptions::ServerError; self.status = 502; end
class ServiceUnavailable          &lt; Merb::ControllerExceptions::ServerError; self.status = 503; end
class GatewayTimeout              &lt; Merb::ControllerExceptions::ServerError; self.status = 504; end
class HTTPVersionNotSupported     &lt; Merb::ControllerExceptions::ServerError; self.status = 505; end</code></pre>
