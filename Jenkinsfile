#ci.gocd.yaml
pipelines:
  dcsp2-backend-pip:
    group: dcsp2
    label_template: "d${COUNT}-g${src[:7]}"
    materials:
      src:
        git: git@gitlab.com:digitalshell.com.cn/dcsp2/dcsp2-backend.git
        branch: 'master'
        shallow_clone: true
    stages:
      - test: # name of stage
          jobs:
            unit_test: # name of the job
              artifacts:
                - test:
                    source: build/reports
                    destination: test
              tabs:
                coverage: test/reports/jacoco/codeCoverageReport/html/index.html
                test: test/reports/tests/index.html
              tasks:
                - exec:
                    command: scripts/unit_test
      - publish_image:
          jobs:
            publish_image:
              tasks:
                - exec:
                    command: scripts/publish_image
      - deploy-dev:
          jobs:
            deploy-dev:
              tasks:
                - exec:
                    command: scripts/deploy
                    arguments:
                      - "dev"
      - deploy-qa:
          approval: manual
          jobs:
            deploy-qa:
              tasks:
                - exec:
                    command: scripts/deploy
                    arguments:
                      - "qa"
  dcsp2-backend-release:
    group: dcsp2
    label_template: "r${COUNT}-g${src[:7]}"
    materials:
      src:
        git: git@gitlab.com:digitalshell.com.cn/dcsp2/dcsp2-backend.git
        branch: 'release'
    stages:
      - test: # name of stage
          jobs:
            unit_test: # name of the job
              artifacts:
                - test:
                    source: build/reports
                    destination: test
              tabs:
                coverage: test/reports/jacoco/codeCoverageReport/html/index.html
                test: test/reports/tests/index.html
              tasks:
                - exec:
                    command: scripts/unit_test
      - publish_image:
          jobs:
            publish_image:
              tasks:
                - exec:
                    command: scripts/publish_image
      - deploy-uat:
          approval: manual
          jobs:
            deploy-uat:
              tasks:
                - exec:
                    command: scripts/deploy
                    arguments:
                      - "uat"
      - deploy-prod:
          approval: manual
          jobs:
            deploy-prod:
              tasks:
                - exec:
                    command: scripts/deploy
                    arguments:
                      - "prod"
