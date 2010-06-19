Lazytest
========

A Behavior-Driven Development framework for Clojure

by Stuart Sierra, http://stuartsierra.com/


Example Usage
=============

    (ns com.example.my-tests
      (:use lazytest.describe))

    (describe + "with integers"
      (it "adds small numbers"
        (= 7 (+ 3 4)))
      (it "adds large numbers"
        (= 53924864 (+ 41885013 12039851)))
      (it "adds negative numbers"
        (= -10 (+ -4 -6))))



Getting Started with Leiningen
==============================

Put the following in `project.clj`

    (defproject your-project-name "1.0.0-SNAPSHOT"
      :description "Your project description"
      :dependencies [[org.clojure/clojure "1.2.0-master-SNAPSHOT"]
                     [org.clojure/clojure-contrib "1.2.0-SNAPSHOT"]
                     [com.stuartsierra/lazytest "1.0.0-SNAPSHOT"]]
      :repositories {"stuartsierra.com" "http://stuartsierra.com/m2snapshots"})

Put your test sources in `test/`

Then run:

    lein clean
    lein deps
    java -cp "src:test:classes:lib/*" lazytest.watch src test

And watch your tests run automatically whenever you save a file.

Type CTRL+C to stop.



Getting Started with Maven
==========================

Put the following in `pom.xml`

    <dependencies>
      <dependency>
        <groupId>org.clojure</groupId>
        <artifactId>clojure</artifactId>
        <version>1.2.0-master-SNAPSHOT</version>
      </dependency>
      <dependency>
        <groupId>org.clojure</groupId>
        <artifactId>clojure-contrib</artifactId>
        <version>1.2.0-SNAPSHOT</version>
      </dependency>
      <dependency>
        <groupId>com.stuartsierra</groupId>
        <artifactId>lazytest</artifactId>
        <version>1.0.0-SNAPSHOT</version>
      </dependency>
    </dependencies>
    <repositories>
      <repository>
        <id>stuartsierra-snapshots</id>
        <url>http://stuartsierra.com/m2snapshots</url>
        <releases>
          <enabled>false</enabled>
        </releases>
        <snapshots>
          <enabled>true</enabled>
        </snapshots>
      </repository>
      <repository>
        <id>stuartsierra-releases</id>
        <url>http://clojure.org/maven2</url>
        <releases>
          <enabled>true</enabled>
        </releases>
        <snapshots>
          <enabled>false</enabled>
        </snapshots>
      </repository>
      <repository>
        <id>clojars</id>
        <url>http://clojars.org/repo</url>
      </repository>
      <repository>
        <id>clojure-snapshots</id>
        <url>http://build.clojure.org/snapshots</url>
        <releases>
          <enabled>false</enabled>
        </releases>
        <snapshots>
          <enabled>true</enabled>
        </snapshots>
      </repository>
      <repository>
        <id>clojure-releases</id>
        <url>http://build.clojure.org/snapshots</url>
        <releases>
          <enabled>true</enabled>
        </releases>
        <snapshots>
          <enabled>false</enabled>
        </snapshots>
      </repository>
    </repositories>
    <build>
      <plugins>
        <plugin>
          <groupId>com.theoryinpractise</groupId>
          <artifactId>clojure-maven-plugin</artifactId>
          <version>1.3.3</version>
        </plugin>
      </plugins>
    </build>

Put your test sources in `src/test/clojure/`

Then run:

    mvn clojure:repl

And type:

    (use 'lazytest.watch)
    (start ["src"])

And watch your tests run automatically whenever you save a file.

Type CTRL+C to stop.



Making Emacs Indent Tests Properly
==================================

Put the following in `.emacs`

    (eval-after-load 'clojure-mode
      '(define-clojure-indent (describe 'defun) (it 'defun)))



Known Defects
=============

* Changing an applicaton source file does not automatically recompile
  the associated test source file.

* Empty tests are not reported as "pending"

* Failed assertions do not print expected/actual values
