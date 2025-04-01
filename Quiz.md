# GitLab CI/CD Quiz (100 Questions) - Bulleted Options Formatting

## 🔹 Section 1: Pipelines & Stages

1.  What is the default behavior of stages in GitLab CI/CD?
    * A) Jobs in the same stage run sequentially.
    * **B) Jobs in the same stage run in parallel.**
    * C) Stages must be defined in alphabetical order.
    * D) Jobs can only belong to one stage.

2.  Which keyword defines the order of stage execution in a pipeline?
    * A) `order`
    * **B) `stages`**
    * C) `sequence`
    * D) `phase`

3.  What happens if a job in the `test` stage fails?
    * A) The pipeline continues to the `deploy` stage.
    * **B) The pipeline stops, and jobs in later stages are not executed.**
    * C) GitLab automatically retries the failed job.
    * D) The pipeline is marked as "warning" but continues.

4.  How can you force a job to run even if previous stages fail?
    * A) `allow_failure: true`
    * **B) `when: always`**
    * C) `ignore_failure: true`
    * D) `continue_on_failure: yes`

5.  Which file defines the CI/CD pipeline in GitLab?
    * A) `gitlab-pipeline.yml`
    * **B) `.gitlab-ci.yml`**
    * C) `ci-config.yaml`
    * D) `pipeline.gitlab`

## 🔹 Section 2: Jobs & Scripts

6.  What is the correct syntax for defining a job in `.gitlab-ci.yml`?
    * A)
        ```yaml
        job-name:
          - script: echo "Hello"
        ```
    * **B)**
        ```yaml
        job-name:
          script:
            - echo "Hello"
        ```
    * C)
        ```yaml
        job:
          name: job-name
          commands: echo "Hello"
        ```
    * D)
        ```yaml
        task: job-name
          run: echo "Hello"
        ```

7.  How do you prevent a job from running in a pipeline?
    * A) `enabled: false`
    * B) `active: no`
    * **C) `rules: - when: never`**
    * D) `skip: true`

8.  Which keyword allows a job to run out of stage order (based on job dependencies)?
    * A) `depends_on`
    * **B) `needs`**
    * C) `requires`
    * D) `depends`

9.  What is the purpose of the `before_script` keyword?
    * A) Runs before all jobs in the pipeline.
    * **B) Runs before each job where it’s defined (before the main `script`).**
    * C) Runs only if the job succeeds.
    * D) Runs after the main `script`.

10. How do you run a job only for Git tags (using modern syntax)?
    * **A)**
        ```yaml
        rules:
          - if: '$CI_COMMIT_TAG'
        ```
    * B)
        ```yaml
        only:
          - tags
        ```
    * C)
        ```yaml
        when: tag
        ```
    * D)
        ```yaml
        trigger:
          - tags
        ```

## 🔹 Section 3: Variables & Environments

11. Where can you define CI/CD variables? (Select all that apply)
    * A) `.gitlab-ci.yml`
    * B) Project Settings > CI/CD > Variables
    * C) Group CI/CD Variables
    * *(Also Instance CI/CD Variables)*
    * **D) All of the above (A, B, C are common locations)**

12. How do you mask a variable in GitLab CI/CD so it doesn't appear in job logs?
    * A) Add `masked: true` in `.gitlab-ci.yml`.
    * **B) Enable "Mask variable" when creating it in the UI (Project/Group/Instance settings).**
    * C) Use `export VAR=value` in scripts.
    * D) GitLab automatically masks all variables.

13. What is the correct way to use an environment variable in a job script?
    * **A) `$VARIABLE_NAME` or `${VARIABLE_NAME}`**
    * B) `%VARIABLE_NAME%`
    * C) `{{VARIABLE_NAME}}`
    * D) `env.VARIABLE_NAME`

14. How do you define a dynamic environment name using a CI/CD variable?
    * **A)**
        ```yaml
        environment:
          name: deploy/$CI_COMMIT_REF_NAME
        ```
    * B)
        ```yaml
        env:
          name: $BRANCH
        ```
    * C)
        ```yaml
        deploy_to:
          environment: dynamic
        ```
    * D)
        ```yaml
        environment:
          dynamic: true
        ```

15. What is the purpose of `interruptible: true` in a job definition?
    * A) Allows manual job cancellation.
    * **B) Automatically cancels the job if a newer pipeline for the same ref (branch/tag) starts running.**
    * C) Restarts the job on failure.
    * D) Pauses the job for approval.

## 🔹 Section 4: Artifacts & Caching

16. What is the difference between artifacts and cache?
    * **A) Artifacts pass files between jobs in the *same* pipeline; cache speeds up *future runs* of the *same* job.**
    * B) Cache is stored forever; artifacts expire. (Both can expire or be kept)
    * C) Artifacts are encrypted; cache is not. (Neither is encrypted by default)
    * D) They are the same.

