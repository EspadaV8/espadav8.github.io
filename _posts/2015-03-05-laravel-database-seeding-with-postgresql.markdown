---
title: 'Laravel database seeding with PostgreSQL'
date: 2015-03-05 00:00:00 
tags: 
layout: post
---
The usual way to start a seeding file is to have something like the following at the top to clear any existing table data

```php
$this->command->info('Unguarding models');
Model::unguard();
DB::statement('SET FOREIGN_KEY_CHECKS=0;');

$tables = [
	'users',
    'jobs',
];

$this->command->info('Truncating existing tables');
foreach ($tables as $table) {
	DB::table($table)->truncate();
}

// Call all the seeders

DB::statement('SET FOREIGN_KEY_CHECKS=0;');
```

However, this will only work with MySQL. To have something slimiar work with PostgreSQL. PostgreSQL sees something like this as a bad idea (http://www.postgresql.org/message-id/CALnrrJRmFSdee1p8Km8-2cCucSVvk8kzfEMVNBmgyHVuhCusdg@mail.gmail.com). The example in that post (`alter table <tablename> disable trigger all;`) wouldn't work when I tried it within a seeder file, instead I needed to use the following

```php
$this->command->info('Unguarding models');
Model::unguard();

$tables = [
	'users',
    'jobs',
];

$this->command->info('Truncating existing tables');
foreach ($tables as $table) {
	DB::statement('TRUNCATE TABLE ' . $table . ' CASCADE;');
}

// Call all the seeders
```

As the `DB::statement` suggests, this causes the truncate to cascade through any tables that have foreign key references (http://www.postgresql.org/docs/9.4/static/sql-truncate.html).

**N.B.** While typing this up I realised a nicer way would be to simply do

```php
$this->command->info('Unguarding models');
Model::unguard();

$tables = [
	'users',
    'jobs',
];

$this->command->info('Truncating existing tables');
DB::statement('TRUNCATE TABLE ' . implode(',', $tables). ';');

// Call all the seeders
```

Which will cause all the tables to be truncated within one action and avoid any need to check foreign keys. This will only work if you're deleting all tables that have foreign keys with a set table, which for seeding should be fine since you'll more than likely be truncating all the tables anyway.
