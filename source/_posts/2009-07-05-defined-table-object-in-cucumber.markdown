---
layout: post
title: 在Cucumber中定义Table对象
---

在开发程序时总会涉及有多个角色（或用户）的场景，再根据角色的不同提供不同的功能，此时的测试用例就会需要有不同的角色数据，Cucumber提供了一个Table对象来解决这个问题，使用起来也非常简单，以下就是一个简单的场景，作用从描述中就可以得知
<pre><code>Feature: Manage Users
In order manage user details
As a security enthusiast
I want to edit user profiles only when authorized
#
Scenario: Show edit link as admin
Given the following user records
| username | password | admin |
| bob          | secret      | false |
| admin      | secret       | true  |
And I am logged in as "admin" with password "secret"
When I visit profile for "bob"
Then I should see "Edit Profile"</code></pre>
<!--more-->
直接运行这个测试，会提示
<pre><code>You can implement step definitions for undefined steps with these snippets:
Given /^the following user records$/ do |table|
# table is a Cucumber::Ast::Table
pending
end</code></pre>
在上面Scenario中，通过block传递了一个自定义的Cucumber Table对象，为了让这个Table对象能够使用，我们只需要使用hashs方法即可。此方法会返回一个hashs的数组对象。数组中每个元素即是以Hash形式表现的Table中的行数据。这时我们就可以使用这些Hash来创建数据了。

通常这个Table对象不会提供非常全的数据项，为了使数据具有完整性，推荐使用Factory_girl来实现，例如：
<pre><code> Given /^the following user records$/ do |table|
table.hashes.each do |hash|
Factory(:user, hash)
end
end </code></pre>
这样我们就可以根据需要来实现自定义的Table对象，方便测试数据的初始化与灵活性了。
