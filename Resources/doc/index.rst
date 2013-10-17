DirectBundle
============

DirectBundle is an implementation of ExtDirect specification to Symfony2
framework.

Installing
----------

The best way to install DirectBundle into your project is using composer.

.. code-block:: Json
    
    //composer.json
    {
        "require": {
            "oaugustus/direct-bundle": "dev-master"
        }
    }

Then update your composer: ``composer update``

Register DirectBundle into your application kernel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: php

    // app/AppKernel.php
    public function registerBundles()
    {
        $bundles = array(
            // ...,
            new Neton\DirectBundle\DirectBundle(),
            // ...,
        );

        //..
        return $bundles;
    }


Register DirectBundle route into your route config
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: yml

    // app/config/routing.yml
    # ... your other routes here
    direct:
        resource: "@DirectBundle/Resources/config/routing.yml"


How to use
----------

Add the ExtDirect API into your page
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you is using Twig engine, only add the follow line in your views page at the
script section:

.. code-block:: html

    <script type="text/javascript" src="{{ url('api')}}"></script>


Or if you are not using a template engine:

.. code-block:: html

    <script type="text/javascript" src="http://localhost/symfony-sandbox/web/app.php/api.js"></script>


Expose your controller methods to ExtDirect Api
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: php

    // ...
    namespace Neton\HelloBundle\Controller;

    // importing annotation references into your controller
    use Neton\DirectBundle\Annotation\Form as form;
    use Neton\DirectBundle\Annotation\Remote as remote;


    class TestController extends Controller
    {
       /*
        * Single exposed method.
        *
        * @remote    // this annotation expose the method to API
        * @param  array $params
        * @return string
        */
        public function indexAction($params)
        {
            return 'Hello '.$params['name'];
        }

        /*
         * An action to handle forms.
         *
         * @remote   // this annotation expose the method to API
         * @form     // this annotation expose the method to API with formHandler option
         * @param array $params Form submited values
         * @param array $files  Uploaded files like $_FILES
         */
        public function testFormAction($params, $files)
        {
            // your proccessing
            return true;
        }
    }


Call the exposed methods from JavaScript
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: js

    // Hello is the Bundle name without 'Bundle'
    // Test is the Controller name without 'Controller'
    // index is the method name without 'Action'
    Actions.Hello_Test.index({name: 'Otavio'}, function(r){
       alert(r);
    });


Finished
~~~~~~~~

Well, this all to DirectBundle work. Suggestions, bug reports and observations
are wellcome.
