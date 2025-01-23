# Chimoney-Laravel-SDK-Documentation
Installation guide for Chimoney Laravel SDK 

The Chimoney Laravel SDK provides an easy way to interact with the Chimoney API within your Laravel applications. This guide will walk you through installing, setting up, and using the SDK effectively.

---

## Installation Instructions

### Prerequisites
Ensure the following before proceeding:
- PHP 7.4 or higher
- Laravel 8.x or higher
- Composer installed on your system

### Installation
1. Use Composer to install the Chimoney Laravel SDK:

   ```bash
   composer require chimoney/laravel-sdk
   ```

2. Publish the configuration file to customize settings:

   ```bash
   php artisan vendor:publish --provider="Chimoney\LaravelSdk\ChimoneyServiceProvider"
   ```

This will create a `chimoney.php` configuration file in your `config` directory.

---

## Configuration Details

### Setting Environment Variables
Add the following variables to your `.env` file:

```env
CHIMONEY_API_KEY=your_api_key_here
CHIMONEY_BASE_URL=https://api.chimoney.io
```

### Configuring the SDK
The SDK uses the `config/chimoney.php` file to manage settings. Ensure your API key and base URL are correctly defined.

---

## Usage Guide

### Authenticating
Ensure your `.env` file contains the correct `CHIMONEY_API_KEY`. The SDK will use this key for authentication.

### Making API Requests
Here are some common operations with code examples:

#### Fetching Account Balance
```php
use Chimoney\LaravelSdk\Chimoney;

$chimoney = new Chimoney();
$response = $chimoney->getBalance();

if ($response->success) {
    echo 'Balance: ' . $response->data['balance'];
} else {
    echo 'Error: ' . $response->message;
}
```

#### Sending Payments
```php
use Chimoney\LaravelSdk\Chimoney;

$chimoney = new Chimoney();
$response = $chimoney->sendPayment([
    'recipient' => 'test@example.com',
    'amount' => 100,
    'currency' => 'USD'
]);

if ($response->success) {
    echo 'Payment sent successfully!';
} else {
    echo 'Error: ' . $response->message;
}
```

### Handling Responses
The SDK returns a standard response object:
- `success`: Boolean indicating success or failure
- `data`: Data returned from the API
- `message`: Error or success message

---

## Testing Instructions

### Verify Installation
Run the following Artisan command to check if the SDK is correctly installed:

```bash
php artisan chimoney:test
```

### Testing Functionality
1. Create a sample route in your `routes/web.php` file:

   ```php
   use Chimoney\LaravelSdk\Chimoney;

   Route::get('/test-chimoney', function () {
       $chimoney = new Chimoney();
       return $chimoney->getBalance();
   });
   ```

2. Visit `/test-chimoney` in your browser or use a tool like Postman to verify the response.

---

## Troubleshooting Tips

- **Invalid API Key:** Ensure the `CHIMONEY_API_KEY` in your `.env` file is correct.
- **Configuration Not Found:** Run `php artisan config:cache` to clear and refresh the configuration cache.
- **Network Errors:** Verify your internet connection and the `CHIMONEY_BASE_URL`.

For further assistance, refer to the [official documentation](https://chimoney.io/docs) or contact support.

---

Happy coding with Chimoney Laravel SDK!
