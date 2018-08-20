# Steps to get started

Requirements:
Your local development environment must provide [a webserver like Apache or nginx, PHP 7.1+, composer and MySQL 5.7.x or MariaDB 10.2.x](https://www.neos.io/download-and-extend.html).

#### Start a new git project

1. Clone this repository `git clone git@github.com:code-q-web-factory/Neos-Skeleton.git PROJECT_NAME`
2. Replace the Package name "CodeQ.Site" with your own company name. We recommend keeping ".Site" for all projects to easily copy the code from one project to another.
    ```
    export REPO_NAME="MyFirstWebsite"
    export NEOS_PACKAGE_NAME="YourCompany.Site"
    export COMPOSER_PACKAGE_NAME="yourcompany\/site"
    cd ${REPO_NAME}
    mv DistributionPackages/CodeQ.Site DistributionPackages/${NEOS_PACKAGE_NAME}
    find ./DistributionPackages/${NEOS_PACKAGE_NAME} -type f | xargs sed -i '' "s/CodeQ\.Site/${NEOS_PACKAGE_NAME}/g"
    find . -type f -name 'composer.json' | xargs sed -i '' "s/codeq\/site/${COMPOSER_PACKAGE_NAME}/g"
    ```
3. Create a new git project on the server of your choice, in our example Github
4. Start the new git project locally and push the initial state
    ```
    rm -rf .git && git init
    git remote add origin git@github.com:${REPO_NAME}.git
    git fetch
    composer install
    git add .
    git commit -m "TASK: Copy from Neos-Skeleton"
    git push -u origin master
    ```

#### Run the project locally

5. Start your database server and create a new database with the encoding **utf8mb4** and the collation **utf8mb4_unicode_ci** (Be careful: Don't confuse it with *utf8mb4_general_ci*, which is the default for some database management tools. This can lead to hard-to-debug issues later on.)
6. Start the local server in the terminal:
    ```
    ./flow server:run
    ```
7. Setup the database configuration at [http://127.0.0.1:8081/setup](http://127.0.0.1:8081/setup) and import the initial content from your package.

#### Configure your project

8. Configure the Google Analytics tracking code in [Production/Settings.yaml](DistributionPackages/CodeQ.Site/Configuration/Production/Settings.yaml) in the format `UA-XXXXXXXX-X`
9. German is the default language, you can adapt it in [Settings.Language.yaml](DistributionPackages/CodeQ.Site/Configuration/Settings.Language.yaml)
10. In the Neos administration, you can find a page "Page not found", which is shown every time a page couldn't be found. Feel free to add content here.

#### Start developing

11. Copy your preferred frontend tooling into Resources/Public/Frontend and adopt the include assets paths in [Settings.IncludeAssets.yaml](DistributionPackages/CodeQ.Site/Configuration/Settings.IncludeAssets.yaml)
12. Create your own document and content node types and add the styles to your CSS.

#### Tip:
Folow the [Code Q Code Conventions](https://docs.google.com/document/d/13ykoM0Ta2qJvO_6BYa-DIsx7_MxFsInOSbJqJHuINBw/edit?usp=sharing) and validate your code with
```
./flow configuration:validate
./flow guidelines:validateDistribution
./flow guidelines:validatePackages
```