17. How do you make an artifact expire after 1 week?
    * **A)**
        ```yaml
        artifacts:
          expire_in: 7 days
        ```
    * B)
        ```yaml
        cache:
          ttl: 604800
        ```
    * C)
        ```yaml
        expire_artifacts: 1w
        ```
    * D) Artifacts cannot expire.

18. Which job can access artifacts from a previous job by default (without `needs`)?
    * A) Only jobs in the same stage.
    * **B) Only jobs in later stages.**
    * C) Any job in the pipeline.
    * D) Only jobs with `needs:`.

19. How do you cache `node_modules` between pipeline runs for the same branch/job?
    * **A)**
        ```yaml
        cache:
          key: $CI_COMMIT_REF_SLUG # Or a more specific key
          paths:
            - node_modules/
        ```
    * B)
        ```yaml
        artifacts:
          paths:
            - node_modules/
        ```
    * C)
        ```yaml
        save: node_modules
        ```
    * D)
        ```yaml
        store:
          - dependencies
        ```

20. What happens if two jobs running in parallel modify the same distributed cache key?
    * A) GitLab merges changes automatically.
    * **B) The last job to finish uploading overwrites the cache for that key.**
    * C) The cache becomes read-only.
    * D) GitLab throws an error.

## 🔹 Section 5: Advanced Features

21. How do you trigger a pipeline in another project (multi-project pipeline)?
    * **A)**
        ```yaml
        trigger:
          project: 'other/project'
          branch: 'main' # Optional
        ```
    * B)
        ```yaml
        trigger_pipeline:
          script:
            - curl -X POST -F "token=$CI_JOB_TOKEN" "[https://gitlab.com/api/v4/projects/123/trigger/pipeline](https://gitlab.com/api/v4/projects/123/trigger/pipeline)" # API method, not direct trigger keyword
        ```
    * C)
        ```yaml
        include:
          - project: 'other/project' # Includes config, doesn't trigger a run there
        ```
    * D) GitLab does not support this.

22. What is the purpose of `extends` in `.gitlab-ci.yml`?
    * **A) Reuses job configurations (inheritance).**
    * B) Increases job timeout.
    * C) Runs jobs in parallel.
    * D) Imports external scripts.

23. How do you run a job only if a specific file changes?
    * **A)**
        ```yaml
        rules:
          - changes:
              - path/to/file.txt
              - another/path/**/*
        ```
    * B)
        ```yaml
        only:
          changes: path/to/file
        ```
    * C)
        ```yaml
        when:
          file_modified: path/to/file
        ```
    * D)
        ```yaml
        condition:
          - file_changed
        ```

24. What does `needs: []` (an empty needs array) mean for a job?
    * **A) The job has no explicit dependencies on specific previous jobs and can start as soon as its stage is ready (often running sooner than jobs without `needs`).**
    * B) The job is optional.
    * C) The job waits for all jobs in all previous stages. (This is the default behavior *without* `needs`)
    * D) The job is skipped.

25. How do you manually trigger a pipeline run?
    * A) Push a new commit. (This is an automatic trigger)
    * **B) Click "Run pipeline" in the GitLab UI (CI/CD > Pipelines).**
    * C) Use `gitlab-ci trigger`. (Not a standard command)
    * D) Schedule it in cron. (This is a scheduled trigger)

## 🔹 Section 6: Security & Permissions

26. How do you protect a CI/CD variable from being visible in job logs?
    * A) Use `secret: true` in `.gitlab-ci.yml`.
    * **B) Enable "Mask variable" in the CI/CD settings (UI).**
    * C) Prefix the variable with `_SECRET_`.
    * D) GitLab automatically masks all variables.

27. Which role (or higher) can typically configure CI/CD pipelines and settings in a project?
    * **A) Developer**
    * B) Reporter
    * C) Guest
    * D) Only project Owners. (Maintainers can too)

28. How do you prevent a job from running on pipelines triggered from forks?
    * **A)**
        ```yaml
        rules:
          - if: '$CI_PROJECT_NAMESPACE == "my-group/my-project"' # Example rule checking the source project
        # Or more commonly:
        # rules:
        #  - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH # Run only on default branch
        ```
    * B)
        ```yaml
        only:
          - main # Restricts to branch, doesn't explicitly block forks
        ```
    * C) `allow_forks: false` (Not a valid keyword)
    * D) GitLab blocks forks by default. (It allows them by default)

29. What is the purpose of the predefined `CI_JOB_TOKEN`?
    * **A) Authenticates API calls within the CI/CD pipeline (e.g., to GitLab Container Registry, Packages, other project APIs if permitted).**
    * B) Encrypts artifacts.
    * C) Masks variables.
    * D) Triggers manual jobs.

30. How do you restrict a job to run only on protected branches?
    * **A)**
        ```yaml
        rules:
          - if: '$CI_COMMIT_REF_PROTECTED == "true"'
        ```
    * B)
        ```yaml
        only:
          - protected # Deprecated syntax
        ```
    * C) `protected: true` (Not a valid keyword for this)
    * D) Use branch permissions in settings. (Settings protect branches, this rule *runs jobs* based on that protection)

