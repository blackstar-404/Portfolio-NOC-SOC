# 01_Lab_CPU_Monitoring_Windows  
**Incidente de CPU em Servidor Windows monitorado com Zabbix**

## 1. Contexto do Lab

Este laboratório utiliza a arquitetura definida no arquivo [`00_Lab_Architecture_Setup`](./00_Lab_Architecture_Setup.md). O ambiente foi construído em VirtualBox, contando com:

- **Zabbix Server** (`ZABBIX-SRV` – Linux)  
- **Windows Server 2022** para testes e Active Directory (`SRV-DC01`)  
- **Windows 11** como estação cliente (`WKS-01`)  
- Rede interna, controle de DNS e serviços essenciais detalhados no setup inicial  

## 2. Objetivo

Simular a rotina de um analista NOC Jr diante de um alerta de CPU alta em um servidor Windows, exercitando:

- Acompanhamento de triggers no painel do Zabbix  
- Validação do incidente diretamente no servidor afetado  
- Classificação de criticidade (P2/P3)  
- Documentação do incidente e acompanhamento até a normalização  

## 3. Configuração do Trigger

Utilizado trigger nativo do template “Windows by Zabbix agent”:


# Incidente NOC – CPU Alta

**ID:** INC-2025-11-18-0001  
**Título:** CPU privileged time alta em Servidor_Lab  
**Tipo:** Incidente  
**Host afetado:** Servidor_Lab  
**Detectado por:** Zabbix  
**Hora de abertura:** 04:14:14 PM  
**Criticidade:** P3 (laboratório) | P2 (produção)  
**Descrição:** Alerta disparado pelo trigger "Windows: CPU privileged time is too high (over 30% for 5m)"

## Validação
- Confirmada CPU alta via Task Manager
- Processo causador identificado: simulado para teste
- Não é falso positivo

## Ação Inicial
- Encerramento ou redução dos processos geradores de carga

## Fechamento
- Zabbix mudou status para RESOLVED após normalização
- Recovery time registrado: 04:15:15 PM
- Duração do incidente: ~1 minuto
- Status final: Resolvido
