# CakePHP 3.x Mailgun Transport

Send mail via Mailgun SDK in CakePHP 3.0

## Requirements

* PHP 5.4+
* Mailgun SDK
* Composer

## Installation Steps

* 1) Install Mailgun SDK with composer add `"mailgun/mailgun-php" : "1.8"` in composer.json and run `composer update`
* 2) Copy the file MailgunTransport.php in 'src/Mailer/Transport/' folder
* 3) Add configuration in app.php

```json
{
'EmailTransport' => [
		'default' => [
			...
		],
		'mailgun' => [
			'className' => 'Mailgun',
		],
	],
	'Email' => [
		'default' => [
			...
		],
		'mailgun' => [
			'transport' => 'mailgun',
			'mailgun_domain' => 'example.com',
			'mailgun_api_key' => 'key-xxxxxxxxxxxxxxxxxxxxxxxxx'
		],
	],
}
```

And you are good to go.

# Usage

```php

$email = new Email('mailgun');
$result = $email->from(['me@example.com' => 'My Site'])
	->to('you@example.com')
	->subject('Hello')
	
	//->template('get_in_touch')
	//->viewVars(['to' => 'You', 'from' => 'Me'])
	//->emailFormat('both')
	
	->addHeaders(['o:tag' => 'testing'])
	->addHeaders(['o:deliverytime' => strtotime('+1 Min')]);
	->addHeaders(['v:my-custom-data' => json_encode(['max' => 'testing'])])
	
	->readReceipt('admin@example.com')
	->returnPath('bounce@example.com')
	
	->attachments([
		'cake_icon1.png' => Configure::read('App.imageBaseUrl') . 'cake.icon.png',
		'cake_icon2.png' => ['file' => Configure::read('App.imageBaseUrl') . 'cake.icon.png'],
		WWW_ROOT . 'favicon.ico'
	]);
	
	->send('How are you?');

```