## 🔹 Section 7: Debugging & Troubleshooting

31. How do you primarily debug a failing job?
    * **A) Check the job logs in GitLab UI.**
    * B) Rerun the pipeline with `debug: true`. (Not a standard keyword, use `CI_DEBUG_TRACE=true`)
    * C) Use `echo $CI_DEBUG` in scripts. (Variable doesn't exist by default)
    * D) Download the runner’s console output. (Logs in UI are usually sufficient)

32. What does the `retry` keyword do?
    * **A) Automatically reruns a failed job (up to 2 times by default if specified without a count).**
    * B) Pauses the job for manual review.
    * C) Skips the job on failure.
    * D) Restarts the runner.

33. How do you access artifacts from a failed job (assuming they were configured to be saved on failure)?
    * **A) Download them from the job’s page ("Keep" artifacts or browse job artifacts).**
    * B) They are deleted if the job fails (Only if `when: on_success` (default) and `expire_in` is met).
    * C) Use `needs: [failed_job]`. (`needs` defines dependency, doesn't guarantee artifact access on failure)
    * D) Only available via API. (Also available in UI)

34. What is the default timeout for a job in GitLab CI/CD?
    * A) 30 minutes.
    * **B) 1 hour (60 minutes).**
    * C) 24 hours.
    * D) No timeout.

35. How do you simulate running a job locally using the GitLab Runner executable?
    * **A) Use `gitlab-runner exec <executor> <job_name>`**
    * B) Run `gitlab-ci-local`. (Third-party tool, not official GitLab Runner)
    * C) Use `docker-compose ci`. (Not a standard GitLab method)
    * D) GitLab does not support local testing.

## 🔹 Section 8: Scheduled Pipelines

36. How do you schedule a pipeline to run daily?
    * **A) In GitLab UI: CI/CD > Schedules > New schedule (using Cron syntax like `0 0 * * *`).**
    * B) Add `cron: "0 0 * * *"` to `.gitlab-ci.yml`. (Not a valid keyword)
    * C) Use `rules: - when: scheduled`. (Doesn't define the schedule itself)
    * D) Configure a webhook. (Webhooks react to events, not schedules)

37. Which keyword/condition ensures a job runs *only* in scheduled pipelines?
    * **A)**
        ```yaml
        rules:
          - if: '$CI_PIPELINE_SOURCE == "schedule"'
            when: always # Optional, default is on_success
          - when: never # Prevent running in other cases
        ```
    * B)
        ```yaml
        only:
          - schedules # Older syntax
        ```
    * C) `when: scheduled` (Not a valid value for `when`)
    * D) `trigger: schedule` (Not a valid keyword)

38. Can you pass variables to scheduled pipelines?
    * A) No, scheduled pipelines use fixed variables.
    * **B) Yes, via the schedule’s "Variables" section in the GitLab UI.**
    * C) Only if defined in `.gitlab-ci.yml`.
    * D) Only for manual jobs.

39. How do you trigger a pipeline on a specific branch via a schedule?
    * **A) Set the branch/tag/ref in the schedule’s "Target branch or tag" field in the GitLab UI.**
    * B) Use `only: - schedules` in the job. (Doesn't specify the branch)
    * C) Add `branch: main` to the schedule config. (Not a valid field)
    * D) GitLab schedules always use the default branch. (They use the specified target ref)

40. What happens if a scheduled pipeline fails?
    * A) GitLab retries it automatically. (Only if `retry` is configured)
    * **B) It remains marked as failed, and notifications may be sent (based on configuration).**
    * C) The schedule is disabled automatically. (It is not)
    * D) It triggers a rollback. (Only if configured to do so)

## 🔹 Section 9: Docker & Kubernetes Integration

41. How do you specify that a job should run inside a Docker container?
    * **A)**
        ```yaml
        job:
          image: alpine:latest
          script: echo "Hello from Alpine"
        ```
    * B)
        ```yaml
        job:
          docker: alpine
          commands: echo "Hello"
        ```
    * C)
        ```yaml
        container:
          name: alpine
        ```
    * D) GitLab only supports shell runners.

42. What is the purpose of the `services` keyword in `.gitlab-ci.yml`?
    * **A) Spin up additional linked containers alongside the job container (e.g., databases, browsers for testing).**
    * B) Define microservices for deployment.
    * C) Configure Kubernetes pods directly.
    * D) Enable Docker Swarm mode.

43. How do you typically deploy an application to Kubernetes using GitLab CI/CD?
    * **A) Use `kubectl` (or `helm`, etc.) commands within a job's `script`, often using a pre-configured Kubernetes Agent connection or `kubeconfig`.**
    * B) Add `deploy: kubernetes` to `.gitlab-ci.yml`. (Not a standard keyword)
    * C) GitLab Auto DevOps only. (Auto DevOps is one way, but manual config is common)
    * D) Requires a custom runner. (Standard Docker or Kubernetes runners can do this)

