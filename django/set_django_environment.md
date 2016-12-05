## Django 개발 환경 설정

#### `pyenv`, `virualenv`, `autoenv` 설치
```
# 파이썬 버전 관리를 위해 pyenv 설치
$ git clone https://github.com/yyuu/pyenv.git ~/.pyenv

$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
$ echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
# zsh을 사용하는 경우 ~/.zshrc # ubuntu나 fedora는 ~/.bashrc

$ exec $SHELL
```
```
# 프로젝트 별로 파이썬 버전 관리와 프레임워크, 라이브러리 등을 관리하기 위해 pyenv-virtualenv 설치

$ git clone https://github.com/yyuu/pyenv-virtualenv.git ~/.pyenv/plugins/pyenv-virtualenv

$ echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bash_profile
# zsh을 사용하는 경우 ~/.zshrc # ubuntu나 fedora는 ~/.bashrc

$ exec "$SHELL"
```
```
# autoenv를 사용하면 .env 파일을 찾아 스크립트를 자동으로 실행시켜서 해당 개발환경을 설정해줄 수 있다.

$ git clone git://github.com/kennethreitz/autoenv.git ~/.autoenv
$ echo 'source ~/.autoenv/activate.sh' >> ~/.bashrc
# zsh을 사용하는 경우 ~/.zshrc # ubuntu나 fedora는 ~/.bashrc
```

더 자세한 내용은

* [pyenv](https://github.com/yyuu/pyenv)
* [pyenv-virtualenv](https://github.com/yyuu/pyenv-virtualenv)
* [autoenv](https://github.com/kennethreitz/autoenv)

#### `pyenv`, `virualenv`  사용하기 
```
$ pyenv install 3.5.2
$ pyenv virtualenv 3.5.2 blog

$ pyenv activate 3.5.2 blog
```

#### `autoenv`  사용하기 
```
# ~/blog/.nev
pyenv activate blog

$ cd ~/blog/

(blog) $
```
