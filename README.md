# Laboratório Virtual de Suporte & Active Directory

> **Status:** projeto em andamento

Simulação de um ambiente corporativo de infraestrutura Windows, reproduzindo tarefas reais de um analista de suporte/TI: administração de domínio, gestão de usuários e aplicação de políticas de grupo.

## Objetivo

Demonstrar, na prática, competências essenciais de suporte técnico Nível 1/2 em ambiente de domínio Windows:
- Instalação e configuração de um Domain Controller (Active Directory Domain Services)
- Organização de usuários por Unidades Organizacionais (OUs)
- Ingresso de máquinas cliente no domínio
- Criação e aplicação de Group Policy Objects (GPOs)

## Ambiente

| Item | Detalhe |
|---|---|
| Virtualização | Oracle VirtualBox |
| Servidor | Windows Server 2022 (Evaluation) — Domain Controller |
| Cliente | Windows 10/11, ingressado no domínio |
| Domínio | `empresa.local` |

## Estrutura implementada

- **OUs:** Financeiro, TI, Atendimento
- **Usuários de teste** criados em cada OU
- **GPO aplicada:** restrição de acesso ao Painel de Controle na OU Atendimento

## Documentação técnica

O passo a passo completo da configuração está em [GUIA-EXECUCAO.md](GUIA-EXECUCAO.md).

## Evidências

_(prints da configuração serão adicionados na pasta `prints/` conforme o ambiente for montado)_

## Aprendizados

_(a preencher ao final, com os principais desafios encontrados durante a configuração)_
