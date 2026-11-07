# Go integration

Call NZOChain API v1 with `net/http`. Educational example only — not an official SDK.

## Requirements

- Go 1.21+
- Environment variable `NZOCHAIN_API_KEY`

## Environment

```bash
export NZOCHAIN_API_KEY="YOUR_NZOCHAIN_API_KEY"
```

## Complete example

```go
package main

import (
	"bytes"
	"encoding/json"
	"fmt"
	"io"
	"net/http"
	"os"
	"time"
)

type riskRequest struct {
	Wallet  string `json:"wallet"`
	Network string `json:"network"`
}

type riskResponse struct {
	Success bool `json:"success"`
	Data    struct {
		RiskScore int      `json:"riskScore"`
		RiskLevel string   `json:"riskLevel"`
		Decision  string   `json:"decision"`
		Reasons   []string `json:"reasons"`
	} `json:"data"`
	Code    string `json:"code"`
	ResetAt string `json:"resetAt"`
}

func main() {
	apiKey := os.Getenv("NZOCHAIN_API_KEY")
	if apiKey == "" {
		fmt.Fprintln(os.Stderr, "Missing NZOCHAIN_API_KEY")
		os.Exit(1)
	}

	payload, err := json.Marshal(riskRequest{
		Wallet:  "0xYOUR_WALLET_ADDRESS",
		Network: "ethereum",
	})
	if err != nil {
		panic(err)
	}

	req, err := http.NewRequest(
		http.MethodPost,
		"https://api.nzochain.com/api/v1/wallets/risk?lang=en",
		bytes.NewReader(payload),
	)
	if err != nil {
		panic(err)
	}
	req.Header.Set("Content-Type", "application/json")
	req.Header.Set("X-API-Key", apiKey)

	client := &http.Client{Timeout: 60 * time.Second}
	res, err := client.Do(req)
	if err != nil {
		fmt.Fprintln(os.Stderr, err)
		os.Exit(1)
	}
	defer res.Body.Close()

	raw, err := io.ReadAll(res.Body)
	if err != nil {
		panic(err)
	}

	var body riskResponse
	_ = json.Unmarshal(raw, &body)

	switch {
	case res.StatusCode == http.StatusUnauthorized:
		fmt.Fprintln(os.Stderr, "Unauthorized: check API key")
		os.Exit(1)
	case res.StatusCode == http.StatusForbidden:
		fmt.Fprintf(os.Stderr, "Forbidden: %s\n", body.Code)
		os.Exit(1)
	case res.StatusCode == http.StatusTooManyRequests:
		fmt.Fprintf(os.Stderr, "Quota/rate limited: %s resetAt=%s\n", body.Code, body.ResetAt)
		os.Exit(1)
	case res.StatusCode >= 400 || !body.Success:
		fmt.Fprintf(os.Stderr, "Request failed HTTP %d\n", res.StatusCode)
		os.Exit(1)
	}

	fmt.Println(body.Data.RiskScore, body.Data.RiskLevel, body.Data.Decision)
}
```

## How to run

```bash
export NZOCHAIN_API_KEY="YOUR_NZOCHAIN_API_KEY"
go run .
```

## Quota note

Successful calls consume monthly B2B API quota. Handle `429` distinctly from auth failures.

Static validation only — no live API calls were made while authoring this guide.
