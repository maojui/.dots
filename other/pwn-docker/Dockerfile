FROM ubuntu:bionic

RUN apt update; \
    apt upgrade -y

RUN apt install -y \
    python python-dev python-pip \
    python3 python3-dev python3-pip \
    htop tmux git zsh gcc g++ make \
    cmake binutils curl wget netcat nmap \
    vim zip unzip locales \
    gdb strace ltrace; \
    rm -rf /var/lib/apt/lists/*

RUN dpkg --add-architecture i386; \
    apt update; apt install -y libc6:i386 libstdc++6:i386; \
    rm -rf /var/lib/apt/lists/*

RUN cd /root && git clone https://github.com/maojui/.dots.git; \
    cd .dots && make all && locale-gen en_US.UTF-8

RUN pip install -U pip --no-cache-dir; \
    sed -i 's/from pip import main/from pip._internal import main/' /usr/bin/pip; \
    pip install pwntools ipython --no-cache-dir; \
    pip3 install -U pip --no-cache-dir; \
    sed -i 's/from pip import main/from pip._internal import main/' /usr/bin/pip3; \
    pip3 install git+https://github.com/arthaud/python3-pwntools.git ipython --no-cache-dir

RUN git clone --depth 1 https://github.com/longld/peda.git ~/.peda; \
    echo "source ~/.peda/peda.py" >> ~/.gdbinit

RUN git clone --depth 1 https://github.com/scwuaptx/Pwngdb.git ~/.pwngdb; \
    cp ~/.pwngdb/.gdbinit ~/; \
    sed -i 's/~\/Pwngdb/~\/\.pwngdb/g' ~/.gdbinit; \
    sed -i 's/~\/peda/~\/\.peda/g' ~/.gdbinit; \
    apt install -y libc6-dbg libc6-dbg:i386; \
    rm -rf /var/lib/apt/lists/*

RUN chsh -s /usr/bin/zsh; \
    bash -c 'history -c'

CMD zsh
