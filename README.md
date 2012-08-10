# Data::Anonymization

Tool to create anonymized production data dump to use for PREF and other TEST environments.

## Getting started

Install gem using:

    $ gem install data-anonymization

Create ruby program using data-anonymization DSL as following:

```ruby
require 'data-anonymization'

DS = DataAnon::Strategy

database 'DatabaseName' do
  strategy DS::Blacklist  # whitelist (default) or blacklist

  # database config as active record connection hash
  source_db :adapter => 'sqlite3', :database => 'sample-data/chinook-empty.sqlite'

  table 'User' do
    primary_key 'id'
    anonymize 'DateOfBirth' # uses default anonymization based on data types
    anonymize('UserName').using DS::Field::StringTemplate.new('user#{row_number}')
    anonymize 'Password' { |f| "password" }
    ...
  end

  ...

end
```

Run using:

    $ ruby my_dsl.rb

Read more to learn all the features of the tool...

## What is data anonymization?

For almost all the project it is almost a need to have production data dump to run performance tests, rehearsal production releases and debugging production issues.
However, getting production data and using it is not feasible due to multiple reasons and one of them is users personal data in database. And hence the need of data anonymization.
This tool helps you to get anonymized production data dump using either Blacklist or Whitelist strategies.

### Blacklist

### Whitelist



## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request