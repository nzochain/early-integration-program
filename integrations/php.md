# PHP integration

Call NZOChain API v1 with cURL in PHP. Educational example only — not an official SDK.

## Requirements

- PHP 8.1+ with `curl` extension
- Environment variable `NZOCHAIN_API_KEY`

## Environment

```bash
export NZOCHAIN_API_KEY="YOUR_NZOCHAIN_API_KEY"
```

## Complete example

```php
<?php
declare(strict_types=1);

$apiKey = getenv('NZOCHAIN_API_KEY');
if ($apiKey === false || $apiKey === '') {
    fwrite(STDERR, "Missing NZOCHAIN_API_KEY\n");
    exit(1);
}

$payload = json_encode([
    'wallet' => '0xYOUR_WALLET_ADDRESS',
    'network' => 'ethereum',
], JSON_THROW_ON_ERROR);

$ch = curl_init('https://api.nzochain.com/api/v1/wallets/risk?lang=en');
curl_setopt_array($ch, [
    CURLOPT_POST => true,
    CURLOPT_HTTPHEADER => [
        'Content-Type: application/json',
        'X-API-Key: ' . $apiKey,
    ],
    CURLOPT_POSTFIELDS => $payload,
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_TIMEOUT => 60,
]);

$raw = curl_exec($ch);
$status = (int) curl_getinfo($ch, CURLINFO_HTTP_CODE);
$error = curl_error($ch);
curl_close($ch);

if ($raw === false) {
    fwrite(STDERR, "cURL error: {$error}\n");
    exit(1);
}

$body = json_decode($raw, true) ?? [];

if ($status === 401) {
    fwrite(STDERR, "Unauthorized: check API key\n");
    exit(1);
}
if ($status === 403) {
    $code = $body['code'] ?? 'FORBIDDEN';
    fwrite(STDERR, "Forbidden: {$code}\n");
    exit(1);
}
if ($status === 429) {
    $code = $body['code'] ?? 'RATE_LIMIT';
    $reset = $body['resetAt'] ?? 'n/a';
    fwrite(STDERR, "Quota/rate limited: {$code} resetAt={$reset}\n");
    exit(1);
}
if ($status >= 400 || (($body['success'] ?? null) === false)) {
    fwrite(STDERR, "Request failed HTTP {$status}\n");
    exit(1);
}

$data = $body['data'] ?? [];
echo ($data['riskScore'] ?? '') . ' ' .
     ($data['riskLevel'] ?? '') . ' ' .
     ($data['decision'] ?? '') . PHP_EOL;
```

## Expected response shape

Published v1 envelope with `success` and `data` containing `riskScore`, `riskLevel`, `decision`, optional `reasons` / `meta`.

## How to run

```bash
export NZOCHAIN_API_KEY="YOUR_NZOCHAIN_API_KEY"
php wallet_risk.php
```

## Quota note

Each call consumes monthly B2B API quota. Do not embed keys in public repositories.

Static validation only — no live API calls were made while authoring this guide.
