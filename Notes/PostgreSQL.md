---
created-date: 2022-03-18
---

# PostgreSQL

Seguir as orientações de download e instalação: https://www.postgresql.org/download/linux/ubuntu/

Após instalado:

Ver os clusters ativos:
```
pg_lsclusters
```

Criar um cluster:
``` 
pg_createcluster -d /home/postgres/pastaCluster versaoPostgreSQL nomeCluster --start
```

---

``` 
su 
```
``` 
su - postgres 
```
``` 
psql 
```

## Configuração Postgresql

### postgresql.conf
Arquivo onde ficam definidas e armazenadas todas as configurações do servidor PostgreSQL
A view pg_settings, acessada por dentro do banco de dados, guarda todas as configurações atuais.

Localizaçãoa Padrão: dentro do diretório PGDATA definido no momento da inicialização do cluster.

No Ubuntu, se o postgreSQL foi instalado a partir do repositório oficial:
/etc/postgresql/versao/nomeDoCluster/postgrelsql.conf

### pg_hba.conf

Arquivo responsável pelo controle de autenticações de usuários no servidor PostgreSQL.

### pg_ident.conf

Arquivo responsável por mapear os usuários do sistema operacional com os usuários do banco de dados.
Localizado no diretório de dados PGDATA.

### Comandos Administrativos
#### Ubuntu:
Lista todos os clusters do PostgreSQL
``` 
pg_lsclusters
```
Cria um novo cluster porgreSQL
``` 
pg_createcluster <version> <cluster name>
```
Apaga um cluster PostgreSQL
``` 
pg_dropcluster <version> <cluster>
```
Start, Stop, Status, Restart cluster PostgreSQL
``` 
pg_ctlcluster <version> <cluster> <action>
```
Binários do PostgreSQL:

- createdb, createuser, dropdb, dropuser, initdb, pg_ctl, pg_basebackup, pg_dump / pg_dumpall, pg_restore, psql, reindexdb, vacuumdb

---

Cluster: Coleção de bancos de dados que compartilham as mesams configurações do PostgreSQL e do sistema operacional (port, listen_addresses, etc).

Banco de dados: Conjunto de schemas com seus objetos e relações.

Schemas: Conjunto de objetos/relações (tabelas, funções, views, etc).

---
### PGAdmin
#### Importante para conexão:
1. Liberar acesso ao cluster em postgresql.conf
2. Liberar acesso ao cluster para o usuário do banco de dados em pg_hba.conf
3. Criar/Editar usuários
OBS: NÃO COLOQUE '*' em "listem_address" no arquivo posgresql.conf em produção

Colocar senha:
```
su 
```

```
su - postgres
```

```
psql
```

```
ALTER USER postgres PASSWORD 'senha'; 
```

No arquivo postgrelsql.conf colote listen_address = *
No arquivo pg_hba.conf troque todos os method's peer por md5
pg_ctlcluster version nameCluster reload

