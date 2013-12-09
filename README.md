54.206.2.225 localhost.lan
54.206.2.225 development.localhost.lan
ec2-54-206-1-99.ap-southeast-2.compute.amazonaws.com

https://github.com/jmcunningham/AngularJS-Learning

-----------------
You are about to add the following PPA to your system:

 More info: https://launchpad.net/~cartodb/+archive/mapnik
Press [ENTER] to continue or ctrl-c to cancel adding it

gpg: keyring `/tmp/tmpWp3Euh/secring.gpg' created
gpg: keyring `/tmp/tmpWp3Euh/pubring.gpg' created
gpg: requesting key D878D6C2 from hkp server keyserver.ubuntu.com
gpg: /tmp/tmpWp3Euh/trustdb.gpg: trustdb created
gpg: key D878D6C2: public key "Launchpad PPA for CartoDB" imported
gpg: Total number processed: 1
gpg:               imported: 1  (RSA: 1)
OK

--------------

https://github.com/CartoDB/cartodb/wiki/Problems-faced-during-CartoDB-install-&-solutions-if-known

--------------


网上论坛
	发布回复		
第 1 个，共 99+ 个（99+ 个未读）  


我的论坛
首页
加星标的主题


收藏夹
点击论坛的星标即可收藏它


最近看过的论坛
cartodb
v8-users
sinatrarb
ruby-bundler
nokogiri-talk


最近发过帖的论坛
cartodb
隐私权政策 - 服务条款
cartodb ›
#<NoMethodError: undefined method `email=' for #<User @values={}>>
6 名作者发布了 15 个帖子  



Ivo Jerkovic 	
9月30日

将帖子翻译为中文  

I tried to create a user using create_dev_user script and I got this error. Table USERS remains empty.
Does anyone have a clue what is this problem about?
Thank you in advance.
点击此处回复

9月30日

 strk Sounds like an unexpected database structure was found. The code expects a table "users" with a column "email" in the cartodb (meta) database (carto_db_<environment>). Check it out. --strk;



David Chappel 	
10月5日

将帖子翻译为中文  

I get the same error.  The database is created with an empty users table. 

Cheers,
D
- 显示引用文字 -
 


David Chappel 	
10月5日

将帖子翻译为中文  

I'm digging into it.   (Total ruby noob so bear with me!)

--- Creating databases
/home/cartodb/cartodb20/lib/importer/lib/cartodb-importer/importer.rb:20: warning: already initialized constant SUPPORTED_FORMATS
** Invoke cartodb:db:setup (first_time)
** Invoke db:create (first_time)
** Invoke environment (first_time)
** Execute environment
** Execute db:create
[sequel] Created database 'devdb'
[sequel] Created database 'testdb'
** Invoke db:migrate (first_time)
** Invoke db:migrate:load (first_time)
** Invoke environment 
** Execute db:migrate:load
** Execute db:migrate
** Invoke db:schema:dump (first_time)
** Invoke environment 
** Execute db:schema:dump
** Invoke cartodb:db:create_publicuser (first_time)
** Invoke environment 
** Execute cartodb:db:create_publicuser
** Execute cartodb:db:setup
#<NoMethodError: undefined method `email=' for #<User @values={}>>
- 显示引用文字 -
 


Alejandro Martinez @Vizzuality 	
10月5日

将帖子翻译为中文  

We have an ongoing issue with the setup scripts, can you try to just 
run the script again with the same parameters and see if it works that 
way? 

(this is due to Rails not being reloaded after running rake 
db:migrate, which makes it not properly detect the DB structure) 
- 显示引用文字 -
> -- 
> 
> --- 
> You received this message because you are subscribed to the Google Groups 
> "cartodb" group. 
> To unsubscribe from this group and stop receiving emails from it, send an 
> email to cartodb+u...@googlegroups.com. 
> For more options, visit https://groups.google.com/groups/opt_out. 
 


David Chappel 	
10月7日

将帖子翻译为中文  

I've run it numerous times with the same results.

My process is:
-the system is not running.  (I use "rvmsudo bundle exec foreman start -p 80")
-start the redis server.  (service start...)
-I drop the test and development dbs.
-run the script.

I want to say, btw, thank you for your help!!!!!   I appreciate it!

D
- 显示引用文字 -
 


Staniel 	
10月8日

将帖子翻译为中文  

Hi， I came across exactly the same email problem with you. But when I try the same command again, the error message changes to the follow:

--- Creating databases
/home/omnilab/cartodb20/lib/importer/lib/cartodb-importer/importer.rb:20: warning: already initialized constant SUPPORTED_FORMATS
createdb: database creation failed: ERROR:  database "carto_db_development" already exists
[sequel] Created database 'carto_db_development'
createdb: database creation failed: ERROR:  database "carto_db_test" already exists
[sequel] Created database 'carto_db_test'
#<Sequel::DatabaseError: PGError: fe_sendauth: no password supplied

