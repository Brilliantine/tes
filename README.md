stages:
  - test

run_emulator:
  stage: test
  image: androidsdk/android-30:latest  # <-- Новый образ
  tags:
    - android
  before_script:
    - echo "Начинаем настройку..."
    - yes | sdkmanager --licenses
    # В этом образе SDK уже включает все нужные инструменты, поэтому команды чуть короче
    - echo "y" | sdkmanager --install "system-images;android-30;default;x86_64"
    - echo "no" | avdmanager create avd -n ci_device -k "system-images;android-30;default;x86_64" --force
  script:
    - echo "Запускаем эмулятор..."
    - $ANDROID_HOME/emulator/emulator -avd ci_device -no-window -no-audio -gpu swiftshader_indirect &
    - adb wait-for-device
    - echo "Эмулятор готов! Здесь будут твои первые тесты."
    - sleep 10
    - echo "Всё работает!"
