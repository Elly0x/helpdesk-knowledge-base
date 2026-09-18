# Redefinir senha e desbloquear conta no Active Directory

**Categoria:** Incidente Nível 1
**Tempo médio de resolução:** 2-5 min
**Ferramenta:** Active Directory Users and Computers (ADUC) ou PowerShell

## Sintoma relatado pelo usuário
- "Não consigo fazer login, diz que a senha está errada."
- "Minha conta está bloqueada."
- "Esqueci minha senha."

## Diagnóstico rápido

| Mensagem no login | Causa provável |
|---|---|
| "The user name or password is incorrect" | Senha errada ou expirada |
| "This user account has been locked out" | Conta bloqueada (várias tentativas erradas) |
| "Your account has been disabled" | Conta desativada por um admin |

## Procedimento — via interface gráfica (ADUC)

1. Abra **Active Directory Users and Computers** no servidor.
2. Localize o usuário na OU correspondente (ex: `empresa.local/Atendimento`).
3. Clique com o botão direito no usuário → **Reset Password**.
4. Defina uma senha temporária que siga a política de complexidade do domínio.
5. Marque **"User must change password at next logon"** — nunca entregue uma senha definitiva você mesmo.
6. Se a conta estiver com o ícone de bloqueio (cadeado vermelho): botão direito → **Properties** → aba **Account** → marque **"Unlock account"**.
7. Peça para o usuário tentar logar novamente e confirmar.

## Procedimento — via PowerShell (mais rápido para quem atende vários chamados)

```powershell
# Redefinir senha
Set-ADAccountPassword -Identity "joao.silva" -Reset -NewPassword (ConvertTo-SecureString "SenhaTemp@2026" -AsPlainText -Force)

# Forçar troca no próximo login
Set-ADUser -Identity "joao.silva" -ChangePasswordAtLogon $true

# Desbloquear conta
Unlock-ADAccount -Identity "joao.silva"
```

## Boas práticas
- Nunca envie a senha temporária por e-mail sem antes confirmar a identidade do usuário (ramal, ticket, ou pergunta de segurança).
- Registre no chamado: horário, motivo do bloqueio (se souber) e se houve troca de senha.
- Se a conta bloquear repetidamente no mesmo dia, verifique se não há um dispositivo (celular, app antigo) tentando autenticar com a senha antiga em loop — causa comum de "self lockout".

## Escalar para Nível 2 se
- O usuário continuar bloqueado imediatamente após o desbloqueio (possível sincronização de senha em cache ou ataque de força bruta).
- A conta estiver desativada por política de segurança/RH, não por erro de login.