I am new to CartoDB and not sure what happening. If carto_db_development exists already, how to remove it? 

BTW, have you solve the email problem?
Staniel

在 2013年10月7日星期一UTC+8下午11时41分44秒，David Chappel写道：
- 显示引用文字 -
 


David Chappel 	
10月8日

将帖子翻译为中文  


I believe you need to edit the <cartodb20?>/config/app_config.yml and database.yml files.   As the postgres user delete these databases prior to running the script.  Also create users that are referenced in the database.yml file.  The postgis users should have the ability to create users and databases. I'm a newbie but I think that should help.
I have not sorted the email problem.  I've create a new function "email=" in the User class which throws an exception and a stack trace to find out where the email= function is called.  Ruby is an interesting language.

D




- 显示引用文字 -
- 显示引用文字 -
-- 
 
--- 
You received this message because you are subscribed to a topic in the Google Groups "cartodb" group.
To unsubscribe from this topic, visit https://groups.google.com/d/topic/cartodb/cI_O5FQp5Ro/unsubscribe.
To unsubscribe from this group and all its topics, send an email to cartodb+u...@googlegroups.com.

For more options, visit https://groups.google.com/groups/opt_out.

 


么立新 	
10月9日

将帖子翻译为中文  

I know these two files are related to my problems. Before I met the problem I set the password manually in database.yml. Can you give me some detail instruction about how to create a new user and delete the old database, like what content should I add or delete? I'm truly a newbie and it's hard to explore the whole stuff. Thanks!

Staniel


2013/10/8 David Chappel <david....@gmail.com>
- 显示引用文字 -

 


David Chappel 	
10月11日

将帖子翻译为中文  

I'm assuming your on a Linux system right?
It is pretty easy.  All you need to do is create a couple users that have the ability to create databases.

To do this you need to become the postgres users. (su postgres as root or sudo su postgres etc.)
now the postgres user can createdb and createuser.  In this case we only need a user.
http://www.postgresql.org/docs/9.1/static/app-createuser.html
The script creates the database as defined in the database.yml file.
so something like :
createuser --createdb --pwprompt development
It should prompt you for a password (same as you put in database.yml) etc.


The corresponding commands also exist: dropuser and dropdb.   
If you left the database names as default, you can type as postgres before the script is run:
dropdb carto_db_development
and
dropdb carto_db_test


You can also create users when dropping into the psql shell but please remember to use quotes to preserve case.

Hope that helps!
D
- 显示引用文字 -
 


么立新 	
10月11日

将帖子翻译为中文  

Thanks David, I got over the create database problem, the dropdb command helps.But the email issue is still there. I'm not sure what you mean by saying  "create a new function "email=" in the User class ". Which file do I need to edit? And how? Please excuse me for knowing nothing about Ruby…… 

Best Regards,
Staniel


2013/10/11 David Chappel <david....@gmail.com>
- 显示引用文字 -

 


David Chappel 	
10月11日

将帖子翻译为中文  

I'm stuck there too.  It was (from memory) the User class but the new setter does not solve the issue.  The email member is  is not set.   I haven't had the time to battle it--I'm ignorant of ruby too.

- 显示引用文字 -
 


么立新 	
10月11日

将帖子翻译为中文  

It was so sad to stuck here, seems almost finish all the process except this one. Anyway thank you for your help!


- 显示引用文字 -
 


strk 	
10月11日

将帖子翻译为中文  

On Fri, Oct 11, 2013 at 10:31:33AM +0800, 么立新 wrote: 
> It was so sad to stuck here, seems almost finish all the process except 
> this one. Anyway thank you for your help! 

Have you seen if a ticket for this problem exists on the github bug tracker ? 
If not, I suggest you file one: https://github.com/cartodb/cartodb/issues 
There's also a wiki page about troubleshooting: 
https://github.com/CartoDB/cartodb20/wiki/Problems-faced-during-CartoDB-install-&-solutions-if-known 

Looking forward to your contributions :) 

--strk(also frustrated by ruby); 

 


tomay 	
上午5:08（3 小时前）

将帖子翻译为中文  

I'm wondering if anyone has solved this issue (can't create user), or found a work-around. I'm also getting the same error:
#<NoMethodError: undefined method `email=' for #<User @values={}>>

I notice the issue opened here: https://github.com/CartoDB/cartodb/issues/259 
but this doesn't seem to have been resolved. 

I get the same error manually running "rake cartodb:db:create_user" as suggested at the end of that discussion by strk
- 显示引用文字 -
 
------------------------

Datasource should be fully configurable from Windshaft-CartoDB, 
when it sets up the graintore configuration in lib/cartodb/server_options.js 

More tweaks can be done based on request parameters from the 
req2param callback. 
