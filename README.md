before_script:
  - echo "Начинаем настройку..."
  - set +e                     # Временно разрешаем некритичные ошибки
  - yes | sdkmanager --licenses
  - set -e                     # Снова включаем строгую проверку ошибок
  - echo "y" | sdkmanager --install "system-images;android-30;google_apis;x86_64"
  - echo "no" | avdmanager create avd -n ci_device -k "system-images;android-30;google_apis;x86_64" --force
