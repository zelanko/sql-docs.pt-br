---
title: Configurar repositórios do Linux para SQL Server 2017 e 2019 | Microsoft Docs
description: Verifique e configure os repositórios de código-fonte para 2019 do SQL Server e SQL Server 2017 no Linux. O repositório de origem afeta a versão do SQL Server que é aplicada durante a instalação e atualização.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/14/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 5aee3ea6a744c15afce8055d153959b8db9ac66d
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46713208"
---
# <a name="configure-repositories-for-installing-and-upgrading-sql-server-on-linux"></a>Configurar repositórios para instalar e atualizar o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve como configurar o repositório correto para atualizações e instalações do SQL Server 2017 e 2019 do SQL Server no Linux.

> [!TIP]
> SQL Server 2019 CTP 2.0 já está disponível! Para testá-la, use este artigo para configurar o novo **mssql-server-visualização** repositório. Em seguida, instale usando as instruções na [guia de instalação](sql-server-linux-setup.md).

## <a id="repositories"></a>Repositórios

Quando você instala o SQL Server no Linux, você deve configurar um repositório da Microsoft. Esse repositório é usado para adquirir o pacote do mecanismo de banco de dados, **mssql-server**e relacionadas a pacotes do SQL Server. Atualmente, há três repositórios principais:

| Repositório | Nome | Description |
|---|---|---|
| **Visualização (2017)** | **mssql-server** | Repositório do SQL Server 2017 CTP e RC (Descontinuado). |
| **Visualização (2019)** | **MSSQL-server-visualização** | Repositório de 2019 CTP do SQL Server e o RC. |
| **CU** | **mssql-server-2017** | Repositório do SQL Server 2017 atualização cumulativa (CU). |
| **GDR** | **mssql-server-2017-gdr** | Repositório do SQL Server 2017 GDR somente para atualizações críticas. |

## <a id="cuversusgdr"></a> Atualização cumulativa versus GDR

É importante observar que há dois tipos principais de repositórios para cada distribuição:

- **Atualizações cumulativas (CU)**: repositório de atualização a cumulativa (CU) contém os pacotes para a versão base do SQL Server e correções de bug ou melhorias desde essa versão. As atualizações cumulativas são específicas para uma versão de lançamento, como o SQL Server 2017. Elas são lançadas em um ritmo regular.

- **GDR**: repositório o GDR contém pacotes para a versão base do SQL Server e apenas correções críticas e atualizações de segurança desde essa versão. Essas atualizações também são adicionadas para a próxima versão CU.

