# Your Bundle Skeleton

This is a minimal and empty project which can be used in order to build your bundle with Symfony 4.* !

**/!\ Don't forget to :**
- Respect Case-sensitivity !
- Change namespaces when converting your projecting into a bundle !


##### This is how your root should look like :

    <your-bundle>/
    ├─ NameNameBundle.php
    ├─ Controller/
    ├─ README.md
    ├─ LICENSE
    ├─ Resources/
    │   ├─ config/
    │   ├─ doc/
    │   │  └─ index.rst
    │   ├─ translations/
    │   ├─ views/
    │   └─ public/
    └─ Tests/


### **composer.json of the bundle**

    {
        "name": "name/name",
        "minimum-stability": "dev",
      "autoload": {
        "psr-4": {
          "Name\\Bundle\\Name\\":"vendor/Name/Name"
        }
      },
      "autoload-dev": {
        "psr-4": {
          "Name\\Bundle\\Name\\": "vendor/Name/Name"
        }
      }
    }

### **composer.json of the project**

        "autoload": {
            "psr-4": {
                "App\\": "src/",
                "Name\\Bundle\\Name\\":"vendor/Name/Name"
            }
        },
        "autoload-dev": {
            "psr-4": {
                "App\\Tests\\": "tests/",
                "Name\\Bundle\\Name\\":"vendor/Name/Name"
            }
    

### **bundle controller**

    <?php
    
    namespace Name\Bundle\Name;
    
    use Symfony\Component;
    use Symfony\Component\HttpKernel\Bundle\Bundle;
    
    
    class NameName extends Bundle{}

### **Bundles.php**

    Name\Bundle\Name\NameName::class => ['all' => true],


### **Routes.yaml** 
*in order to link annotations of the bundle controllers to the project*

- first add this to your controllers (where you have written all the routes) :


        use Sensio\Bundle\FrameworkExtraBundle\Configuration\Method;
    

- & then you can write down in Routes.yaml :

    
        app_annotations:
            # loads routes from the PHP annotations of the controllers found in that directory
            resource: '..\vendor\Name\Name\Controller\'
            type:     annotation



### **Console** 
*in order to add all Bundle resources in the public directory of the project*

    bin/console assets:install

*if you don't want to make this every time add attribute --symlink*

    php app/console assets:install --symlink



*If you get the error "Attempted to load class " Bundle" from namespace "Name\Bundle\Name". Did you forget a "use" statement for another namespace?"*

    composer dump-autoload


### **Routing**

If your index.html.twig is in *Your_Bundle/Resources/views*

    return $this->render('@NameName/index.html.twig');



### **Tests with Kahlan**

You should first look at [Kahlan's documentation](https://kahlan.github.io/docs/) 

- This is how you use unit test for your bundle in your final project :


        vendor/bin/kahlan --spec=vendor/Name/Name/Tests --src=vendor/Name/Name
    
    
- & if you need any details :


        vendor/bin/kahlan --spec=vendor/Name/Name/Tests --src=vendor/Name/Name --cc=true --reporter=verbose
