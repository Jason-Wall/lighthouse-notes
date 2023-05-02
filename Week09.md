# Week 09

## Rails

Debugging tricks:\
`raise <object>.inspect` will produce an error in the browser that outputs a stringy version of the object.\

Adding a column to a table the right way...\
`rails g migration add_column_name_to_table_name column_name:data_type` \

Generating a new controller:\
`rails generate controller <controllerName>`

View all your routes in the browser.
http://localhost:3000/rails/info/routes

How to add user auth in Rails:
[https://gist.github.com/thebucknerlife/10090014](https://gist.github.com/thebucknerlife/10090014)

Console - Like node:

```rb
bin/rails c
#Then you can do all kinds of commands - Like check your database:
Sale.first
Sale.all
Sale.create! name: "X-mas Sale", starts_on:'Dec5, 2023', ends_on:'Jan 3, 2024'


```
## Rpsec
Testing library for ruby:\
`gem install rspec`
Create a new testing framework inside your project:
`rspec --init`
Add `--format documentation` to the .rspec file for nicer test output.

