# tes
tes
Step 5:
version: '3.8'

services:
  gitlab:
    image: gitlab/gitlab-ce:latest
    container_name: gitlab
    restart: always
    hostname: 'gitlab.local'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://gitlab.local'
    ports:
      - "80:80"
      - "2222:22"
    volumes:
      - './gitlab/config:/etc/gitlab'
      - './gitlab/logs:/var/log/gitlab'
      - './gitlab/data:/var/opt/gitlab'
    shm_size: '256m'

  gitlab-runner:
    image: gitlab/gitlab-runner:latest
    container_name: gitlab-runner
    restart: always
    depends_on:
      - gitlab
    volumes:
      - '/var/run/docker.sock:/var/run/docker.sock'
      - '/dev/kvm:/dev/kvm'                 # <-- магия для эмулятора
      - './gitlab-runner/config:/etc/gitlab-runner'

      Step 7: .gitlab-ci.yml
      stages:
  - test

run_emulator:
  stage: test
  image: reactnativecommunity/react-native-android:latest
  tags:
    - android
  before_script:
    - echo "Начинаем настройку..."
    - echo "y" | sdkmanager --install "system-images;android-29;default;x86"
    - echo "no" | avdmanager create avd -n ci_device -k "system-images;android-29;default;x86" --force
  script:
    - echo "Запускаем эмулятор..."
    - $ANDROID_HOME/emulator/emulator -avd ci_device -no-window -no-audio -gpu swiftshader_indirect &
    - adb wait-for-device
    - echo "Эмулятор готов! Здесь будут твои первые тесты."
    - sleep 10
    - echo "Всё работает!"
