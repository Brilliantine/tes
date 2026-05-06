version: '3.8'

services:
  gitlab:
    image: gitlab/gitlab-ce:latest
    container_name: gitlab
    restart: always
    hostname: 'gitlab'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://172.20.0.10'
    ports:
      - "80:80"
      - "2222:22"
    volumes:
      - './gitlab/config:/etc/gitlab'
      - './gitlab/logs:/var/log/gitlab'
      - './gitlab/data:/var/opt/gitlab'
    networks:
      ci_network:
        ipv4_address: 172.20.0.10

  gitlab-runner:
    image: gitlab/gitlab-runner:latest
    container_name: gitlab-runner
    restart: always
    depends_on:
      - gitlab
    volumes:
      - '/var/run/docker.sock:/var/run/docker.sock'
      - '/dev/kvm:/dev/kvm'
      - './gitlab-runner/config:/etc/gitlab-runner'
    networks:
      ci_network:

networks:
  ci_network:
    driver: bridge
    ipam:
      config:
        - subnet: 172.20.0.0/24
