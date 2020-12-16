---
title: Configurar compartilhamentos de pasta de instantâneos
titleSuffix: SQL Server on Linux
description: Saiba como configurar a replicação de compartilhamentos de pasta de instantâneos do SQL Server em Linux.
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: 1e0ace10e1a976128146b82d77660d1edc06040a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471487"
---
# <a name="configure-replication-snapshot-folder-with-shares"></a>Configurar a pasta de instantâneo de replicação com compartilhamentos

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

A pasta de instantâneo é um diretório que você designou como um compartilhamento, agentes que leem essa pasta e gravam nela devem ter permissões suficientes para acessá-la.

![diagrama de replicação][1]

### <a name="replication-snapshot-folder-share-explained"></a>Compartilhamento da pasta de instantâneo de replicação explicado

Antes dos exemplos, vamos examinar como o SQL Server usa os compartilhamentos do Samba na replicação. Veja abaixo um exemplo básico de como isso funciona.

1. Os compartilhamentos do Samba são configurados para que os arquivos gravados em `/local/path1` pelos agentes de replicação no publicador possam ser vistos pelo assinante
2. O SQL Server está configurado para usar caminhos de compartilhamento ao configurar o publicador no servidor de distribuição, de modo que todas as instâncias examinariam o `//share/path`
3. O SQL Server encontra o caminho local do `//share/path` para saber onde procurar os arquivos
4. Leituras/gravações do SQL Server para caminhos locais apoiados por um compartilhamento do Samba


## <a name="configure-a-samba-share-for-the-snapshot-folder"></a>Configurar um compartilhamento do Samba para a pasta de instantâneos 

Os agentes de replicação precisarão de um diretório compartilhado entre hosts de replicação para acessar pastas de instantâneo em outros computadores. Por exemplo, na replicação de pull transacional, o agente de distribuição reside no assinante, que requer acesso ao distribuidor para obter artigos. Nesta seção, examinaremos um exemplo de como configurar um compartilhamento do Samba em dois hosts de replicação.


## <a name="steps"></a>Etapas

Como exemplo, configuraremos uma pasta de instantâneo no Host 1 (o distribuidor) para ser compartilhada com o Host 2 (o assinante) usando o Samba. 

### <a name="install-and-start-samba-on-both-machines"></a>Instalar e iniciar o Samba em ambos os computadores 

No Ubuntu:

```bash
sudo apt-get -y install samba
sudo service smbd restart
```

No RHEL:

```bash
sudo yum install samba
sudo service smb start
sudo service smb status
```

### <a name="on-host-1-distributor-set-up-the-samba-share"></a>No Host 1 (distribuidor), configurar o compartilhamento do Samba 

1. Configurar usuário e a senha para o Samba:

  ```bash
  sudo smbpasswd -a mssql 
  ```

1. Edite `/etc/samba/smb.conf` o para incluir a seguinte entrada e preencha os campos *share_name* e *path*
 ```bash
  <[share_name]>
  path = </local/path/on/host/1>
  writable = yes
  create mask = 770
  directory mask 
  valid users = mssql 
  ```

  **Exemplo**

  ```bash
  [mssql_data]    <- Name of the shared directory
  path = /var/opt/mssql/repldata <- location of directory we wish to share
  writable = yes  <- determines if the share is writable from other hosts
  create mask = 770  <- Linux permissions for files created 
  directory mask = 770 <- Linux permissions for directories created
  valid users = mssql   <- list of users who can login to this share
  ```

### <a name="on-host-2-subscriber--mount-the-samba-share"></a>No Host 2 (assinante), montar o compartilhamento do samba

Edite o comando com os caminhos corretos e execute o seguinte comando no computador2:

  ```bash
  sudo mount //<name_of_host_1>/<share_name> </local/path/on/host/2> -o user=mssql,uid=mssql,gid=mssql
  ```

  **Exemplo**

  ```bash
  mount //host1/mssql_data /var/opt/mssql/repldata_shared -o user=mssql,uid=mssql,gid=mssql

  user=mssql <- sets the login name for samba
  uid=mssql   <- makes the mssql user as the owner of the mounted directory
  gid=mssql   <- sets the mssql group as the owner of the mounted directory
  ```

### <a name="on-both-hosts--configure-sql-server-on-linux-instances-to-use-snapshot-share"></a>Nos dois hosts, configure instâncias do SQL Server em Linux para usar o compartilhamento de instantâneos

Adicione a seção a seguir a `mssql.conf` em ambos os computadores. Use o compartilhamento do Samba onde quer que ele esteja para o //share/path. Neste exemplo, isso seria `//host1/mssql_data`

  ```bash
  [uncmapping]
  //share/path = /local/path/on/hosts/
  ```

  **Exemplo**

  No host1:

  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/1
  ```

  No host2:
  
  ```bash
  [uncmapping]
  //host1/mssql_data = /local/path/on/hosts/2
  ```

### <a name="configuring-publisher-with-shared-paths"></a>Configurar o Publicador com caminhos compartilhados

* Ao configurar a replicação, use o caminho de compartilhamentos (exemplo `//host1/mssql_data`
* Mapeie `//host1/mssql_data` para um diretório local e o mapeamento adicionado a `mssql.conf`.

## <a name="next-steps"></a>Próximas etapas

[Conceitos: Replicação do SQL Server em Linux](sql-server-linux-replication.md)

[Procedimentos armazenados de replicação](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

[1]: ./media/sql-server-linux-replication-snapshot-shares/image1.png
