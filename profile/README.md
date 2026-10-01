<div align="center">

<img src="logo.svg" width="72" alt="Alror" />

# Alror

**Ship every change at the speed of AI, safely.**

Alror scores the risk of every pull request, rolls it out as a canary sized to that risk,
verifies it statistically against the baseline, and rolls it back automatically when it regresses.

</div>

### How it works

1. **Score**: every PR gets a 0–100 risk score from what it touches: critical services, sensitive paths, migrations, missing tests, AI-authored changes.
2. **Plan**: the score picks the rollout. Low risk goes 25% → 100%; high risk goes 1% → 5% → 25% → 50% → 100% with longer bakes.
3. **Verify**: at each step the canary is compared with the baseline (Mann-Whitney U, effect size and significance) on error rate and latency.
4. **Reverse**: a regression rolls the release back in seconds, with the reason written down.

### Get started

```bash
curl -fsSL https://raw.githubusercontent.com/manaskumar3003/alror-cli/main/scripts/install.sh | sh
alror init
alror risk
alror deploy -s checkout-api -i registry.example.com/checkout-api:v2
```

Add the risk check to your pull requests:

```yaml
- uses: manaskumar3003/alror-cli/actions/check@main
```

### Open source

| | |
| --- | --- |
| [**alror-cli**](https://github.com/manaskumar3003/alror-cli) | The `alror` CLI and runner, GitHub actions, and the Go and TypeScript SDKs (Apache-2.0) |

Works with Kubernetes (Argo Rollouts), Prometheus, Datadog, GitHub Actions and Slack.
