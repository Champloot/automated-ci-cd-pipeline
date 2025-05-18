# Реализация CI/CD-конвейера для автоматизации развертывания веб-сервера на базе Vagrant, Ansible, Jenkins и GitHub


## Описание
Проект демонстрирует создание автоматизированного CI/CD конвейера для веб-сервера Nginx. При изменении файла `index.html` в GitHub, Jenkins запускает Ansible-плейбук для обновления сервера. Инфраструктура развертывается с помощью Vagrant и включает три виртуальные машины:
- **Jenkins-сервер** (CI/CD оркестрация).
- **Ansible-контроллер** (управление конфигурацией).
- **Веб-сервер Nginx** (хостинг статического контента).

## Цели
- Автоматизация развертывания и обновления веб-сервера.
- Интеграция инструментов DevOps: Vagrant, Ansible, Jenkins, GitHub.
- Минимизация ручного вмешательства в процесс доставки кода.

## Технологии и инструменты
- **Виртуализация**: Vagrant, VirtualBox.
- **CI/CD**: Jenkins.
- **Управление конфигурацией**: Ansible.
- **Веб-сервер**: Nginx.
- **Контроль версий**: GitHub.

## Требования
- Установленные [Vagrant](https://www.vagrantup.com/) и [VirtualBox](https://www.virtualbox.org/).
- Учетная запись GitHub.
- Базовые знания работы с терминалом.

## Установка и настройка

### 1. Клонирование репозитория
```bash
git clone https://github.com/Champloot/devops_practice.git
cd devops_practice
```
2. Запуск виртуальных машин
```bash
vagrant up
```
После выполнения команды будут созданы три виртуальные машины:

Jenkins: 192.168.56.10.

Ansible: 192.168.56.11.

Nginx: 192.168.56.12.

3. Настройка Jenkins
Откройте веб-интерфейс Jenkins: http://192.168.56.10:8080.

Получите пароль из файла на VM_1:

```bash
vagrant ssh jenkins
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
Установите рекомендованные плагины и создайте администратора.

Настройте Pipeline:

Тип задачи: Pipeline.

SCM: Укажите URL репозитория GitHub.

Script Path: Jenkinsfile.

4. Настройка Ansible
Инвентарь (inventory.ini) и плейбуки (deploy.yml) уже настроены в репозитории.

Проверьте работу Ansible вручную:

```bash
ansible-playbook -i ansible/inventory.ini ansible/deploy.yml
```
Использование
Внесите изменения в файл index.html в репозитории GitHub.

Запустите Pipeline в Jenkins (вручную или через веб-хук).

Проверьте обновленную страницу по адресу: http://192.168.56.12.

Архитектура
Архитектура

GitHub: Хранилище кода и триггер изменений.

Jenkins: Оркестрация CI/CD пайплайна.

Ansible: Настройка веб-сервера через плейбуки.

Nginx: Обслуживание статического контента.

Примеры
```Jenkinsfile
groovy
pipeline {
    agent any
    stages {
        stage('Deploy') {
            steps {
                sh """
                ssh -o StrictHostKeyChecking=no \
                    -i /var/lib/jenkins/.ssh/id_rsa \
                    vagrant@192.168.56.11 \
                    'ansible-playbook -i ansible/inventory.ini ansible/deploy.yml'
                """
            }
        }
    }
}
```
Проблемы и ограничения
Проект развернут локально. Для продакшена рекомендуется использовать облачные решения (AWS, GCP).

Веб-хуки между GitHub и Jenkins требуют дополнительной настройки для автоматизации.

Лицензия
Проект распространяется под лицензией MIT.

Автор
Artem Verchenko
GitHub: Champloot
