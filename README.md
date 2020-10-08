<h1 align="center">
  <br>
    <img src="media/Files-permissions-and-ownership-basics-in-Linux.png" alt="logo" width="500">
  <br><br>
Linux Files Permissions Guide
  <br>
  <br>
</h1>

<h4 align="center">By Jose Amat - jose.alc.luis@gmail.com</h4>

<h2>Summary</h2>

- [1. Estrutura de arquivos](#1-estrutura-de-arquivos)
  - [1.1. Bloco de Permissões](#11-bloco-de-permissões)
    - [1.1.1. Tipo de arquivos](#111-tipo-de-arquivos)
    - [1.1.2. Permissões](#112-permissões)
- [2. Alterar permissões](#2-alterar-permissões)
  - [2.1. Comando chmod](#21-comando-chmod)
    - [2.1.1. Modo textual](#211-modo-textual)
      - [2.1.1.1. Sintaxe:](#2111-sintaxe)
      - [2.1.1.2. Exemplo:](#2112-exemplo)
    - [2.1.2. Modo octal](#212-modo-octal)
      - [2.1.2.1. Sintaxe:](#2121-sintaxe)
      - [2.1.2.2. Exemplo:](#2122-exemplo)
- [3. Alterar proprietário](#3-alterar-proprietário)
  - [3.1. Comando chown (change owner)](#31-comando-chown-change-owner)
    - [3.1.1. Sintaxe](#311-sintaxe)
    - [3.1.2. Exemplo](#312-exemplo)
- [4. Alterar grupo](#4-alterar-grupo)
  - [4.1. Comando chgrp (change group)](#41-comando-chgrp-change-group)
    - [4.1.1. Sintaxe](#411-sintaxe)
    - [4.1.2. Exemplo](#412-exemplo)

# 1. Estrutura de arquivos
```bash
$ ls -l
drwxr-xr-x  2 joamat joamat 4096 Sep  4 18:24 'Área de Trabalho'
drwxr-xr-x 21 joamat joamat 4096 Oct  5 13:30  Documents
drwxr-xr-x  9 joamat joamat 4096 Oct  7 11:43  Downloads
drwxr-xr-x  2 joamat joamat 4096 Oct  6 17:31  Imagens
drwxr-xr-x  2 joamat joamat 4096 Jul  8 13:38  Modelos
drwxr-xr-x  2 joamat joamat 4096 Jul  8 13:38  Música
drwxr-xr-x  2 joamat joamat 4096 Jul 31 11:02  Pictures
drwxr-xr-x  2 joamat joamat 4096 Jul  8 13:38  Público
drwxr-xr-x  6 joamat joamat 4096 Jul 11 03:06  snap
drwxr-xr-x  2 joamat joamat 4096 Sep 28 18:35  Vídeos
```

| Permissões | Links | Proprietários | Grupo | Tamanho | Data e hora | Nome |
| - | - | - | - | - | - | - |
| drwxr-xr-x | 21 | joamat | joamat | 4096 | Oct  5 13:30 | Documents |

## 1.1. Bloco de Permissões

| Tipo de arquivo | Proprietário | Grupo | Outros |
| :-: | :-: | :-: | :-: |
| d | rwx | r-x | r-x |

### 1.1.1. Tipo de arquivos

| Nome | Descrição |
| - | - |
| `d` | diretório |
| `-` | arquivo comum de usuário |
| `c` | arquivo de caractere |
| `b` | arquivo de bloco |
| `l` | link |

### 1.1.2. Permissões

| Nome | Descrição |
| - | - |
| `r` | read (leitura) |
| `w` | write (escrita) |
| `x` | execution (execução) |
| `-` | no permission (sem permissão) |

# 2. Alterar permissões

## 2.1. Comando chmod
Altera as permissões de acesso a arquivos e diretórios

### 2.1.1. Modo textual

#### 2.1.1.1. Sintaxe:

```bash
$ chmod u=[perm_text],g=[perm_text],o=[perm_text]  [arquivo ou diretório]
```


#### 2.1.1.2. Exemplo:

Dar permissões `rwxr-xr-x` para o arquivo **test.txt**:

| Permissão | Separação | Permissão textual |
| :- | :-: | :-: |
| rwxr-xr-x | (rwx)(r-x)(r-x) | `u=rwx,g=rx,o=rx` |

```bash
$ ls -l test.txt
-rw-rw-r-- 1 joamat joamat 0 Oct  8 13:27 test.txt

$ chmod u=rwx,g=rx,o=rx test.txt
$ ls -l test.txt
-rwxr-xr-x 1 joamat joamat 0 Oct  8 13:27 test.txt
```

`Nota: Você pode usar + ou - para adicionar ou extrair alguma permissão, respectivamente.`



### 2.1.2. Modo octal

#### 2.1.2.1. Sintaxe:

```bash
$ chmod [permissões] [arquivo ou diretório]
```
| Valor textual | Valor binário | Valor octal | Descrição |
| :- | :-: | :-: | -: |
| r-- | 100 | `4` | read |
| -w- | 010 | `2` | write |
| --x | 001 | `1` | execution |
| --- | 000 | `0` | no permission |


#### 2.1.2.2. Exemplo:

Dar permissões `rwxr-xr-x` para o arquivo **test.txt**:


| Permissão textual | Separação textual | Separação octual | Permisão octual |
| :- | :-: | :-: | :-: |
| rwxr-xr-x | (rwx) (r-x) (r-x) | (4+2+1) (4+0+1) (4+0+1) | `755` |

```bash
$ chmod 755 test.txt
$ ls -l
drwxr-xr-x  2 joamat joamat 4096 Sep  4 18:24 'Área de Trabalho'
drwxr-xr-x 21 joamat joamat 4096 Oct  5 13:30  Documents
drwxr-xr-x  9 joamat joamat 4096 Oct  7 11:43  Downloads
drwxr-xr-x  2 joamat joamat 4096 Oct  6 17:31  Imagens
drwxr-xr-x  2 joamat joamat 4096 Jul  8 13:38  Modelos
drwxr-xr-x  2 joamat joamat 4096 Jul  8 13:38  Música
drwxr-xr-x  2 joamat joamat 4096 Jul 31 11:02  Pictures
drwxr-xr-x  2 joamat joamat 4096 Jul  8 13:38  Público
drwxr-xr-x  6 joamat joamat 4096 Jul 11 03:06  snap
-rwxr-xr-x  1 joamat joamat    0 Oct  8 11:03  test.txt
drwxr-xr-x  2 joamat joamat 4096 Sep 28 18:35  Vídeos
```

# 3. Alterar proprietário
## 3.1. Comando chown (change owner)
Altera o proprietário de um arquivo ou diretório

### 3.1.1. Sintaxe
```bash
$ chown [novo_proprietário] [arquivo_ou_diretório]
```

### 3.1.2. Exemplo

Alterar proprietário do arquivo `test.txt` de **joamat** para **root**

```bash
$ ls -l test.txt 
-rw-rw-r-- 1 joamat joamat 0 Oct  8 11:42 test.txt

$ sudo chown root test.txt

$ ls -l test.txt
-rw-rw-r-- 1 root joamat 0 Oct  8 11:42 test.txt
```

# 4. Alterar grupo
## 4.1. Comando chgrp (change group)
Altera o grupo de um arquivo ou diretório

### 4.1.1. Sintaxe
```bash
$ chgrp [novo_grupo] [arquivo_ou_diretório]
```

### 4.1.2. Exemplo

Alterar grupo do arquivo `test.txt` de **joamat** para **root**

```bash
$ ls -l test.txt 
-rw-rw-r-- 1 root joamat 0 Oct  8 11:31 test.txt

$ sudo chgrp root test.txt

$ ls -l test.txt
-rw-rw-r-- 1 root root 6 Oct  8 11:39 test.txt
```

