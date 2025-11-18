# 00_Lab_Architecture_Setup: Base de Monitoramento NOC

## 1. Visão Geral e Estratégia do Laboratório

Este arquivo é o inventário principal do projeto, onde registro todas as configurações das máquinas virtuais. 
A infraestrutura foi construída para simular um ambiente corporativo, isolado e monitorado, focado em **Operações de TI (NOC/SOC)**.

O objetivo é a prática de *troubleshooting* metódico, utilizando o **Zabbix** como principal ferramenta de detecção de anomalias e o **Active Directory** como base de identidade.

---

## 2. Inventário de Ativos e Topologia de Rede

O ambiente é virtualizado no VirtualBox e opera em uma rede interna isolada, garantindo controle total sobre DNS e tráfego.

### Mapa de Ativos (Inventory)

| Hostname | Endereço IP | Sistema Operacional | Função Primária | Status de Monitoramento |
| :--- | :--- | :--- | :--- | :--- |
| **SRV-DC01** | `10.0.0.10` | Windows Server 2022 | **Controlador de Domínio (DC)** | Monitorado (Zabbix Agent 2) |
| **ZABBIX-SRV** | `10.0.0.30` | Zabbix Appliance (Linux) | **Servidor de Monitoramento** | Online / Frontend Web |
| **WKS-01** | `10.0.0.20` | Windows 11 | Estação de Trabalho Cliente | Membro do Domínio `MeuLab.local` |

---

## 3. Configurações de Nível Crítico (Zabbix & AD)

### 3.1. Zabbix: Implementação e Conectividade
O Zabbix Server foi instalado em um Appliance Linux (garantindo a prática de console) e o Agente Zabbix 2 no Windows Server.

* **Configuração Linux:** O IP Estático (`10.0.0.30`) foi configurado manualmente via console (`vi`).
* **Comunicação:** O `SRV-DC01` está cadastrado no Zabbix. A Regra de Firewall de Entrada (`wf.msc`) para a porta **TCP 10050** foi criada para permitir a coleta de métricas.

### 3.2. Active Directory e Funções Essenciais
* **Domínio Principal:** `MeuLab.local`.
* **Roles Instaladas:** Active Directory Domain Services (AD DS) e DNS.
* **GPOs e OUs:** Estrutura de Unidades Organizacionais (`Minha_Empresa`) e GPOs básicas criadas para gestão de permissões.

### 3.3. Resolução de Incidentes de Nível 3 (NTP)
Durante a configuração, um incidente de sincronização de tempo foi resolvido, resultando nas seguintes ações permanentes para o NOC:

* **Regra de NTP Outbound:** Criada uma Regra de Firewall de **Saída (Outbound)** para a porta **UDP 123** no `SRV-DC01` para garantir que o PDC Emulator possa buscar a hora correta da internet.
* **Serviço W32Time:** Configuração forçada (`w32tm`) para corrigir conflitos de GPO e garantir o status `Mestre do Tempo` no domínio.

---
*Esta documentação reflete o estado estável da infraestrutura. Qualquer alteração ou incidente será registrado nos arquivos de relatório subsequentes.*