Cada versão de CU e GDR contém o pacote completo do SQL Server e todas as atualizações anteriores para esse repositório. Há suporte para a atualização de uma versão GDR para uma versão de CU, alterando seu repositório configurado para o SQL Server. Você também pode [fazer o downgrade](sql-server-linux-setup.md#rollback) para qualquer versão dentro de sua versão principal (ex: 2017).

> [!NOTE]
> Você pode atualizar de uma versão GDR para CU, alterando os repositórios de versão a qualquer momento. Atualizando de uma CU versão de lançamento de uma GDR não tem suporte. 

## <a id="configure"></a> Configurar um repositório

As seções a seguir descrevem como verificar e configurar um repositório para as seguintes plataformas com suporte:

- [Red Hat Enterprise Server](#rhel)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#sles)

## <a id="rhel"></a> Configurar repositórios RHEL
Use as etapas a seguir para configurar repositórios no Red Hat Enterprise Server (RHEL).

### <a name="check-for-previously-configured-repositories-rhel"></a>Verificar se há repositórios previamente configurados (RHEL)
Primeiro, verifique se você já tiver registrado um repositório do SQL Server.

1. Exibir os arquivos a **/etc/yum.repos.d** diretório com o seguinte comando:

   ```bash
   sudo ls /etc/yum.repos.d
   ```

2. Procure um arquivo que configura o diretório do SQL Server, tais como **mssql server.repo**.

3. Imprima o conteúdo do arquivo.

   ```bash
   sudo cat /etc/yum.repos.d/mssql-server.repo
   ```

4. O **nome** propriedade é o repositório configurado. Você pode identificá-lo com a tabela na [repositórios](#repositories) seção deste artigo.

### <a name="remove-old-repository-rhel"></a>Remover o repositório antigo (RHEL)
Se necessário, remova o repositório antigo com o comando a seguir.

```bash
sudo rm -rf /etc/yum.repos.d/mssql-server.repo
```

Esse comando presume que o arquivo identificado na seção anterior foi nomeado **mssql server.repo**.

### <a name="configure-new-repository-rhel"></a>Configurar o novo repositório (RHEL)
Configure o novo repositório a ser usado para atualizações e instalações do SQL Server. Use um dos comandos a seguir para configurar o repositório de sua escolha.

| Repositório | Versão | Comando |
|---|---|---|
| **Visualização (2019)** | 2019 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |

## <a id="sles"></a> Configurar repositórios SLES
Use as seguintes etapas para configurar os repositórios em SLES.

### <a name="check-for-previously-configured-repositories-sles"></a>Verificar se há repositórios previamente configurados (SLES)
Primeiro, verifique se você já tiver registrado um repositório do SQL Server.

1. Use **zypper informações** para obter informações sobre qualquer repositório configurado anteriormente.

   ```bash
   sudo zypper info mssql-server
   ```

2. O **repositório** propriedade é o repositório configurado. Você pode identificá-lo com a tabela na [repositórios](#repositories) seção deste artigo.

### <a name="remove-old-repository-sles"></a>Remover o repositório antigo (SLES)
Se necessário, remova o repositório antigo. Use um dos comandos a seguir com base no tipo de repositório configurado anteriormente.

| Repositório | Comando para remover |
|---|---|
| **Visualização (2017)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
| **Visualização (2019)** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-preview'` |
| **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
| **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|

### <a name="configure-new-repository-sles"></a>Configurar o novo repositório (SLES)
Configure o novo repositório a ser usado para atualizações e instalações do SQL Server. Use um dos comandos a seguir para configurar o repositório de sua escolha.

| Repositório | Versão | Comando |
|---|---|---|
| **Visualização (2019)** | 2019 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-preview.repo` |
| **CU** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
| **GDR** | 2017 | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |

## <a id="ubuntu"></a> Configurar repositórios do Ubuntu
Use as seguintes etapas para configurar os repositórios no Ubuntu.

### <a name="check-for-previously-configured-repositories-ubuntu"></a>Verificar se há repositórios configurados anteriormente (Ubuntu)
Primeiro, verifique se você já tiver registrado um repositório do SQL Server.

1. Exibir o conteúdo a **/etc/apt/sources.list** arquivo.

   ```bash
   sudo cat /etc/apt/sources.list
   ```

2. Examine a URL do pacote para o mssql-server. Você pode identificá-lo com a tabela na [repositórios](#repositories) seção deste artigo.

### <a name="remove-old-repository-ubuntu"></a>Remover o repositório antigo (Ubuntu)
Se necessário, remova o repositório antigo. Use um dos comandos a seguir com base no tipo de repositório configurado anteriormente.

| Repositório | Comando para remover |
|---|---|
| **Visualização (2017)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |
| **Visualização (2019)** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview xenial main'` |
| **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
| **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

### <a name="configure-new-repository-ubuntu"></a>Configurar o novo repositório (Ubuntu)
Configure o novo repositório a ser usado para atualizações e instalações do SQL Server.

1. Importe as chaves GPG repositório público.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

2. Use um dos comandos a seguir para configurar o repositório de sua escolha.

   | Repositório | Versão | Comando |
   |---|---|---|
   | **Visualização (2019)** | 2019 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-preview.list)"` |
   | **CU** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"` |
   | **GDR** | 2017 | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)"` |

3. Execute **apt-get atualização**.

   ```bash
   sudo apt-get update
   ```

## <a name="next-steps"></a>Próximas etapas

Depois de configurar o repositório correto, você poderá [instale](sql-server-linux-setup.md#platforms) ou [atualizar](sql-server-linux-setup.md#upgrade) do SQL Server e qualquer relacionadas a pacotes do novo repositório.

> [!IMPORTANT]
> Neste ponto, se você optar por usar um dos artigos a instalação, como o [guias de início rápido](sql-server-linux-setup.md#platforms), lembre-se de que você já configurou o repositório de destino. Não repita essa etapa nos tutoriais. Isso é especialmente verdadeiro se você configurar o repositório GDR, porque os inícios rápidos usam o repositório do CU.

Para obter mais informações sobre como instalar o SQL Server 2017 no Linux, consulte [orientação de instalação do SQL Server no Linux](sql-server-linux-setup.md).