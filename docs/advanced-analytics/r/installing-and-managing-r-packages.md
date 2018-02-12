---
title: Pacotes R instalados com o SQL Server | Microsoft Docs
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 082aea3b1cde3c335dd7fa51b8ef219fc30f7efd
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="r-packages-installed-with-sql-server"></a>Pacotes R instalados com o SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve os pacotes de R que são instalados com o SQL Server, se você instalar e habilitar os recursos de aprendizado de máquina. Este artigo também descreve como gerenciar e exibir os pacotes existentes ou adicionar novos pacotes para uma instância do SQL Server.

**Aplica-se a:** serviços de aprendizado de máquina do SQL Server de 2017 (no banco de dados), SQL Server 2016 R Services (no banco de dados)

## <a name="what-is-the-instance-library-and-where-is-it"></a>O que é a biblioteca de instância e onde ele está?

Qualquer solução de R que é executado no SQL Server pode usar somente os pacotes que estão instalados na biblioteca R padrão associada à instância. Quando você instala os recursos de R no SQL Server, a biblioteca de pacote de R está localizada na pasta de instância.

+ Instância padrão *MSSQLSERVER* 

    SQL Server 2017: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` 
    
    SQL Server 2016: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`

+ Instância nomeada *MyNamedInstance* 

    SQL Server 2017: `C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` 
    
    SQL Server 2016: `C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library`

Você pode executar a instrução a seguir para verificar a biblioteca padrão para a instância atual do R.

```sql
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Alternatiely, você pode usar o novo [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) de função, se executar o sp\_executar\_externo\_script diretamente no computador de destino. A função não pode retornar os caminhos de biblioteca para conexões remotas.

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
```

> [!NOTE]
> Se você usar a associação para atualizar os componentes de R em uma instância, pode alterar o caminho para a biblioteca de instância. Certifique-se de verificar qual biblioteca está sendo usada pelo SQL Server.

## <a name="r-packages-installed-with-sql-server"></a>Pacotes R instalados com o SQL Server

Por padrão o R **base** pacotes estão instalados. Pacotes de base incluem a funcionalidade de núcleo fornecida por pacotes como `stats` e `utils`.

Instalação do R no SQL Server 2016 ou o SQL Server 2017 sempre inclui o **RevoScaleR** de pacote e pacotes aprimorados relacionados e provedores, que oferece suporte para contextos de computação remota, streaming, execução paralela de função rx, e muitos outros recursos. Para atualizar o pacote RevoScaleR, a usar a associação para atualizar apenas a componentes de aprendizado de máquina, patch ou atualize sua instância para uma versão mais recente do SQL Server.

+ Para obter uma visão geral dos recursos aprimorados de R, consulte [sobre o servidor de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/what-is-microsoft-r-server)

+ Para baixar as bibliotecas de RevoScaleR em um computador cliente, instale [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

## <a name="permissions-required-for-installing-r-packages"></a>Permissões necessárias para instalar pacotes de R

No SQL Server 2016, o administrador precisava instalar novos pacotes de R em toda a instância. 

SQL Server 2017 incorporou novos recursos para o pacote de instalação e gerenciamento:

+ Você pode usar comandos de R de um cliente remoto para instalar pacotes usando o escopo particular ou compartilhado. Este recurso requer o [Microsoft R Server](https://docs.microsoft.com/machine-learning-server/install/r-server-install) ou [Server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), bem como privilégios dbo na instância.
+ Novos recursos de banco de dados foram adicionados para dar suporte ao gerenciamento de pacotes por administradores de banco de dados sem o uso de T-SQL. No futuro, esses recursos oferecem DBAs com a capacidade de delegar a maioria das facetas do gerenciamento de pacote para usuários privilegiados.

Esta seção descreve as permissões necessárias para instalar e gerenciar pacotes por versão.

+ SQL Server 2016 R Services (no banco de dados)

    Para instalar um novo pacote de R em um computador que esteja executando [!INCLUDE [ssCurrent](..\..\includes\sscurrent-md.md)], você deve ter direitos administrativos no computador. É a tarefa do administrador de banco de dados ou outro administrador no servidor para garantir que todos os pacotes necessários estão instalados a [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] instância.

    Se você não tem privilégios administrativos no computador que hospeda o [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] instância, você pode fornecer as informações do administrador sobre como instalar pacotes de R e fornecer acesso a um repositório de pacote seguro onde pacotes solicitado por usuários podem ser obtidos.

+ Serviços de Machine Learning do SQL Server 2017

    Se você for um administrador na instância do SQL Server, você pode instalar novos pacotes conforme o desejado. Apenas certifique-se de usar a biblioteca padrão que é associada à instância. Pacotes instalados em outros locais não podem ser executado quando chamado a partir de um procedimento armazenado. Qualquer código de R que é executado usando o SQL Server como um contexto de computação também requer que os pacotes estejam disponíveis na biblioteca de instância.

    Esta versão também inclui alguns novos recursos que se destina a dar suporte ao gerenciamento de pacote mais fácil por DBAs em uma versão posterior. Por enquanto, recomendamos que você continue a instalar os pacotes de R em toda a instância.

+ R Server (Autônomo)

    Você precisa de direitos administrativos no computador para instalar novos pacotes de R.

+ Outros ambientes de cliente

    Se você estiver instalando um novo pacote de R em um computador que está sendo usado como uma estação de trabalho de R e o computador **não** tiver uma instância de [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] instalada, você ainda precisará de direitos administrativos no computador para Instale o pacote. Após a instalação do pacote, você pode executá-lo localmente.

## <a name="managing-or-viewing-installed-packages"></a>Gerenciar ou exibir os pacotes instalados

Há várias maneiras que você pode obter uma lista completa dos pacotes instalados no momento. Para obter mais informações, consulte [determinar quais pacotes estão instalados no SQL Server](determine-which-packages-are-installed-on-sql-server.md).