44. Which file *primarily* defines the Kubernetes deployment details when using GitLab Auto DevOps?
    * A) `kube.yml`
    * **B) The standard Helm chart used by Auto DevOps (customizable via `.gitlab/auto-deploy-values.yaml`).**
    * C) `docker-compose.yml`
    * D) `gitlab-k8s.yaml`

45. How do you securely authenticate with a private Docker registry (like Docker Hub or GitLab's own registry) in a job?
    * **A) Define a CI/CD variable `DOCKER_AUTH_CONFIG` containing the necessary credentials (often configured via Project/Group settings).**
    * B)
        ```yaml
        before_script:
          - docker login --username $DOCKER_USER --password $DOCKER_PASSWORD # Less secure if creds are exposed
        ```
    * C) Use `CI_DOCKER_KEY` in secrets. (Not a standard predefined variable)
    * D) GitLab handles it automatically for all registries. (Only for the integrated GitLab registry using `CI_JOB_TOKEN`)

## 🔹 Section 10: GitLab Runners

46. What is a shared runner in GitLab?
    * **A) A runner available to multiple projects (often all projects if enabled) within a GitLab instance or group.**
    * B) A runner used only for scheduled jobs.
    * C) A runner with elevated permissions.
    * D) A runner that auto-scales. (Shared runners *can* be configured to auto-scale, but it's not inherent)

47. How do you ensure a job runs only on a specific type of runner (e.g., one capable of running Docker)?
    * **A)**
        ```yaml
        job:
          tags:
            - docker # Matches a tag defined on the runner
        ```
    * B) `runner: docker` (Not a valid keyword)
    * C)
        ```yaml
        only:
          - runners:docker # Not valid syntax
        ```
    * D) Use runner permissions. (Permissions control access, tags control job assignment)

48. What is the main purpose of the `config.toml` file for a GitLab Runner?
    * **A) Configure the runner's behavior, such as executor type, concurrency limits, cache settings, volume mounts, etc.**
    * B) Define CI/CD variables for jobs. (Variables are defined in GitLab UI or `.gitlab-ci.yml`)
    * C) Store job artifacts. (Artifacts are usually uploaded to GitLab instance storage)
    * D) Manage Docker images used by jobs. (Images are specified in `.gitlab-ci.yml`)

49. How do you register a new GitLab Runner?
    * **A) Run the `gitlab-runner register` command interactively or non-interactively.**
    * B) `gitlab-ci runner add` (Not a valid command)
    * C) Through the GitLab UI only. (UI provides registration token/URL, but registration is via the command)
    * D) Via Kubernetes `kubectl apply`. (You deploy the runner pod, but registration still happens)

50. Can you run CI/CD jobs on the Windows operating system with GitLab Runner?
    * **A) Yes, by installing GitLab Runner on a Windows machine and configuring a `shell` or `docker-windows` executor.**
    * B) Only via Docker containers running Linux.
    * C) No, GitLab Runner only supports Linux and macOS.
    * D) Only on GitLab SaaS runners.

## 🔹 Section 11: Variables & Interpolation

51. How do you correctly interpolate (use the value of) a variable within a `script` section?
    * A) `$(VAR)` (Used for command substitution in shell)
    * **B) `$VAR` or `${VAR}` (Standard shell variable expansion)**
    * C) `%VAR%` (Windows batch style)
    * D) `{{VAR}}` (Template engine style, not standard shell)

52. What is the purpose of the `dependencies` keyword when defined within a job?
    * **A) Control which artifacts (if any) are downloaded from jobs in previous stages.**
    * B) Define required Docker images.
    * C) Force job execution order (that's `needs` or `stages`).
    * D) Specify system packages to install.

53. How do you configure a job to collect and display a JUnit test report in the GitLab UI (e.g., on Merge Requests)?
    * **A)**
        ```yaml
        artifacts:
          reports:
            junit: path/to/report.xml # Or an array of paths
        ```
    * B)
        ```yaml
        reports:
          - type: junit
        ```
    * C) Use `junit-parse` in scripts. (Parsing might happen, but this doesn't integrate it with UI)
    * D) GitLab auto-detects all JUnit XML files. (Requires explicit configuration)

54. How do you use a variable within a top-level job name itself in `.gitlab-ci.yml`?
    * A) `job_$CI_COMMIT_REF_NAME:`
    * B) `job:${VAR}:`
    * **C) Variables cannot be directly interpolated into top-level job names.**
    * D) `name: "job-$VAR"` (The `name` keyword is not for job identifiers)

55. What is the correct way to escape a literal dollar sign (`$`) within a `script` block in `.gitlab-ci.yml` to prevent variable interpolation by GitLab?
    * **A) `$$`**
    * B) `\$` (This works for the shell, but GitLab might interpolate first)
    * C) `%24` (URL encoding)
    * D) `echo "$"` (Depends on shell quoting rules)

56. Which predefined CI/CD variable contains the commit SHA for the pipeline?
    * A) `$CI_SHA`
    * **B) `$CI_COMMIT_SHA`**
    * C) `$GIT_COMMIT`
    * D) `$COMMIT_HASH`

