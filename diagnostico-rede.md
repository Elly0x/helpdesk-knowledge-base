# Diagnóstico: computador sem acesso à rede/internet

**Categoria:** Incidente Nível 1
**Tempo médio de resolução:** 5-15 min
**Ferramentas:** Prompt de Comando (cmd)

## Sintoma relatado pelo usuário
- "A internet não funciona no meu computador."
- "Não abre nenhum site, mas no celular funciona."
- "Perdi acesso à rede do escritório do nada."

## Fluxo de diagnóstico (nessa ordem)

### 1. Verificar se o computador tem um IP válido
```
ipconfig /all
```
Observe o **Endereço IPv4**:
- `169.254.x.x` → o computador não conseguiu IP do DHCP. Problema de cabo, Wi-Fi ou switch/roteador.
- IP normal (ex: `192.168.1.45`) mas sem internet → provavelmente problema de DNS ou gateway.
- "Media disconnected" → cabo de rede desconectado ou porta com defeito.

### 2. Testar conectividade local (gateway)
```
ping 192.168.1.1
```
(substitua pelo IP do "Default Gateway" que apareceu no `ipconfig`)
- Responde → a rede local está OK, o problema é além do roteador.
- Não responde → problema no cabo, switch, Wi-Fi ou placa de rede do próprio PC.

### 3. Testar conectividade externa
```
ping 8.8.8.8
```
- Responde → internet física está OK, problema é de DNS.
- Não responde → problema de rede/provedor, não é só o PC do usuário.

### 4. Testar resolução de nomes (DNS)
```
nslookup google.com
```
- Se o `ping 8.8.8.8` funciona mas `nslookup` falha → problema de DNS. Corrija o servidor DNS nas propriedades do adaptador (ou use `8.8.8.8` / `1.1.1.1` temporariamente).

### 5. Rastrear o caminho até a falha
```
tracert google.com
```
Mostra em qual "salto" (hop) a conexão para de responder — útil para saber se o problema é local, no roteador da empresa, ou no provedor.

## Tabela resumo

| Comando | O que testa | Se falhar, suspeite de |
|---|---|---|
| `ipconfig /all` | Configuração de IP local | DHCP, cabo, placa de rede |
| `ping <gateway>` | Rede local | Cabo, switch, Wi-Fi |
| `ping 8.8.8.8` | Internet (sem depender de DNS) | Link do provedor, firewall |
| `nslookup <site>` | Resolução de nomes (DNS) | Servidor DNS configurado |
| `tracert <site>` | Caminho completo até o destino | Identificar em que ponto a rede falha |

## Soluções rápidas mais comuns
1. `ipconfig /release` seguido de `ipconfig /renew` — força renovar o IP.
2. `ipconfig /flushdns` — limpa cache de DNS corrompido.
3. Reiniciar o adaptador de rede pelo Painel de Controle.
4. Testar outro cabo/porta antes de escalar (elimina hardware como causa).

## Escalar para Nível 2 se
- Vários usuários do mesmo setor reportam o mesmo problema ao mesmo tempo (indica switch/roteador, não o PC individual).
- `tracert` mostra que a falha acontece fora da rede interna (fora do controle do time de suporte local).
