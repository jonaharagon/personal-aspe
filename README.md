# Ariadne Signature Profile Host

Hosts [Ariadne Signature Profiles](https://docs.keyoxide.org/getting-started/creating-profile/) on `jda.mn`. For example, the file [`.well-known/aspe/id/MQQHXQXAC2ZMPKEOJAJ766QX34`](.well-known/aspe/id/MQQHXQXAC2ZMPKEOJAJ766QX34) makes a profile available at [https://keyoxide.org/aspe:jda.mn:MQQHXQXAC2ZMPKEOJAJ766QX34](https://keyoxide.org/aspe:jda.mn:MQQHXQXAC2ZMPKEOJAJ766QX34).

## Generating a profile

Follow the instructions [here](https://docs.keyoxide.org/getting-started/creating-profile/), but instead of clicking "Save and Upload Profile" in the web tool, click "Export Profile" and it will give you the necessary data to upload to this repository.

Your ASPE will then be available via `aspe:jda.mn:[FINGERPRINT]`

## How this works

`Caddyfile`:

```caddyfile
jda.mn {
        rewrite /.well-known/aspe/* /jonaharagon/personal-aspe/main/{uri}
        @aspe {
                path /jonaharagon/personal-aspe/main/*
        }
        handle @aspe {
                reverse_proxy https://raw.githubusercontent.com {
                        header_up Host raw.githubusercontent.com
                        header_down Content-Type "application/asp+jwt; charset=UTF-8"
                }
        }
}
```
