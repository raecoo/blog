---
layout: post
title: Cheat DataMapper
---

DataMapper, the ruby object relational mapper
website:  http://www.datamapper.org
git:      git://github.com/sam/dm-core.git
mail:     http://groups.google.com/group/datamapper
now:      http://www.twitter.com/datamapper
bugs:     http://datamapper.lighthouseapp.com/projects/20609-datamapper/

Setting up a Connection
<pre><code> DataMapper.setup(:default, "adapter://user:password@hostname/dbname")
supported adapters: mysql, sqlite3, postgres, sqlite3::memory:
additional adapters are in dm-more, (couchdb, rest, imap, file, saleforce...)</code></pre>
<!--more-->
Creating a Model (with properties)
<pre><code> class Zoo
include DataMapper::Resource
property :id, Serial
end</code></pre>

Properties
<pre><code> property :id,   Serial               # auto-incrementing PK
property :name, String, :key =&gt; true # natural key
# you must specify &gt;= 1 key, CPK support 100%</code></pre>

# available data-types
property :description, Text # (lazy by default)
property :created_at,  DateTime
property :open,        Boolean
property :admission,   BigDecimal

# require dm-types for Csv, Enum, EpochTime, FilePath, Flag,
#  IPAddress, URI, Yaml

Property Options (pass as hash)
<pre><code> :default, :nullable, :field (column name), :size, :length, :format,
:index, :unique_index, :ordinal, :auto_validate, :precision,
:scale, :accessor, :reader, :writer, :lazy</code></pre>

Finders
<pre><code> Zoo.get(PK_HERE)
Zoo.first({see_below})
Zoo.all({see_below})</code></pre>

Finder Options (pass as hash)
<pre><code> :conditions =&gt; ["property = ? and property = ?", 'value', 'value']
:conditions =&gt; {:property =&gt; 'value', ...}
:property =&gt; 'ZooNameHere'
# any non-standard key =&gt; value pair is assumed a condition if not
# otherwise recognized
:property.lte =&gt; 12.00  # &lt;=
.gte           # &gt;=
.gt            # &gt;
.lt            # &lt;
.not           # NOT =
.like          # LIKE
.in            # IN ()
'class.property' =&gt; 'value'
Class.relationship.property =&gt; 'value' # will automatically issue JOINS</code></pre>

Finder Gotcha
<pre><code> :order =&gt; [:created_at.desc, ...] # descending sort
.asc        # ascendi</code></pre>ng

Associations
<pre><code> has 1                    # has_one
has n                    # has_many
belongs_to :things
has n, :things, :through =&gt; :more_things
has n, :things, :through =&gt; Resource # has_and_belongs_to_many</code></pre>

Association Options
(any Finder Options)
<pre><code> :class_name =&gt; 'ClassNameHere'
:order =&gt; [:property.desc]
:child_key =&gt; [:property, ...]
:through =&gt; :other_association</code></pre>

Validations (require 'dm-validations')
<pre><code> validates_present     :title
validates_is_number   :rating
validates_format      :email, :as =&gt; :email_address
validates_length      :summary, :in =&gt; (1..100)
validates_is_unique   :slug
validates_with_method (do...end, :method_name)</code></pre>

Callbacks AKA "Hooks"
<pre><code> Object-level
before :method_name, (do...end, :another_method_name)
after  :method_name, (do...end, :another_method_name)
Class-level
before_class_method :method_name, (do...end, :another_method_name)
after_class_method  :method_name, (do...end, :another_method_name)</code></pre>

Callbacks Gotcha
<pre><code> Hooks act on 'self' and aren't passed an arguement
'self' for object-level hooks are the instance
'self' for class-level hooks are the class itself</code></pre>

Misc. Stuff &amp; Gotchas
<pre><code> Single Table Inheritance
property :type, Discriminator # then inherit from this model</code></pre>

Paranoia
<pre><code> property :deleted_at, ParanoidDateTime
property :deleted,    ParanoidBoolean</code></pre>

Multiple DB Connections
<pre><code> DataMapper.setup(:external, "adapter://username:password@hostname/dbname")
repository(:external) do...end
Association: has n, :things, :repository =&gt; repository(:external)
Finder: Thing.all(:repository =&gt; repository(:external))</code></pre>
