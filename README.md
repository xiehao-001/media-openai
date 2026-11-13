# Media (OpenAI-Compatible)

`@eduwork/dsh-media-openai` · v0.1.0-dev · MulanPSL-2.0 AND MIT

Registers OpenAI-compatible image and text-to-speech services with `@eduwork/dsh-artifact-services`, so chat and Studio share the same media tools, previews and permission boundary. The module contributes no school or vendor defaults: addresses, models, sizes, voices and credentials all come from deployment or user configuration.

It exists so a deployment can point DSH at any compatible endpoint, including an institution's own gateway, without shipping a provider-specific plugin.

## Highlights

- Image providers declared with `local: false`, required `nativeSizes`, a `defaultSize`, `crop` and `pad` fit modes and custom request sizes.
- Optional image editing (`images.edit: true`) that accepts up to `16` source images.
- Speech providers with a voice catalog (`id`, `title`, `language`), a default voice and WAV output for the shared timeline and preview contract.
- Strict provider validation: unique lowercase ids (the names `system` and `local` are reserved), `protocol: 'openai-compatible'`, an HTTPS base URL (HTTP only for loopback hosts) with no embedded credentials, query or hash.
- Availability follows `credentials.describe(credentialRef).configured` (default reference `EDUWORK_API_KEY`), or an authorized OIDC profile when `oidcProfileId` is set, so unusable providers are not offered.
- Requests run through the governed tools `image_generate`, `image_edit` and `speech_synthesize`, keeping approvals, cancellation and workspace permissions in force.
- Provider availability is refreshed when credentials change (`credentials/updated`, `credentials/reference-updated`).

## Install

Install this directory as a local DSH plugin bundle. From a shell:

```bash
dsh plugin --profile web add /absolute/path/to/media-openai
```

Or add the directory through the **Plugins** panel in DSH (local bundle). Restart the DSH app after installation; plugins are activated from the bundle patch (`cordis.patch.yml`).

## Configuration

No configuration keys: the bundle patch inserts the plugin with defaults.

In practice the plugin is configured through its `providers` array: each entry sets `id`, `title`, `protocol`, `baseURL`, `credentialRef` (default `EDUWORK_API_KEY`) or `oidcProfileId`, and the optional `images` and `speech` blocks (`model`, `nativeSizes`, `defaultSize`, `responseFormat`, `edit`, `editMaxImages`, `voices`, `defaultVoice`). The normalizer requires `providers` to be an array, so the shipped empty config needs at least `providers: []` before the module can load.

## Requirements

- DeepSeek Harness >=0.2.1 <0.3.0
- Peer packages: @eduwork/dsh-artifact-services, @deepseek-ai/cordis

## Notes and limits

- Adds no tools or skills of its own: the tools, previews and skills belong to Artifact Services, and this package only registers providers behind them.
- `credentialRef` cannot point at a login session: values starting with `DSH_OIDC_` are rejected, and `oidcProfileId` is the supported route.
- Image sizes must be 64 to 4096 pixels per side, and enabling images requires a non-empty `nativeSizes` list.
- Development-stage build: the version is `0.1.0-dev`.

## 中文文档

[README.zh-CN.md](./README.zh-CN.md)

## License

MulanPSL-2.0 AND MIT — see [LICENSE](./LICENSE) and, where present, [LICENSE-MIT](./LICENSE-MIT). Extracted from the ECNU EduWork distribution (https://github.com/ECNU/EduWork); upstream copyright and license notices are preserved.
