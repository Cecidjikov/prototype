# Създаване на работна папка
mkdir my_project
cd my_project

# Инициализиране на работната папка като Git хранилище
git init

# Клониране на хранилището
git clone https://github.com/вашето-потребителско-име/вашето-хранилище.git

# Превключване към клон 'singleton'
git checkout -b singleton

#pragma once

#include <iostream>

class Logger {
private:
    Logger() {}
    static Logger* instance;

public:
    static Logger* getInstance() {
        if (!instance) {
            instance = new Logger;
        }
        return instance;
    }

    void log(const std::string& message) {
        std::cout << "Log: " << message << std::endl;
    }
};

Logger* Logger::instance = nullptr;

#pragma once

#include "Logger.h"

class IProgram {
protected:
    Logger* logger;

public:
    IProgram() {
        logger = Logger::getInstance();
    }

    virtual void log(const std::string& message) = 0;
};

# Превключване към клон 'prototype'
git checkout -b prototype

#pragma once

#include <iostream>

class DB {
public:
    void connect() {
        std::cout << "Connected to the database" << std::endl;
    }

    void query(const std::string& sql) {
        std::cout << "Executing query: " << sql << std::endl;
    }

    DB* clone() {
        return new DB(*this);
    }
};

# Превключване към основния клон
git checkout master

# Обединяване на промените от клон 'singleton'
git merge singleton

# Обединяване на промените от клон 'prototype'
git merge prototype

# Разрешаване на конфликти, ако такива има
# След решаването на конфликтите, продължете с командите:
git add .
git merge --continue

# Push-ване на промените към хранилището
git push origin master

# Изтриване на клон 'singleton'
git branch -d singleton

# Изтриване на клон 'prototype'
git branch -d prototype

# Push-ване на промените след изтриването на клоновете
git push origin master