## 🔹 Section 12: Job Artifacts & Reports

57. How do you configure a job to extract code coverage percentage from its log output?
    * A)
        ```yaml
        artifacts:
          reports:
            coverage: coverage.txt # This is for Cobertura reports, not log parsing
        ```
    * **B) Use the `coverage` keyword with a regular expression:**
        ```yaml
        job:
          script:
            - echo "Coverage: 90%"
          coverage: '/Coverage:\s*(\d+%?)/'
        ```
    * C) Add `report_type: coverage` to `.gitlab-ci.yml`. (Not valid)
    * D) GitLab auto-detects coverage percentages from logs. (Requires `coverage` keyword)

58. What is the purpose of `artifacts:expose_as`?
    * **A) Expose a specific artifact with a given name in the Merge Request UI.**
    * B) Encrypt artifacts before uploading.
    * C) Share artifacts directly between different projects.
    * D) Delete artifacts immediately after the job completes.

59. How do you ensure artifacts are uploaded even if the job fails?
    * **A)**
        ```yaml
        artifacts:
          when: always
        ```
    * B)
        ```yaml
        artifacts:
          on_failure: true # Valid value, but 'always' covers success too
        ```
    * C) Use `save_artifacts: yes`. (Not valid)
    * D) GitLab saves artifacts on failure by default. (Default is `on_success`)

## 🔹 Section 13: Pipeline Efficiency

60. How does using the `needs` keyword typically improve pipeline performance compared to only using `stages`?
    * **A) Allows jobs to start as soon as their specific dependencies (`needs`) are met, rather than waiting for all jobs in a previous stage to complete.**
    * B) Reduces the total number of runners used. (Not directly)
    * C) Merges jobs from different stages into a single stage. (No, it creates a DAG)
    * D) Automatically cancels redundant jobs. (That's `interruptible` or `rules`)

61. What is the purpose of the `cache:key` keyword?
    * **A) Uniquely identify a cache archive, allowing control over when cache is shared or invalidated (e.g., per branch, per commit, based on lock files).**
    * B) Encrypt the cache contents.
    * C) Limit the maximum size of the cache.
    * D) Specify how long the cache should be kept before deletion.

62. How do you configure caching to be specific to each Git branch?
    * **A)**
        ```yaml
        cache:
          key: $CI_COMMIT_REF_SLUG # Uses a slug representation of the branch/tag name
          paths:
            - node_modules/
        ```
    * B) `cache: branch: true` (Not valid)
    * C) `cache: per_branch: yes` (Not valid)
    * D) GitLab automatically caches per branch by default. (Requires explicit `key` configuration)

## 🔹 Section 14: Security Scanning (GitLab Secure)

63. How do you typically enable SAST (Static Application Security Testing) in your pipeline?
    * **A) Include the official GitLab SAST template:**
        ```yaml
        include:
          - template: Security/SAST.gitlab-ci.yml
        ```
    * B) Add `security: sast` to jobs. (Not valid)
    * C) Use `scan: code` in scripts. (Not standard)
    * D) It's only available via GitLab Auto DevOps. (Templates can be used independently)

64. What is the purpose of `dependencies: []` often seen in SAST jobs included from templates?
    * A) Install tools required for scanning. (Tools are usually in the job's Docker image)
    * B) Define project dependencies for the scanner to analyze. (Scanner finds these itself)
    * C) Skip scanning if no relevant code files have changed. (That's handled by `rules`)
    * **D) Prevent the job from downloading artifacts from previous stages, ensuring it scans the current checkout.** (This is the most common reason for `dependencies: []` here)

65. How do you customize the behavior of SAST scanners (e.g., exclude rules, target specific paths)?
    * A) Edit the included `.gitlab-ci.yml` template directly. (Not recommended, overrides are better)
    * **B) Override predefined CI/CD variables used by the SAST template (e.g., `SAST_EXCLUDED_PATHS`).**
    * C) Modify a separate `sast-config.yaml` file. (Not the standard method)
    * D) Use `rules:custom` in the job definition. (Rules control job execution, not scanner config)

## 🔹 Section 15: GitLab API & Webhooks

66. How do you trigger a pipeline via the GitLab API using a personal access token or trigger token?
    * **A) Send a POST request to the pipeline trigger API endpoint:**
        ```bash
        # Example using a trigger token
        curl -X POST \
             --fail \
             -F token=YOUR_TRIGGER_TOKEN \
             -F ref=main \
             "[https://gitlab.example.com/api/v4/projects/YOUR_PROJECT_ID/trigger/pipeline](https://gitlab.example.com/api/v4/projects/YOUR_PROJECT_ID/trigger/pipeline)"
        ```
    * B) Send a GET request to `https://gitlab.com/api/v4/pipelines`. (This lists pipelines)
    * C) Use a `gitlab-pipeline-trigger` CLI tool. (Not an official GitLab tool)
    * D) It's only possible via the GitLab UI.

