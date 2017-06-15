# Upgrade from 1.7 to 2.0

### Client options

- The `verify_ssl` option has been renamed to `ssl_verification`.
- The `ca_cert` option has been renamed to `ssl_ca_file`.
- The `environment` option has been renamed to `current_environment`.
- The `http_proxy` option has been renamed to `proxy`.
- The `processorOptions` option has been renamed to `processors_options`.
- The `exclude` option has been renamed to `excluded_exceptions`.
- The `send_callback` option has been renamed to `should_capture`.
- The `name` option has been renamed to `server_name`.
- The `project` option has been removed.
- The `extra_data` option has been removed in favour of setting additional data
  directly in the context.
- The `open_timeout` option has been added to set the maximum number of seconds
  to wait for the server connection to open.
- The `excluded_loggers` option has been added to set the list of logger 'progname's
  to exclude from breadcrumbs.
- The `environments` option has been added to set the whitelist of environments
  that will send notifications to Sentry.
- The `serialize_all_object` option has been added to configure whether all the
  object instances should be serialized.
- The `context_lines` option has been added to configure the number of lines of
  code context to capture.

### Client

- The constructor of the `Client` class has changed its signature. The only way
  to set the DSN is now to set it in the options passed to the `Configuration`
  class.

  Before:

  ```php
  public function __construct($options_or_dsn = null, $options = array())
  {
      // ...
  }
  ```

  After:

  ```php
  public function __construct(Configuration $config)
  {
      // ...
  }
  ```

- The methods `Client::getRelease` and `Client::setRelease` have been removed.
  You should use `Configuration::getRelease()` and `Configuration::setRelease`
  instead.

  Before:

  ```php
  $client->getRelease();
  $client->setRelease(...);
  ```

  After:

  ```php
  $client->getConfig()->getRelease();
  $client->getConfig()->setRelease(...);
  ```

- The methods `Client::getEnvironment` and `Client::setEnvironment` have been
  removed. You should use `Configuration::getCurrentEnvironment` and
  `Configuration::setCurrentEnvironment` instead.

  Before:

  ```php
  $client->getEnvironment();
  $client->setEnvironment(...);
  ```

  After:

  ```php
  $client->getConfig()->getCurrentEnvironment();
  $client->getConfig()->setCurrentEnvironment(...);
  ```

- The methods `Client::getDefaultPrefixes` and `Client::setPrefixes` have been
  removed. You should use `Configuration::getPrefixes` and `Configuration::setPrefixes`
  instead.

  Before:

  ```php
  $client->getPrefixes();
  $client->setPrefixes(...);
  ```

  After:

  ```php
  $client->getConfig()->getPrefixes();
  $client->getConfig()->setPrefixes(...);
  ```

- The methods `Client::getAppPath` and `Client::setAppPath` have been removed.
  You should use `Configuration::getProjectRoot` and `Configuration::setProjectRoot`
  instead.

  Before:

  ```php
  $client->getAppPath();
  $client->setAppPath(...);
  ```

  After:

  ```php
  $client->getConfig()->getProjectRoot();
  $client->getConfig()->setProjectRoot(...);

- The methods `Client::getExcludedAppPaths` and `Client::setExcludedAppPaths`
  have been removed. You should use `Configuration::getExcludedProjectPaths`
  and `Configuration::setExcludedProjectPaths` instead.

  Before:

  ```php
  $client->getExcludedAppPaths();
  $client->setExcludedAppPaths(...);
  ```

  After:

  ```php
  $client->getConfig()->getExcludedProjectPaths();
  $client->getConfig()->setExcludedProjectPaths(...);

- The methods `Client::getSendCallback` and `Client::setSendCallback` have been
  removed. You should use `Configuration::shouldCapture` and `Configuration::setShouldCapture`
  instead.

  Before:

  ```php
  $client->getSendCallback();
  $client->setSendCallback(...);
  ```

  After:

  ```php
  $client->getConfig()->shouldCapture();
  $client->getConfig()->setShouldCapture(...);

- The method `Client::getServerEndpoint` has been removed. You should use
  `Configuration::getServer` instead.

  Before:

  ```php
  $client->getServerEndpoint();
  ```

  After:

  ```php
  $client->getConfig()->getServer();
  ```

- The method `Client::getTransport` has been removed. You should use
  `Configuration::getTransport` instead.

  Before:

  ```php
  $client->getTransport();
  ```

  After:

  ```php
  $client->getConfig()->getTransport();
  ```

- The method `Client::getErrorTypes` has been removed. You should use
  `Configuration::getErrorTypes` instead.

  Before:

  ```php
  $client->getErrorTypes();
  ```

  After:

  ```php
  $client->getConfig()->getErrorTypes();
  ```

- The `Client::getDefaultProcessors` method has been removed.

### Client builder

- To simplify the creation of a `Client` object instance, a new builder class
  has been added.

  Before:

  ```php
  $client = new Client([...]);
  ```

  After:

  ```php
  $client = new Client(new Configuration([...]));

  // or

  $client = ClientBuilder::create([...])->getClient();
  ```