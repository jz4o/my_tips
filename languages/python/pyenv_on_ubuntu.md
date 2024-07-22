# pyenv on ubuntu: Ubuntu に pyenv をインストールする

## 確認環境

```sh
$ cat /etc/os-release
PRETTY_NAME="Ubuntu 24.04 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=noble
LOGO=ubuntu-logo

```

## パッケージをインストール

1. `$ sudo apt-get update`

1. `$ sudo apt-get upgrade`

1. `$ sudo apt-get install -y build-essential curl gcc git libbz2-dev libffi-dev liblzma-dev libncurses5-dev libreadline-dev libsqlite3-dev libssl-dev make zlib1g zlib1g-dev`

## pyenv をインストール

1. `$ curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash`
   
1. ```
   $ cat <<'EOF' >> ~/.bashrc

   # Load pyenv automatically by appending
   # the following to
   # ~/.bash_profile if it exists, otherwise ~/.profile (for login shells)
   # and ~/.bashrc (for interactive shells) :
   
   export PYENV_ROOT="$HOME/.pyenv"
   [[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
   eval "$(pyenv init -)"
   
   # Restart your shell for the changes to take effect.
    
   # Load pyenv-virtualenv automatically by adding
   # the following to ~/.bashrc:
    
   eval "$(pyenv virtualenv-init -)"
   EOF
   ```

1. `$ exec $SHELL -l`

1. `$ pyenv --version`

## コマンドメモ

* インストール可能なバージョンを出力する
  * `$ pyenv install --list`
* 任意のバージョンをインストールする
  * `$ pyenv install <version>`
* 任意のバージョンをアンインストールする
  * `$ pyenv uninstall <version>`
* インストール済みのバージョンを出力する
  * `$ pyenv versions`
* システム全体で使用するバージョンを設定する
  * `$ pyenv global <version>`
* カレントディレクトリで使用するバージョンを設定する
  * `$ pyenv local <version>`
