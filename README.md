# App Builders Gang — Homebrew Tap

Official Homebrew tap for apps by [App Builders Gang](https://github.com/App-Builders-Gang).

## Install any app from this tap

```bash
brew install --cask App-Builders-Gang/tap/<app-name>
```

Or, tap once and install by short name:

```bash
brew tap App-Builders-Gang/tap
brew install --cask <app-name>
```

## Available apps

| App | Install | Description |
|---|---|---|
| **[PrayerTimes](https://github.com/App-Builders-Gang/PrayerTimes)** | `brew install --cask App-Builders-Gang/tap/prayertimes` | Prayer times in your Mac's menu bar |

## Update installed apps

```bash
brew upgrade --cask <app-name>
```

## Uninstall

```bash
brew uninstall --cask <app-name>
```

## For maintainers — adding a new cask

1. Create `Casks/<app-name>.rb` with the standard Homebrew cask DSL:

   ```ruby
   cask "myapp" do
     version "1.0.0"
     sha256 "<sha256 of the .dmg>"

     url "https://github.com/App-Builders-Gang/MyApp/releases/download/v#{version}/MyApp-#{version}.dmg"
     name "MyApp"
     desc "One-line description"
     homepage "https://github.com/App-Builders-Gang/MyApp"

     livecheck do
       url :url
       strategy :github_latest
     end

     app "MyApp.app"

     uninstall quit: "dev.abd3lraouf.MyApp"

     zap trash: [
       "~/Library/Containers/dev.abd3lraouf.MyApp",
       "~/Library/Preferences/dev.abd3lraouf.MyApp.plist",
     ]
   end
   ```

2. Validate locally before pushing:

   ```bash
   brew audit --cask --new Casks/<app-name>.rb
   brew style Casks/<app-name>.rb
   ```

3. Each app's release workflow should bump its own cask here on tag push. See
   [PrayerTimes/.github/workflows/release.yml](https://github.com/App-Builders-Gang/PrayerTimes/blob/main/.github/workflows/release.yml)
   for a working example.

4. Add an entry to the **Available apps** table above.

## License

Each cask references the licensing of its upstream app. Cask files themselves
are licensed under the [BSD 2-Clause License](LICENSE), the same license used
by Homebrew core.