67. What is the primary purpose of configuring a pipeline webhook?
    * **A) Notify an external service or application about pipeline events (e.g., start, success, failure).**
    * B) Trigger manual jobs within a pipeline.
    * C) Schedule pipelines to run at specific times.
    * D) Authenticate GitLab Runners.

68. How can you retrieve the log (trace) of a specific job using the GitLab API?
    * **A) Send a GET request to the job trace endpoint:**
        ```bash
        curl --header "PRIVATE-TOKEN: <your_token>" "[https://gitlab.example.com/api/v4/projects/YOUR_PROJECT_ID/jobs/JOB_ID/trace](https://gitlab.example.com/api/v4/projects/YOUR_PROJECT_ID/jobs/JOB_ID/trace)"
        ```
    * B) `curl "https://gitlab.com/jobs/logs/1"` (Incorrect URL structure)
    * C) Use `gitlab-runner logs`. (This is for runner-level logs, not specific job traces)
    * D) Job logs are not accessible via the API.

## 🔹 Section 16: Advanced Job Control

69. How do you configure a single job definition to run multiple instances in parallel (e.g., for parallel testing)?
    * **A) Use the `parallel` keyword:**
        ```yaml
        test_job:
          script: ./run-test $CI_NODE_INDEX # Use predefined variables for coordination
          parallel: 5 # Runs 5 instances of test_job
        ```
    * B) Add `concurrent: true`. (Concurrency is a runner setting)
    * C) Define multiple identical jobs manually. (Inefficient)
    * D) GitLab does not support running a single job definition in parallel.

70. What is the purpose of the `interruptible` keyword?
    * **A) When set to `true`, allows newer pipelines for the same ref to automatically cancel older, still-running pipelines or jobs marked as interruptible.**
    * B) Pause jobs for manual approval (`when: manual`).
    * C) Retry failed jobs automatically (`retry`).
    * D) Skip non-essential stages (`allow_failure`).

71. How do you explicitly ensure a job runs only *after* another specific job (`job_a`) in a previous stage has successfully completed?
    * **A) Use `needs: [job_a]`. (This creates a direct dependency)**
    * B) Add `depends_on: job_a`. (Not a valid keyword, `needs` is used)
    * C) Use `rules: - when: on_success`. (This controls *when* a job runs based on conditions, doesn't define dependency like `needs`)
    * D) GitLab handles this automatically based on stages. (Stages provide sequential order, but `needs` allows bypassing that for specific dependencies)

## 🔹 Section 17: GitLab Runner Configuration

72. What is the default executor type when you install GitLab Runner (if none is specified during registration)?
    * A) Docker
    * **B) Shell**
    * C) Kubernetes
    * D) VirtualBox

73. How do you limit the total number of jobs a specific GitLab Runner can execute concurrently?
    * **A) Set the `concurrent` value in the runner's `config.toml` file.**
    * B) Add `limit: 4` to `.gitlab-ci.yml`. (Job-level, not runner-level)
    * C) Use `jobs: max: 4`. (Not valid)
    * D) Configure runner concurrency limits only in the GitLab UI. (Main config is `config.toml`)

74. What is a "tagged" runner?
    * **A) A runner that has been assigned specific tags, allowing jobs in `.gitlab-ci.yml` to target it using the `tags` keyword.**
    * B) A runner that automatically adds Git tags to releases.
    * C) A runner deployed within a Docker Swarm cluster.
    * D) A runner used exclusively for jobs triggered by Git tags.

## 🔹 Section 18: Error Handling

75. What does setting `allow_failure: true` for a job do?
    * **A) Allows the pipeline to proceed and potentially be marked as "passed" or "passed with warnings" even if this specific job fails.**
    * B) Retries the job automatically upon failure (`retry`).
    * C) Marks the job as optional, meaning it can be skipped manually. (`when: manual`)
    * D) Skips executing the job entirely (`when: never`).

76. How do you configure a job to be automatically retried up to 3 times if it fails?
    * A) `retry: 3` (Shorthand, implies max 3)
    * B) `attempts: 3` (Not valid)
    * **C)**
        ```yaml
        retry:
          max: 3
          # Optional: when: [api_failure, runner_system_failure]
        ```
    * D) `retry_on_failure: 3` (Not valid)

77. What is the default retry behavior for a job if the `retry` keyword is not specified?
    * A) Retry twice.
    * **B) Retry 0 times (no automatic retries).**
    * C) Retry indefinitely until it succeeds.
    * D) Retry once.

## 🔹 Section 19: Templates & Includes

78. How do you include a CI/CD configuration file from a *different* project within your GitLab instance?
    * **A)**
        ```yaml
        include:
          - project: 'my-group/my-shared-templates'
            ref: 'main' # Optional: specify branch/tag/SHA
            file: '/templates/.gitlab-ci-template.yml'
        ```
    * B) `template: git@gitlab.com:my-project/template.yml` (Not valid syntax)
    * C) `import: - url: "https://gitlab.com/template.yml"` (Not valid syntax)
    * D) GitLab does not support including configuration from other private projects.

