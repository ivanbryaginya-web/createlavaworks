name: Build
on: [push, workflow_dispatch]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with:
          java-version: '21'
          distribution: 'temurin'
      - uses: gradle/actions/setup-gradle@v4
      - name: Build
        run: chmod +x gradlew && ./gradlew build
      - name: Upload mod
        uses: actions/upload-artifact@v4
        with:
          name: mod
          path: build/libs/*.jar
