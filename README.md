# clj-migratus

[Migratus](https://github.com/yogthos/migratus) runner for [native Clojure projects](https://clojure.org/reference/deps_and_cli).

## Usage

Add the following to your `deps.edn`:

```
:aliases {:migrate {:extra-deps {com.github.paulbutcher/clj-migratus {:git/tag "v1.0.1"
                                                                      :git/sha "401521e"}}
                     :main-opts ["-m" "clj-migratus"]}}
```

Create a [Migratus configuration](https://github.com/yogthos/migratus#configuration) file. This can either be `migratus.edn`:

```
{:store :database
 :migration-dir "migrations"
 :db {:classname "com.mysql.jdbc.Driver"
      :subprotocol "mysql"
      :subname "//localhost/migratus"
      :user "root"
      :password ""}}
```

Or (recommended) `migratus.clj`, allowing credentials to be taken from the environment:

```
{:store :database
 :db (get (System/getenv) "JDBC_DATABASE_URL")}
```

Then run, for example:

```
$ clj -M:migrate init
$ clj -M:migrate migrate
$ clj -M:migrate create create-user-table
```

See [Migratus Usage](https://github.com/yogthos/migratus#usage) for documentation on each command.
