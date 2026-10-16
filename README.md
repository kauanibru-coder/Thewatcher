
name: Build The Watcher

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '21'

      - name: Extract project
        run: |
          unzip -o TheWatcher-Forge-1.21.1-cloud-build.zip
          cd TheWatcher-Forge-1.21.1
          echo "PROJECT_DIR=$PWD" >> "$GITHUB_ENV"

      - name: Build mod
        run: |
          cd "$PROJECT_DIR"
          gradle build --no-daemon

      - uses: actions/upload-artifact@v4
        with:
          name: TheWatcher-jar
          path: TheWatcher-Forge-1.21.1/build/libs/*.jar
          
