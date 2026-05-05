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


    Running with gitlab-runner 18.11.2 (68229485)
  on docker-kvm-runner y1_rnE34d, system ID: r_smsdvX8edeqQ
Preparing the "docker" executor 00:08
Using Docker executor with image reactnativecommunity/react-native-android:latest ...
Using effective pull policy of [always] for container reactnativecommunity/react-native-android:latest
Pulling docker image reactnativecommunity/react-native-android:latest ...
Using docker image sha256:88d93a9282e0f54f84cec7b979da6c5e3f20d87f5be246b75c231838be852fec for reactnativecommunity/react-native-android:latest with digest reactnativecommunity/react-native-android@sha256:88d93a9282e0f54f84cec7b979da6c5e3f20d87f5be246b75c231838be852fec ...
Preparing environment 00:00
Using effective pull policy of [always] for container sha256:39e9155b72aff010f55a8bbfdb94fedeb0824de18612795d8b901ac4b42d99f5
Running on runner-y1rne34d-project-1-concurrent-0 via 217e5cc51af0...
Getting source from Git repository 00:01
Gitaly correlation ID: 01KQVV36Q1STVVTRPH1547TBEC
Fetching changes with git depth set to 20...
Reinitialized existing Git repository in /builds/root/rzd/.git/
Created fresh repository.
fatal: unable to access 'http://gitlab.local/root/rzd.git/': Could not resolve host: gitlab.local
Cleaning up project directory and file based variables 00:00
ERROR: Job failed: exit code 1
