---
title: Configurar o compartilhamento de pasta instantâneo de replicação do SQL Server no Linux
description: Este artigo descreve como configurar a replicação de SQL Server de compartilhamentos de pasta de instantâneo no Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2513511889c4bc22757f0970269fa9ee7b51857d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093126"
---
# <a name="configure-replication-snapshot-folder-with-shares"></a>Configurar a pasta de instantâneo de replicação com compartilhamentos

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

A pasta de instantâneo é um diretório que você designou como um compartilhamento de; os agentes que leem e gravam nessa pasta devem ter permissões suficientes para acessá-lo.

![diagrama de replicação][1]

### <a name="replication-snapshot-folder-share-explained"></a>Compartilhamento de pasta de instantâneo de replicação explicado

Antes dos exemplos, vamos examinar como o SQL Server usa compartilhamentos samba na replicação. Abaixo está um exemplo básico de como isso funciona.

1. Compartilhamentos Samba estão configurados que arquivos gravados `/local/path1` da replicação no publicador, os agentes podem ser vistos por assinante
2. SQL Server está configurado para usar caminhos de compartilhamento ao configurar o publicador no servidor de distribuição, de modo que todas as instâncias teria esta aparência o `//share/path`
3. SQL Server localiza o caminho local do `//share/path` saber onde procurar os arquivos
4. Leituras e gravações do SQL Server para caminhos locais apoiado por um compartilhamento do samba


## <a name="configure-a-samba-share-for-the-snapshot-folder"></a>Configurar um compartilhamento do samba para a pasta de instantâneo 

Agentes de replicação serão necessário um diretório compartilhado entre os hosts de replicação para acessar pastas de instantâneo em outros computadores. Por exemplo, na replicação transacional de recepção, o agente de distribuição reside no assinante, o que requer acesso ao distribuidor para obter artigos. Nesta seção, vamos examinar um exemplo de como configurar um compartilhamento do samba em dois hosts de replicação.


## <a name="steps"></a>Etapas

Por exemplo, configuraremos uma pasta de instantâneo no Host 1 (distribuidor) para ser compartilhado com o Host 2 (assinante) usando o Samba. 

### <a name="install-and-start-samba-on-both-machines"></a>Instalar e iniciar o Samba nos dois computadores 

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

### <a name="on-host-1-distributor-set-up-the-samba-share"></a>Na configuração do Host 1 (distribuidor) o compartilhamento do Samba 

1. Usuário de configuração e a senha do samba:

  ```bash
  sudo smbpasswd -a mssql 
  ```

1. Editar o `/etc/samba/smb.conf` para incluir a seguinte entrada e preencha o *nome_do_compartilhamento* e *caminho* campos
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

### <a name="on-host-2-subscriber--mount-the-samba-share"></a>No Host 2 (assinante) montar o compartilhamento do Samba

Edite o comando com os caminhos corretos e execute o seguinte comando em machine2:

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

### <a name="on-both-hosts--configure-sql-server-on-linux-instances-to-use-snapshot-share"></a>Em ambos os Hosts de configurar o SQL Server em instâncias do Linux para usar o compartilhamento de instantâneos

Adicione a seguinte seção para `mssql.conf` nos dois computadores. Usar onde quer que o compartilhamento do samba para o / / / caminho do compartilhamento. Neste exemplo, seria `//host1/mssql_data`

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

### <a name="configuring-publisher-with-shared-paths"></a>Publicador é configurado com caminhos de compartilhado

* Ao configurar a replicação, use o caminho de compartilhamentos (exemplo `//host1/mssql_data`
* Mapa `//host1/mssql_data` para um diretório local e o mapeamento adicionado ao `mssql.conf`.

## <a name="next-steps"></a>Próximas etapas

[Conceitos: Replicação do SQL Server no Linux](sql-server-linux-replication.md)

[Procedimentos armazenados de replicação](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

[1]: ./media/sql-server-linux-replication-snapshot-shares/image1.png
