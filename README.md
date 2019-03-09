# How to setup a new rails app
## rails new command

`rails new -d postgresql -T -B project_name`

`-d postgresql` : Select postgresql database  
`-T` : Skip basic test files. I prefer to use RSpec  
`-B` : Skip bundle install to setup gemset before to bundle  

## ruby-version and gemset
- Create a file `.ruby-version` containing the version of ruby you want to use (ie `ruby-2.5.3`)
- Create a file `.ruby-gemset` containing the wanted **unique** name for the gemset (ie `my-project-name`)
- In the Gemfile, replace the line `ruby-2.5.3` by `File.read('./.ruby-version')` to avoid any contradictory information about ruby version.
- Get out and back of the repo to setup gemset

## Git
- Add `.DS_Store` in `.gitignore` if your're using mac_OS
- Add `.env` in `.gitignore` even if you don't know if you're going to use `dotenv` or not. This could avoid aftertime regretable forgetting...  

## Clean code
- Add the following gems in the development group of your Gemfile :
  - rubocop
  - annotate
  - husky
- Run `bundle install`
- Create `rubocop.yml` in the root of your application in order to use the relaxed style guide :
```
inherit_from:
 - http://relaxed.ruby.style/rubocop.yml

AllCops:
 DisplayStyleGuide: true
 DisplayCopNames: true
 Exclude:
   - ‘db/schema.rb’
   - ‘vendor’
   - ‘config/environments/*.rb’
   - ‘bin/*’

Rails:
 Enabled: true

Layout/IndentationConsistency:
 EnforcedStyle: rails
```

- Run `rubocop -a` in order to fix gems order and #froozen_string_literal offenses.  
At this step, you shouldn't have offenses rubocop can't fix itself.
- Run `npm install husky --save-dev`
- Add husky in `package.json` as following :
```  
{
  "name": "ECommerce",
  "private": true,
  "dependencies": {},
  "husky": {
    "hooks": {
      "pre-commit": "rubocop && annotate",
      "pre-push": "rspec"
    }
  },
  "devDependencies": {
    "husky": "^1.3.1"
  }
}
```
- Make your first commit `App setup` in order to check if husky is correctly working.
