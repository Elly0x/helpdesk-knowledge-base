# Guia de execução — Laboratório Virtual de Suporte & Active Directory

Passo a passo técnico usado para montar este laboratório, do zero até a GPO funcionando.

## Pré-requisitos
- Notebook com pelo menos 8 GB de RAM (16 GB é confortável) e ~60 GB livres de disco.
- Virtualização habilitada na BIOS/UEFI (Intel VT-x ou AMD-V).

## Passo a passo

### 1. Instalar o VirtualBox
Baixe e instale o [Oracle VirtualBox](https://www.virtualbox.org/) (gratuito).

### 2. Baixar o Windows Server
Baixe a versão de avaliação (180 dias grátis) no site da Microsoft: **Windows Server 2022 Evaluation** (ISO).

### 3. Criar a VM do servidor
- Nome: `DC01` (Domain Controller)
- RAM: 4 GB · Disco: 40 GB (dinâmico)
- Instale o Windows Server a partir da ISO.

### 4. Instalar o Active Directory Domain Services (AD DS)
No **Server Manager** → **Add Roles and Features** → marque **Active Directory Domain Services** → instalar.
Depois, clique no aviso de notificação → **Promote this server to a domain controller** → **Add a new forest** → nome do domínio: `empresa.local`.

### 5. Criar a VM cliente
- Nome: `PC01`
- Windows 10 ou 11
- Configure a rede da VM como **Rede Interna** (Internal Network) — a mesma usada pelo `DC01`, para que se enxerguem.
- Configure o IP do `PC01` manualmente com o DNS apontando para o IP do `DC01`.
- Entre em **Sistema → Sobre → Ingressar em um domínio** → digite `empresa.local`.

### 6. Estruturar o Active Directory
No `DC01`, abra **Active Directory Users and Computers**:
- Crie as OUs: `Financeiro`, `TI`, `Atendimento`.
- Crie 2-3 usuários de teste em cada OU (ex: `joao.silva`, `maria.souza`).

### 7. Criar e aplicar uma GPO simples
**Group Policy Management** → botão direito na OU `Atendimento` → **Create a GPO in this domain**.
Sugestões de política:
- Bloquear acesso ao Painel de Controle (`User Configuration → Administrative Templates → Control Panel → Prohibit access to Control Panel`).
- Ou trocar o papel de parede automaticamente (`User Configuration → Administrative Templates → Desktop → Desktop Wallpaper`).

Depois, no `PC01`, rode `gpupdate /force` e faça login com um usuário da OU `Atendimento` pra confirmar que a política pegou.

## Checklist de documentação (prints a tirar)
- [ ] Print do AD DS instalado e o domínio `empresa.local` promovido
- [ ] Print das OUs criadas (Financeiro, TI, Atendimento)
- [ ] Print dos usuários de teste criados
- [ ] Print do `PC01` ingressado no domínio (Sistema → Sobre)
- [ ] Print da GPO criada
- [ ] Print da GPO funcionando no `PC01` (Painel de Controle bloqueado ou papel de parede alterado)

## Estrutura sugerida do repositório
```
lab-virtual-ad/
├── README.md          <- este guia + resultado final
├── prints/
│   ├── 01-ad-ds-instalado.png
│   ├── 02-ous-criadas.png
│   ├── 03-usuarios-teste.png
│   ├── 04-pc-no-dominio.png
│   ├── 05-gpo-criada.png
│   └── 06-gpo-funcionando.png
```

Quando terminar, é só substituir esse README pela versão final: mesma estrutura, mas com os prints embutidos e uma seção "O que aprendi" contando os erros/obstáculos que apareceram no caminho — isso conta muito numa entrevista.
