## LAB - 1
**lab link: <https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-basic-code-context>**

 **Topic :-** 

- Basic server-side template injection (code context).

 **To Solve :-**

- Review the Tornado documentation to discover how to execute arbitrary code, then delete the `morale.txt` file from Carlos's home directory.

 **Procedure :-**

1. Login with credentials, change name and post a comment.
2. Open "change-blog-post-author" request in repeater tab, verify that expression input after "user.name" in "blog-post-author-display" are evaluated on server side as tornado-template.
3. input `}}{%25+import+os+%25}{{os.system('rm%20/home/carlos/morale.txt')` after "user.input", then send request and refresh the page with comment. And voila.


## LAB - 2
**lab link: <https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-using-documentation>**

 **Topic :-** 

- Server-side template injection using documentation.

 **To Solve :-**

- Identify the template engine and use the documentation to work out how to execute arbitrary code, then delete the `morale.txt` file from Carlos's home directory.

 **Procedure :-**

1. Login with cred, then at "edit template", there `${}` syntax. change one of the expression to an non-existing object. it identify the template.(freemaker)
2. Read about its security section and there is a "new" function to create a new template model. read about template model class, there is a "execute" function to process shell command.
3. Create a payload `<#assign ex="freemarker.template.utility.Execute"?new()> ${ ex("rm /home/carlos/morale.txt") }` and put it instead of the expression. then save and reload. And voila.