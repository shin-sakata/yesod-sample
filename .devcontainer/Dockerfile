FROM ubuntu:18.04

# aptの初期化
RUN apt update -y && apt upgrade -y

# stack install
RUN apt install curl -y
RUN curl -sSL https://get.haskellstack.org/ | sh

# stack path
ENV PATH ~/.local/bin:$PATH
ENV PATH $(stack path --local-bin):$PATH
ENV PATH $(stack path --compiler-bin):$PATH

RUN stack setup

# hie dependencies
# https://github.com/haskell/haskell-ide-engine/blob/master/README.md#installation-from-source
RUN apt install -y libicu-dev libtinfo-dev libgmp-dev zlib1g-dev

# install haskell-ide-engine
RUN git clone https://github.com/haskell/haskell-ide-engine --recurse-submodules
RUN cd /haskell-ide-engine && stack ./install.hs hie-8.6.5
RUN cd /haskell-ide-engine && stack ./install.hs data

# install stylish-haskell
RUN apt install -y stylish-haskell

# Yesodの依存
RUN apt install -y build-essential zlib1g-dev
RUN apt install -y sqlite3 libsqlite3-dev

# Locale対応
# language-javascript-0.6.0.12だとLocale設定していないと動かない
# https://github.com/erikd/language-javascript/issues/86
RUN apt install -y language-pack-ja-base language-pack-ja ibus-mozc
RUN echo 'export LANG=ja_JP.UTF-8' >> /root/.bashrc && echo 'export LANGUAGE="ja_JP:ja"' >> /root/.bashrc && echo 'export LC_ALL=ja_JP.utf8' >> /root/.bashrc
