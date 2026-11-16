# Simulando-um-Brute-Force-Attack-com-Kali-Linux-e-Metasploitable-2-

Aqui irei detalhar minha primeira experiência simulando um ataque Brute Force usando as máquinas virtuais Kali Linux e Metasploitable 2

Brute Force Attack — Kali Linux & Metasploitable 2

Sobre o projeto

Este projeto tem como objetivo demonstrar, em um ambiente controlado de laboratório, como funciona um ataque de força bruta (Brute Force Attack) contra os serviços FTP, Web e SMB.

O experimento foi realizado utilizando o Kali Linux como máquina atacante e o Metasploitable 2 como máquina de destino.

A ferramenta utilizada para executar o teste foi o Medusa, permitindo testar diferentes combinações de usuários e senhas.

Objetivos

- Compreender o funcionamento de um ataque de força bruta.
- Aprender a utilizar o Medusa para auditoria de autenticação.
- Identificar serviços ativos em uma máquina vulnerável.
- Analisar os riscos de senhas fracas.
- Compreender a importância de medidas de proteção contra ataques de autenticação.

Ferramentas utilizadas

Ferramenta| Função
Kali Linux| Sistema operacional da máquina atacante
Metasploitable 2| Máquina virtual vulnerável utilizada como alvo
Medusa| Ferramenta de auditoria de autenticação
Nmap| Identificação de portas e serviços
Terminal Linux| Execução dos comandos

🖥️ Ambiente de laboratório

O experimento foi realizado utilizando duas máquinas virtuais:

Máquina atacante:

- Sistema operacional: Kali Linux.
- Função: Executar os testes de segurança.

Máquina de destino:

- Sistema operacional: Metasploitable 2.
- Serviços analisados: FTP, Web, SMB.
- Porta padrão: 22/TCP.

As máquinas devem estar conectadas a uma rede virtual isolada, sem exposição à internet ou a sistemas de terceiros.

1. Identificação do endereço IP

Primeiramente, foi identificado o endereço IP da máquina Metasploitable 2.

No Kali Linux, foi utilizado o comando:

ip a

Na máquina Metasploitable 2 foi utilizado o comando:

ifconfig

O endereço IP identificado para o alvo foi:

"192.168.56.102"

2. Identificação dos serviços

Com o endereço IP do alvo identificado, foi realizada uma verificação utilizando o Nmap:

nmap -sV -p 21,22,80,445,139 192.168.56.102

O objetivo foi identificar se as portas estavam abertas e verificar a versão do serviço FTP.

3. Preparação da lista de usuários e senhas

Foi realizada a criação de uma lista de usuários e de senhas para que os testes fossem realizados:

Comandos usados para criar as listas:

echo -e "user\nmsfadmin\nadmin\nroot" > users.txt

echo -e "123456\npassword\nqwerty\nmsfadmin" > pass.txt

4. Execução do teste de força bruta

Nessa etapa foi utilizado o comando:
medusa -h 192.168.56.102 -U users.txt -P pass.txt -M ftp -t 6

Explicação dos parâmetros:

medusa: inicia a ferramenta.
-h: define o endereço IP do alvo.
192.168.56.101: endereço IP da máquina de destino.
-U users.txt: informa o arquivo contendo os usuários.
-P senhas.txt: informa o arquivo contendo as senhas.
-M ftp: específica o módulo atacado.
-t 6: indica a quantidade de treads simultâneos

5. Resultados obtidos

O comando foi executado mostrando todas as tentativas de achar o usuário e a senha que ele utiliza, que nesse caso foi o usuário "msfadmin" com a senha "msfadmin".

Informações importantes:

Até o usuário ser encontrado foram realizados 5 testes, sendo o quinto, o usuário.

O teste levou cerca de 2 segundos para ser completo.

6. Análise de segurança

O experimento demonstra como senhas fracas podem comprometer a segurança de serviços que utilizam autenticação por usuário e senha. Como nesse caso o usuário usou seu próprio nome como senha.

Ataques de força bruta podem ser utilizados para testar diversas combinações de credenciais até encontrar uma combinação válida.

Algumas medidas de proteção incluem:

Utilização de senhas fortes e exclusivas.
Limitação de tentativas de autenticação.
Autenticação de múltiplos fatores.

7. Ataques em Formulários de Login Web 
   
Nessa etapa foi utilizado o recurso do DVWA (Damn Vulnerable Web Application). Esse recurso simula uma sessão de login genérica com "username" e "password". Ao precionar a tecla F12(no caso desse teste) pode-se ser acessado a aba de programador que vai mostrar na sessão de Requests que o login que foi testado deu como errado: user "joao" password "456". Porém todos os parâmetros estão disponíveis para serem vistos "username", "password" e "Login". Esse processo infelizmente não foi possível de se finalizar pois o comando exigia um carácter que o teclado não conseguia digitar por ele ficar com as teclas "trocadas" ao entrar na VM.

9. Ataques a SMB
    

10.Conclusão

A realização deste laboratório permitiu compreender, na prática, o funcionamento de um ataque de força bruta e a utilização do Medusa para testar a segurança dos serviços FTP, WEB, SMB.

Também foi possível observar a importância de políticas adequadas de autenticação e da utilização de senhas fortes.

O experimento contribuiu para o aprendizado de conceitos relacionados à segurança da informação, redes de computadores e testes de invasão (Pentest).

---

⚠️ Aviso legal

Este projeto possui finalidade exclusivamente educacional.

Todos os testes foram realizados em um ambiente virtual controlado, utilizando uma máquina intencionalmente vulnerável.

Não utilize estas técnicas contra sistemas, redes ou serviços sem autorização explícita de seus responsáveis.
