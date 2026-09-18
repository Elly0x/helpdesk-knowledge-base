# Guia de boas práticas de segurança: identificando e-mails de phishing

**Categoria:** Conscientização de segurança / Suporte ao usuário final
**Público:** Usuários finais (mas todo técnico de suporte precisa saber ensinar isso)

## Por que isso é chamado de suporte
Grande parte dos chamados de "vírus", "conta invadida" ou "computador lento do nada" começa com um clique em e-mail de phishing. Ensinar o usuário a reconhecer é tão parte do trabalho quanto resolver o incidente depois.

## Os 5 sinais mais comuns

1. **Urgência artificial** — "sua conta será bloqueada em 24h", "ação imediata necessária". Phishing pressiona para você não pensar.
2. **Remetente estranho** — o nome exibido diz "Suporte Microsoft", mas o e-mail real é algo como `suporte@micros0ft-seguranca.com`. Sempre passe o mouse sobre o nome do remetente antes de confiar.
3. **Links que não batem com o texto** — passe o mouse (sem clicar) sobre o link e compare a URL real que aparece embaixo com o que o texto promete.
4. **Pedido de dados sensíveis por e-mail** — bancos, RH e TI legítimos não pedem senha, código de 2FA ou dados de cartão por e-mail.
5. **Erros de português/formatação estranha** — nem sempre presente (phishing bom não tem erro), mas ainda é um sinal comum.

## O que orientar o usuário a fazer

- **Não clicar** em links ou baixar anexos de remetentes não confirmados.
- **Não responder** pedindo confirmação — isso confirma ao atacante que o e-mail é válido e está sendo lido.
- **Reportar** para o time de TI/segurança (encaminhar como anexo, não só encaminhar normal, para preservar os cabeçalhos originais).
- **Verificar por outro canal** — se o e-mail parece vir do banco ou de um colega, confirmar por telefone ou app oficial, nunca pelo link do próprio e-mail suspeito.

## Checklist rápido para o técnico usar num chamado de "recebi um e-mail suspeito"

- [ ] Remetente real bate com o nome exibido?
- [ ] URL do link bate com o domínio oficial da empresa/serviço?
- [ ] Há pedido de senha, código ou dado financeiro?
- [ ] Há senso de urgência/ameaça incomum?
- [ ] O usuário já clicou em algo? Se sim → trocar senha da conta afetada e verificar login recente.

## Se o usuário já clicou

1. Desconectar o dispositivo da rede (evita propagação, se for malware).
2. Trocar a senha da conta comprometida imediatamente, de outro dispositivo.
3. Verificar histórico de login/atividades recentes da conta.
4. Escalar para o time de segurança/Nível 2 e abrir registro do incidente.

## Escalar para Nível 2 / Segurança se
- O usuário confirmou ter digitado credenciais no link falso.
- Há sinais de comportamento anômalo na conta (envio de e-mails que o usuário não fez, login de local desconhecido).
