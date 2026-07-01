# SOC141 - Phishing URL Detected - Lets Defend
## Alerta

<p align="center">
<img src="./assets/SOC141_01-alert.png" alt="Alerta no painel de monitoramento" width="100%">
</p>

## Ações
#### Verificação da url no Virus Total
https://www.virustotal.com/gui/url/d0da32cbd01eba6a19108c1255cb28411fcd6ded0c42da22ad4f412d8d31112a

<p align="center">
<img src="./assets/SOC141_02-virus-total-analysis.png" alt="Resultado da análise no Virus Total" width="100%">
</p>

#### Verificação da url no urlscan
https://urlscan.io/result/019f19cd-2bff-7308-8d69-b0ca3f0d1b49/

<p align="center">
<img src="./assets/SOC141_03-url-scan-analysis.png" alt="Resultado da análise no URL Scan" width="100%">
</p>

## Conclusões
A url em questão não está mais online, de qualquer forma, houve uma solicitação HTTP para o endereço passando um endereço de email.

<p align="center">
<img src="./assets/SOC141_04-access-logs.png" alt="Logs de eventos" width="100%">
</p>

<p align="center">
<img src="./assets/SOC141_05-request-logs.png" alt="Log da requisição" width="100%">
</p>

Analisando os logs, podemos confirmar que essa solicitação foi bem sucedida. Logo a tentativa de phishing ocorreu e precisamos conter a máquina.

<p align="center">
<img src="./assets/SOC141_06-endpoint-containment.png" alt="Contenção do EndPoint" width="100%">
</p>

## Playbook
1 - Link malicioso

2 - Requisição efetuada com sucesso (Conteúdo acessado)

3 - Alerta verdadeiro positivo