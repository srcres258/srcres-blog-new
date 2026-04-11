pipeline {
  agent any

  options {
    disableConcurrentBuilds()
    timestamps()
  }

  triggers {
    githubPush()
  }

  environment {
    SOURCE_BRANCH = 'master'
    TARGET_REPO = 'https://github.com/srcres258/srcres258.github.io.git'
    TARGET_BRANCH = 'main'
    TARGET_DIR = 'gh-pages-repo'
  }

  stages {
    stage('Checkout source') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: "*/${env.SOURCE_BRANCH}"]],
          userRemoteConfigs: [[url: 'https://github.com/srcres258/srcres-blog-new.git']]
        ])
      }
    }

    stage('Check Node.js version >= v24.14.1') {
      steps {
        sh '''
          set -eu
          if ! command -v node >/dev/null 2>&1; then
            echo "ERROR: Node.js is not installed."
            exit 1
          fi

          required_version="24.14.1"
          installed_version="$(node -v | sed 's/^v//')"

          compare_versions() {
            [ "$1" = "$2" ] && return 0
            local first
            first="$(printf '%s\n%s\n' "$1" "$2" | sort -V | head -n1)"
            [ "$first" != "$1" ]
          }

          if ! compare_versions "$installed_version" "$required_version"; then
            echo "ERROR: Node.js >= v${required_version} is required, but found v${installed_version}."
            exit 1
          fi

          echo "Node.js version check passed: v${installed_version}"
        '''
      }
    }

    stage('Install dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Build Hexo static files') {
      steps {
        sh 'npx hexo clean && npx hexo generate'
      }
    }

    stage('Deploy to srcres258.github.io/main') {
      steps {
        withCredentials([string(credentialsId: 'github-token', variable: 'GITHUB_TOKEN')]) {
          sh '''
            set -eu
            set +x

            if [ -z "${GITHUB_TOKEN:-}" ]; then
              echo "ERROR: GITHUB_TOKEN is not set."
              exit 1
            fi

            rm -rf "$TARGET_DIR"

            ASKPASS_SCRIPT="$(mktemp)"
            trap 'rm -f "$ASKPASS_SCRIPT"' EXIT
            cat > "$ASKPASS_SCRIPT" <<'EOF'
#!/bin/sh
case "$1" in
  *Username*) echo "x-access-token" ;;
  *Password*) echo "$GITHUB_TOKEN" ;;
  *) echo "" ;;
esac
EOF
            chmod 700 "$ASKPASS_SCRIPT"

            export GIT_ASKPASS="$ASKPASS_SCRIPT"
            export GIT_TERMINAL_PROMPT=0

            git clone --branch "$TARGET_BRANCH" --single-branch "$TARGET_REPO" "$TARGET_DIR"

            cd "$TARGET_DIR"

            # Delete all files except CNAME (including hidden files/directories).
            find . -mindepth 1 ! -name '.' ! -name '..' ! -name 'CNAME' ! -path './.git*' -exec rm -rf {} +

            # Copy newly generated static files from source repo public/.
            cp -a "$WORKSPACE/public/." .

            git config user.name "srcres258"
            git config user.email "src.res.211@gmail.com"

            git add -A

            if git diff --cached --quiet; then
              echo "No changes to commit."
              exit 0
            fi

            git commit -m "Update"
            git push origin "$TARGET_BRANCH"
          '''
        }
      }
    }
  }

  post {
    success {
      echo 'Pipeline completed successfully.'
    }
    failure {
      echo 'Pipeline failed. Check stage logs for details.'
    }
  }
}
