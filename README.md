# PHP RabbitMQ Management API

Requirements
====
- PHP >= 7.0
- [php guzzle/guzzle](https://github.com/guzzle/guzzle)

Installation
====
1. Download and Install PHP Composer.

   ``` sh
   curl -sS https://getcomposer.org/installer | php
   ```

2. Next, run the Composer command to install the latest version.
   ``` sh
   php composer.phar require squeezely/rabbitmq-management-api
   ```

   
How to use:
====
```php
<?php
use RabbitMQManagement\Configuration\AbstractConfiguration;
use RabbitMQManagement\Configuration\ArrayConfiguration;
use RabbitMQManagement\Vhost\VhostService;
use RabbitMQManagement\Cluster\ClusterService;


$config = new AbstractConfiguration('my.host.com', 15672, 'http', 'user', 'password');
$config = new ArrayConfiguration([
    'hostname' => 'my.host.com',
    'port' => 15672,
    'protocol' => 'http',
    'username' => 'user',
    'password' => 'password'
]);

$vhostService = new VhostService($config);

if($vhostService->createVhost('somevhost', true))
    $vhost = $vhostService->getVhost('somevhost');

foreach($vhostService->getVhosts() as $vhost) {
    var_dump(
        $vhost->getName(),
        $vhost->getTopicPermissions(), 
        $vhost->getPermissions(), 
        $vhost->getData()
    );
}

$clusterService = new ClusterService($config);
var_dump(
    $clusterService->getExtensions(),
    $clusterService->getNodes(),
    $clusterService->getClusterName(),
    $clusterService->getOverview()
);

```

License
====

squeezely/rabbitmq-management-api is licensed under the MIT License - see the LICENSE file for details