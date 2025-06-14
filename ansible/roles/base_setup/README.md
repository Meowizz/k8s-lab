# Ansible Role: k8s_prepare

Роль подготавливает Linux-ноды (CentOS 7/8, AlmaLinux, Rocky Linux) для установки Kubernetes-кластера.

Выполняются действия:

- Перевод SELinux в permissive режим
- Отключение swap (временно и навсегда)
- Остановка firewalld (для простоты в лабораторной среде)
- Настройка параметров ядра (sysctl)
- Установка Docker и его настройка с systemd cgroup-драйвером
- Добавление репозитория Kubernetes и установка kubelet, kubeadm, kubectl
- Перезагрузка ноды при необходимости

---

## Требования

- Ansible 2.9+
- Python 3 на таргет-нодах
- Поддерживаемые дистрибутивы:
  - CentOS 7/8
  - AlmaLinux / Rocky Linux

---

## Переменные роли

| Переменная     | Описание                             | Значение по умолчанию |
|----------------|--------------------------------------|------------------------|
| `kube_version` | Версия Kubernetes (без последнего `.0`) | `"1.29"`              |

> Пример: `"1.29"` установит `kubelet-1.29.0`, `kubeadm-1.29.0` и т.д.

---

## Пример использования

```yaml
- name: Prepare nodes for Kubernetes
  hosts: all
  become: yes
  vars:
    kube_version: "1.29"
  roles:
    - k8s_prepare
