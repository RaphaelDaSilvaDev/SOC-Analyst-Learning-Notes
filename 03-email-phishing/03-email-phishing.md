# Introdução ao Email Phishing
## O que é o Email Phishing
O Phishing é a principal técnica de Acesso Inicial do MITRE ATT&CK. Aqui, o atacante procura manipular o elo mais fraco através de engenharia social para obter informações pessoais do usuário, fazendo com que ele execute uma ação (Seja digitar credenciais em uma página falsa ou abrir um anexo malicioso).

Uma forma de fazer com que o usuário caia nessa armadilha, é enviando emails com senso de urgência ou valor.
- Urgência: Devido a recentes ataques Hackers, precisamos que altere sua senha junto ao banco $, com nossa nova política, você tem 30 dias para redefinir sua senha, após esse período sua conta será bloqueada para evitar possíveis ataques. Clique no link abaixo para redefinir sua senha.
- Valor: Você ganhou 50% de desconto em um pacote de viagem pela Viage+. Clique no link abaixo para escolher seu destino.

Uma vez que o usuário acessa o site malisioso e adiciona as credenciais, as mesmas são roubadas pelos atacantes. Se o usuário abrir um anexo dentro de um email de phishing, esse anexo pode adicionar um keylogger, onde envia todas as entradas do teclado do usuário para o atacante.

O atacante usa esses ataques como primeiro passo para infiltrar em sistemas.

## Coleta de Informações
Emails não tem necessariamente um mecanismo de autenticação, com isso os atacantes podem enviar emails em nome de outra pessoa, isso pode ser feito usando a técnica spoofing.

Os protocolos SPF, DKIM e DMARC foram criados para evitar essa técnica, eles podem ser usado para determinar se o endereço do remetente é falso ou real. Alguns programas de email verificam isso automaticamente. Porém, o uso desses protocolos não é obrigatório, podendo causar problemas em alguns casos.

Grandes instituições usam seus próprios servidores de email, e terão seus próprios IPs, contudo, não podemos dizer que um email de um remetente não falsificado é seguro. Emails podem ser enviados em nome de terceiros, hackeando os endereços de emails corporativos ou pessoais.

É de extrema importância analisar o cabeçalho do email, nele é possível ver informações como remetente, destinatário, responder para, etc.

| Campos Importantes | Descrição |
| -- | -- |
| From (De) | Mostra o nome e endereço de email do remetente. |
| To (Para) | Mostra o nome e endereço de email do destinatário, bem como CC e BCC. |
| Date (Data) | Informa a data em que o email foi enviado. |
| Subject (Assunto) | É o tema do email, resume o conteúdo de todo o corpo. |
| Return-Path / Reply-To (Responder Para) | É o endereço de email usado para enviar a resposta do email. |
| Received (Recebido) | Mostra o caminho que o email fez até chegar no destinatário, para cada servidor que o email passou, adiciona um Received: from ... A leitura é de baixo para cima, sendo o último o ponto de partida, de onde o email saiu.|
| Message-ID (Id da mensagem) | Um identificador único global gerado pelo servidor de envio. |

## Análise Estática
Aqui devemos analisar as propriedades do email, validando o cabeçalho, pegando links, hash de arquivos e jogar em ferramentas de Threat Intel como VirusTotal ou Talos Intelligence para verificar se há algo suspeito.

## Análise Dinâmica
Caso a análise estática não seja conclusiva, ou seja, o hash do arquivo, ou o link no email não consta como malicioso nas ferramenteas de Threat Intel mas parecem suspeitos, devemos abrir executar os links e arquivos, para isso usamos um ambiente sandbox. Não devemos executar isso em nossa máquina principal, sempre devemos usar um sandbox para fazer essa análise como Anu.Run, Joe Sandbox ou Hybrid Analysis.

Nesse ambiente sandbox, é possível ver os processos, conexões com rede, alterações de registros, etc. Dessa forma podemos validar se o arquivo de fato é malicioso ou não.

Vale lembrar que alguns malwares não são executados ao executar um arquivo, ele pode "dormir" por um tempo para não chamar atenção e depois de um tempo "acordar" e fazer seu estrago.

## Técnicas Adicionais
Os atacantes estão constantemente evoluindo para burlar os filtros de spam. Devemos ficar atentos a estas técnicas comuns:

- Phishing baseado em anexos HTML: O atacante envia um arquivo html em anexo, ao clicar o arquivo abre localmente em uma tela de login idêntica a de um site real, como um banco. Como a página roda localmente, os filtros de segurança de rede baseados em reputação de URL não conseguem bloquear, mas ao fazer um submit, as informações são enviadas ao atacante.

- Uso de Serviços legítimos: Hospedar páginas de phishing dentro de serviços confiáveis como Google Forms, Microsoft SharePoint ou AWS S3. Como o domínio é leítimo, o filtro de email deixa passar.

- QR Code: O corpo do email contém um QR Code, pedindo autenticação em multifator por exemplo. Isso joga o ataque para fora do monitoramento das ferramentas corporativas do computador.

## Ferramentas Essenciais
- PhishTool: Excelente ferramenta focada especificamente em destrinchar os arquivos .eml ou .msg, organizando o cabeçalho de forma visual e trazendo os dados de reputação do IP de origem automaticamente.

- CyberChef: Usado para fazer conversões como XOR, Base64, HexaDecimal, etc.

- URLscan.io: Perfeito para análise estática, você joga a URL suspeita e o serviço abre o site em um servidor próprio, tira um print da tela para você ver o design sem precisar acessar o link, além de listar todas as conexões de terceiros que aquela página faz.

## Referências
* https://app.letsdefend.io/path/soc-analyst-learning-path
* https://attack.mitre.org/techniques/T1566/
* https://www.malwarebytes.com/pt-br/cybersecurity/basics/phishing-email
* https://www.kaspersky.com.br/resource-center/threats/phishing-email
---

Criado em 25/06/2026

Atualizado em 25/06/2026