79. What is the primary purpose of the `extends` keyword?
    * **A) Allows a job to inherit and reuse configuration from a YAML anchor or a hidden job template defined elsewhere in the configuration.**
    * B) Increase the timeout duration for a job.
    * C) Merge the configurations of multiple pipeline files. (`include` does this)
    * D) Clone the settings from one runner to another.

80. How do you override a specific setting (like the `script`) of a job that you are inheriting from using `extends`?
    * **A) Redefine the specific key (e.g., `script`) within the job that uses `extends`. The local definition takes precedence.**
    * B) Use `override: true`. (Not valid)
    * C) Delete the key from the template being extended. (Not possible directly)
    * D) Use `extends: override`. (Not valid)

## 🔹 Section 20: Miscellaneous

81. How can you influence the time zone used within a job's execution environment?
    * A)
        ```yaml
        job:
          timezone: "UTC" # Not a valid keyword
        ```
    * B) GitLab uses the server’s time zone exclusively. (Runner environment matters)
    * **C) Set the `TZ` environment variable within the job's scope (e.g., in `variables` or `before_script`).**
        ```yaml
        variables:
          TZ: "America/New_York"
        ```
    * D) Configure the time zone only in the runner's host OS settings. (Can be overridden by job variables)

82. What is the purpose of the `resource_group` keyword in a job definition?
    * **A) Ensures that only one job belonging to a specific resource group runs at a time across all pipelines for the project (useful for controlling access to shared, limited environments).**
    * B) Groups jobs visually within a pipeline stage.
    * C) Allocates specific cloud computing resources to a job.
    * D) Manages dependent `services` linked to a job.

83. How might you clean up unused Docker images, networks, or containers *after* a job has finished executing on a Docker-based runner?
    * **A) Add cleanup commands (like `docker system prune -af`) to the `after_script` section of the job.**
    * B) GitLab's Docker executor does this automatically after every job. (It removes the job container, but not necessarily cached images unless configured)
    * C) Use `cleanup: docker` in the job definition. (Not a valid keyword)
    * D) Configure Docker pruning options in the runner's `config.toml`. (Possible, but `after_script` gives job-level control)

84. What is the primary function of the `dependencies` keyword when used inside a job definition? *(Repeated Question)*
    * **A) Specify which artifacts from jobs in previous stages should be downloaded before this job runs. An empty array (`[]`) means download nothing.**
    * B) Define Docker image dependencies.
    * C) Install OS packages required by the script.
    * D) Trigger downstream pipeline executions.

85. How can you instruct GitLab CI/CD to skip running a pipeline for a specific Git commit?
    * **A) Include `[skip ci]` or `[ci skip]` in the commit message.**
    * B) Use `skip_pipeline: true` in the `.gitlab-ci.yml`. (Not valid)
    * C) Push using a special Git flag like `git push --no-ci`. (Not a standard Git flag)
    * D) Temporarily disable pipelines in the project's CI/CD settings before pushing. (Affects all commits)

86. What information does the predefined CI/CD variable `$CI_PIPELINE_SOURCE` provide?
    * **A) Indicates how the pipeline was triggered (e.g., `push`, `web`, `schedule`, `merge_request_event`, `api`, `trigger`).**
    * B) The Git branch name (`$CI_COMMIT_REF_NAME`).
    * C) The operating system of the runner.
    * D) The URL of the project’s repository (`$CI_PROJECT_URL`).

87. How do you configure a job to run *only* for pipelines associated with merge requests?
    * **A) Use rules checking the pipeline source or MR context:**
        ```yaml
        rules:
          - if: '$CI_PIPELINE_SOURCE == "merge_request_event"'
        # Or alternatively:
        # rules:
        #  - if: $CI_MERGE_REQUEST_IID
        ```
    * B)
        ```yaml
        only:
          - merge_requests # Older syntax
        ```
    * C) `when: merge_request` (Not valid)
    * D) `trigger: merge_request` (Not valid)

88. What is the effect of setting the CI/CD variable `CI_DEBUG_TRACE` to `true`?
    * **A) Enables verbose shell (`set -x`) output in job logs, showing commands as they are executed, which aids in debugging scripts.**
    * B) Traces GitLab API calls made by the job.
    * C) Provides detailed debugging information about the runner's internal operations.
    * D) Logs the values of all defined CI/CD variables at the start of the job.

89. How do you define a job that executes multiple commands sequentially in its main script?
    * **A) List each command as an item under the `script:` keyword:**
        ```yaml
        script:
          - echo "Step 1"
          - ./run_build.sh
          - echo "Step 2"
        ```
    * B)
        ```yaml
        scripts: # Incorrect keyword
          - "echo 'Step 1'"
          - "echo 'Step 2'"
        ```
    * C)
        ```yaml
        commands: # Incorrect keyword
          - command1: "echo 'Step 1'"
          - command2: "echo 'Step 2'"
        ```
    * D) Use multiple `script:` blocks within the same job. (Only one `script` block allowed)

