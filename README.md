stages:
  - test

run_emulator:
  stage: test
  image: vvoyer/android-emulator:latest
  tags:
    - android
  script:
    - echo "Запускаем готовый эмулятор..."
    - /start-emulator.sh &
    - adb wait-for-device
    - echo "Эмулятор готов! Здесь будут твои первые тесты."
    - sleep 5
    - echo "Всё работает!"
