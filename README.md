# bhavani

name: lint
on:
  push:
    branches: [main]
    branches:
      - main
  pull_request:
    branches: [main]
    branches:
      - main
jobs:
  build:
    runs-on: ubuntu-latest
    container:
      image: google/dart:latest
    steps:
      - uses: actions/checkout@v2
      - run: dartfmt --dry-run --set-exit-if-changed lib/*.dart lib/models/*.dart lib/scaffolds/*.dart lib/screens/*.dart lib/utils/*.dart lib/widgets/*.dart
      - uses: subosito/flutter-action@v1
        with:
          channel: stable
      - run: flutter analyze
      - run: flutter format --dry-run --set-exit-if-changed lib/**/*.dart