90. What does the `GIT_STRATEGY` variable control?
    * **A) Determines how the GitLab Runner obtains the project's source code (e.g., `clone`, `Workspace`, or `none`).**
    * B) Defines the merge strategy used for merge commits (e.g., `merge`, `rebase`).
    * C) Configures Git server-side hooks.
    * D) Specifies the method used to authenticate with the Git repository.

91. How do you make a job run only if a specific CI/CD variable (`$MY_VAR`) is defined (has any value)?
    * **A) Use a rule checking if the variable exists:**
        ```yaml
        rules:
          - if: '$MY_VAR' # Evaluates to true if $MY_VAR is non-null and non-empty
        ```
    * B)
        ```yaml
        only:
          variables:
            - $MY_VAR # Older syntax, checks for specific value matches usually
        ```
    * C) `when: '$MY_VAR'` (Incorrect syntax)
    * D)
        ```yaml
        exists: # Incorrect keyword
          variables:
            - MY_VAR
        ```

92. What does the predefined CI/CD variable `$CI_PROJECT_DIR` represent?
    * **A) The absolute path to the directory on the runner where the project's repository has been cloned or fetched.**
    * B) The HTTP/SSH URL of the project’s Git repository (`$CI_REPOSITORY_URL`).
    * C) The directory where the `.gitlab-ci.yml` file is located within the repo.
    * D) The root namespace (group) of the project (`$CI_PROJECT_NAMESPACE`).

93. How can you run a long-running process in the background within a job's script so the script can continue?
    * **A) Use the shell's background operator (`&`) at the end of the command.**
        ```yaml
        script:
          - ./start-server & # Start server in background
          - sleep 5 # Give server time to start
          - ./run-tests # Run tests against the server
        ```
    * B) Add `background: true` to the job definition. (Not valid)
    * C) Use the `nohup` command (`nohup ./start-server &`). (Also works, prevents SIGHUP)
    * D) GitLab CI/CD jobs cannot execute background processes reliably. (They can via shell)

94. What is the fundamental difference between `before_script` and `script` in a job?
    * **A) Commands in `before_script` execute before commands in `script` within the same job.**
    * B) `script` is optional if `before_script` is defined. (No, `script` is usually required)
    * C) `before_script` is intended for cleanup tasks. (`after_script` is for cleanup)
    * D) They are functionally identical and interchangeable.

95. How do you configure a job to run *either* when triggered by a schedule *or* when triggered manually from the UI?
    * **A) Use `rules` combining both conditions:**
        ```yaml
        rules:
          - if: '$CI_PIPELINE_SOURCE == "schedule"'
          - when: manual # Allows manual triggering
        ```
    * B)
        ```yaml
        only:
          - schedules
          - web # 'web' refers to push events, not manual UI triggers
        ```
    * C) Use `allow_manual: true`. (Not a valid keyword)
    * D) A job cannot be triggered by both a schedule and manually.

96. How are artifacts typically passed between jobs created using the `parallel` keyword?
    * **A) Artifacts uploaded by one parallel job instance are available to jobs in subsequent stages (just like non-parallel jobs). They aren't typically passed *between* the parallel instances themselves.**
    * B) Use `needs: []` on the parallel jobs. (Doesn't facilitate sharing between them)
    * C) Parallel job instances cannot share artifacts during the pipeline run.
    * D) Define explicit `dependencies` between the parallel job instances. (Not standard practice)

97. What does the predefined CI/CD variable `$CI_COMMIT_MESSAGE` contain?
    * **A) The full message of the commit that triggered the pipeline.**
    * B) The title of the associated merge request (`$CI_MERGE_REQUEST_TITLE`).
    * C) The aggregated output logs from the job's script.
    * D) The log messages generated by the GitLab Runner itself.

98. How can you check if your `.gitlab-ci.yml` file has valid syntax *before* committing and pushing it?
    * **A) Use the CI Lint tool available in the GitLab project's UI (CI/CD > Editor or CI/CD > Pipelines > CI Lint).**
    * B) Run `gitlab-ci validate`. (Not a standard command)
    * C) Commit and push, then check the pipeline status for linting errors. (Works, but isn't *before*)
    * D) Use a generic YAML validator like `yamllint`. (Checks YAML syntax, but not GitLab CI/CD specific logic/keywords)

99. What does the predefined CI/CD variable `$CI_REGISTRY` represent?
    * **A) The URL of the GitLab Container Registry associated with the project.**
    * B) The URL for Docker Hub.
    * C) The address of the connected Kubernetes cluster's internal registry.
    * D) The base URL for downloading job artifacts.

100. How do you ensure a specific job runs absolutely last in the entire pipeline, regardless of other job timings or `needs` configurations?
     * **A) Place the job in the very last defined stage in the `stages` list, and ensure no later stages are defined.**
     * B) Use `needs: [all]`. (Not a valid value for `needs`)
     * C) Add `priority: high`. (Priority isn't a standard keyword for ordering)
     * D) Create a final stage (e.g., `cleanup`) and put the job there without any `needs` keyword. (Placing it in the last stage is the key)
