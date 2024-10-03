# Используем базовый образ CentOS 7
FROM centos:7

# Исправляем репозитории CentOS на архивные
RUN sed -i 's|^mirrorlist=|#mirrorlist=|g' /etc/yum.repos.d/CentOS-Base.repo && \
    sed -i 's|^#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-Base.repo

# Устанавливаем зависимости для Python
RUN yum -y update && \
    yum -y install epel-release && \
    yum -y install gcc openssl-devel bzip2-devel libffi-devel zlib-devel wget make

# Устанавливаем Python 3.7
RUN cd /usr/src && \
    wget https://www.python.org/ftp/python/3.7.9/Python-3.7.9.tgz && \
    tar xzf Python-3.7.9.tgz && \
    cd Python-3.7.9 && \
    ./configure --enable-optimizations && \
    make altinstall

# Устанавливаем pip
RUN python3.7 -m ensurepip --upgrade && \
    python3.7 -m pip install --upgrade pip

# Устанавливаем необходимые Python-библиотеки
RUN python3.7 -m pip install flask flask-jsonpify flask-restful

# Копируем ваше приложение в контейнер
WORKDIR /app
COPY python-api.py /app/

# Указываем порт, на котором будет запускаться Flask-приложение
EXPOSE 5290

# Команда для запуска приложения
CMD ["python3.7", "python-api.py"]
