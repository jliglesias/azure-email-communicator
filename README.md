# Microsoft Azure Mailer Driver for Laravel

Provides Azure Communication Service integration for Symfony Mailer / Laravel.

## Requirements

- PHP 8.2 or higher.
- [Laravel 10.x](https://laravel.com/docs/10.x) or higher.
- [Azure account](https://azure.com), Azure CS Access Key and Service Endpoint.

## Installation

First time using Azure ECS? Create your [Azure account](https://azure.com), if you don’t have one already.

1. Download [Composer](https://getcomposer.org/doc/00-intro.md) if not already installed

2. On your project directory run on the command line
`composer require jliglesias/laravel-azure-mailer`

3. Get your Azure CS Access Key and Service Endpoint.

## Configuration

Add entry to [root-of-laravel]/config/mail.php:
```php
  <?php

    ...

    'mailers' => [
        //...other drivers

        'azure' => [
            'transport'             => 'azure',
            'resource_name'         => env('AZURE_MAIL_RESOURCE_NAME'),
            'endpoint'              => env('AZURE_MAIL_ENDPOINT', 'https://my-acs-resource-name.communication.azure.com'),
            'access_key'            => env('AZURE_MAIL_KEY'),
            'api_version'           => env('AZURE_MAIL_API_VERSION', '2023-03-31'),
            'disable_user_tracking' => env('AZURE_MAIL_DISABLE_TRACKING', false),
            'sender_address'        => env('AZURE_MAIL_SENDER_ADDRES', 'donotreply@azure.com')
        ],
    ]

  ?>
```
Add entry to [root-of-laravel]/.env:
  
```text 
  
  #...other entries

  # Mail service entries... 
  MAIL_MAILER=azure
  
  #=================================================
  # Azure Service entries
  #=================================================
  AZURE_MAIL_RESOURCE_NAME=my-acs-resource-name
  AZURE_MAIL_KEY=AzureAccessToken
  AZURE_MAIL_SENDER_ADDRES
  
```
## Documentation

Build powerful, cloud-based communication and customer engagement experiences by adding email integration with Azure Communication Service to your apps.

 - Azure Communication Service Docs: [English](https://learn.microsoft.com/en-us/azure/communication-services/)
 - Prepare Email Communication resource for Azure Communication Service Docs: [English](https://learn.microsoft.com/en-us/azure/communication-services/concepts/email/prepare-email-communication-resource/)
 - Sending mail with Laravel (10x): [English](https://laravel.com/docs/10.x/mail#sending-mail)

 ## Examples

Simple mail sending:

```text 
Mail::to($request->user())
    ->cc($moreUsers)
    ->bcc($evenMoreUsers)
    ->send(new OrderShipped($order));
```
or
```text 
Mail::to([new Address('user.name@domain.com', 'My User Name'), ...])
    ->cc([new Address('user.name@domain.com', 'My User Name'), ...])
    ->bcc([new Address('user.name@domain.com', 'My User Name'), ...])
    ->send('my.view');
```
Sending mail with attachments:
```text 
$data = [
      to => [new Address('user.name@domain.com', 'My User Name'), ...],
      subject => 'Subject'
];
$files = [
      public_path('files/160031367318.pdf'),
      public_path('files/1599882252.png'),
];

Mail::send('my.view', $data, function($message)use($data, $files) {
            
            $message->to($data["to"])
                    ->subject($data["subject"]);

            foreach ($files as $file){
                $message->attach($file);
            }

 });
```
If you need more information, read the Laravel (10x) documentation: [English](https://laravel.com/docs/10.x/mail)

 ## Last change

 ** [0.1.0-beta.1](https://github.com/jliglesias/laravel-azure-mailer/blob/master/CHANGELOG.md#010)
  * Main release.

 ** [0.1.1.-beta.1](https://github.com/jliglesias/laravel-azure-mailer/blob/master/CHANGELOG.md#011)
  * Remove folders and files for testing event dispatch and callbacks using AJAX (JQUERY).

## License 

MIT license. Copyright (c) 2024 - [Juan Luis Iglesias](https://github.com/jliglesias)
For more information, see the [LICENSE](https://github.com/jliglesias/azure-email-communicator/blob/main/LICENSE) file.