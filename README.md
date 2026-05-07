before_script:
  - echo "Начинаем настройку..."
  - yes | sdkmanager --licenses
  - echo "y" | sdkmanager --install "system-images;android-30;google_apis;x86_64"
  - echo "no" | avdmanager create avd -n ci_device -k "system-images;android-30;google_apis;x86_64" --force
