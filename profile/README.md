<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="wordmark-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="wordmark-light.svg">
    <img src="wordmark-light.svg" alt="Alror" width="240">
  </picture>
</p>

<p align="center">
  <b>The release gate for the age of AI-written code.</b><br/>
  Alror scores every change for risk, rolls it out as a canary sized to that risk,<br/>
  verifies each step against live metrics, and rolls back on its own when a release hurts users.
</p>

<p align="center">
  <a href="https://alror.com">alror.com</a> ·
  <a href="https://github.com/alrors/alror">GitHub</a> ·
  <a href="https://github.com/alrors/alror/tree/main/docker">Self-host</a> ·
  <a href="https://github.com/alrors/alror/discussions">Discussions</a>
</p>

<p align="center">
  <img src="console.webp" alt="The Alror console: live rollouts, services and usage" width="100%" />
</p>

### How it works

1. **Score:** every pull request gets a 0–100 risk score from what it touches: critical services, sensitive paths, migrations, missing tests, agent-authored commits, recent rollbacks.
2. **Plan:** the score picks the rollout. Low risk goes 25% → 100%; high risk goes 1% → 5% → 25% → 50% → 100% with longer bakes.
3. **Verify:** each stage compares canary and baseline (Mann-Whitney U, effect size and significance) on error rate and latency.
4. **Reverse:** a regression rolls the release back in seconds, with the reason written down, and CI goes red.

### Get started

```bash
go install github.com/alrors/alror/cmd/alror@latest
alror init && alror risk
alror deploy -s checkout-api -i registry.example.com/checkout-api:v2
```

Add the risk check to your pull requests:

```yaml
- uses: alrors/alror/actions/check@main
```

### Open source

[**alrors/alror**](https://github.com/alrors/alror) is the whole product under Apache-2.0: the CLI and runner, the workspace console and API, the Go and TypeScript SDKs, GitHub Actions and a one-command self-hosting setup.

Works with Kubernetes (Argo Rollouts), Amazon ECS, Prometheus, Datadog, GitHub Actions and Slack.
