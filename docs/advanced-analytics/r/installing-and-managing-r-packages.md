---
title: Pacotes R instalados com o SQL Server | Microsoft Docs
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 4d426cf6-a658-4d9d-bfca-4cdfc8f1567f
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 41fb66e7b2155b75d05ce9eab8dc0df3782e4030
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="r-packages-installed-with-sql-server"></a>Pacotes R instalados com o SQL Server

Este artigo descreve os pacotes de R que são instalados com o SQL Server e fornece informações sobre como gerenciar e exibir os pacotes existentes.

Este artigo também fornece links para informações sobre como adicionar novos pacotes para uso com o SQL Server.

**Aplica-se a:** serviços de aprendizado de máquina do SQL Server de 2017 (no banco de dados), SQL Server 2016 R Services (no banco de dados)

## <a name="what-is-the-instance-library-and-where-is-it"></a>O que é a biblioteca de instância e onde ele está?

Qualquer solução de R que é executado no SQL Server pode usar somente os pacotes que estão instalados na biblioteca R padrão associada à instância.

Quando você instala os recursos de R no SQL Server, a biblioteca de pacote de R está localizada na pasta de instância.

+ Instância padrão *MSSQLSERVER* 

    2017 do SQL Server:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` 
    
    SQL Server 2016:`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`

+ Instância nomeada *MyNamedInstance* 

    2017 do SQL Server:`C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` 
    
    SQL Server 2016:`C:\Program Files\Microsoft SQL Server\MSSQL13.MyNamedInstance\R_SERVICES\library`

Você pode executar a instrução a seguir para verificar a biblioteca padrão para a instância atual do R.

```SQL
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```
## <a name="r-packages-installed-with-sql-server"></a>Pacotes R instalados com o SQL Server

Quando você instala a linguagem R no SQL Server, por padrão o R **base** pacotes estão instalados. Pacotes de base incluem a funcionalidade de núcleo fornecida por pacotes como `stats` e `utils`.

Instalação do R no SQL Server 2016 e no SQL Server 2017 também inclui o **RevoScaleR** de pacote e pacotes aprimorados relacionados e provedores, que oferece suporte para contextos de computação remota, streaming, execução paralela de função rx, e muitos outros recursos.

+ Para obter uma visão geral dos recursos aprimorados de R, consulte [sobre o servidor de aprendizado de máquina](https://docs.microsoft.com/r-server/what-is-microsoft-r-server)

+ Para baixar as bibliotecas de RevoScaleR em um computador cliente, instale [Microsoft R Client](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client)

## <a name="permissions-required-for-installing-r-packages"></a>Permissões necessárias para instalar pacotes de R

No SQL Server 2016, o administrador precisava instalar novos pacotes de R em toda a instância. No SQL Server de 2017, novos recursos de banco de dados foram adicionados que possibilitam que o administrador de banco de dados para delegar o gerenciamento de pacote para os usuários selecionados.

Esta seção descreve as permissões necessárias para instalar e gerenciar pacotes por versão.

+ SQL Server 2016 R Services (no banco de dados)

    Para instalar um novo pacote de R em um computador que esteja executando [!INCLUDE [ssCurrent](..\..\includes\sscurrent-md.md)], você deve ter direitos administrativos no computador. É a tarefa do administrador de banco de dados ou outro administrador no servidor para garantir que todos os pacotes necessários estão instalados a [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] instância.

    Se você não tem privilégios administrativos no computador que hospeda o [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] instância, você pode fornecer as informações do administrador sobre como instalar pacotes de R e fornecer acesso a um repositório de pacote seguro onde pacotes solicitado por usuários podem ser obtidos.

+ Serviços de Machine Learning do SQL Server 2017

    Esta versão inclui funções de gerenciamento de pacote que permitem que o administrador de banco de dados delegar os direitos de instalação do pacote para os usuários selecionados. Se esse recurso foi habilitado, solicite que seu administrador de banco de dados você adicionar a uma das novas funções do pacote. Para obter mais informações, consulte [gerenciamento de pacotes de R para o SQL Server](r-package-management-for-sql-server-r-services.md).

    Se você for um administrador na instância do SQL Server, você pode instalar novos pacotes conforme o desejado. Apenas certifique-se de usar a biblioteca padrão que é associada à instância. Pacotes instalados em outros locais não podem ser executado quando chamado a partir de um procedimento armazenado. Qualquer código de R que é executado usando o SQL Server como um contexto de computação também requer que os pacotes estejam disponíveis na biblioteca de instância.

+ R Server (Autônomo)

    Você precisa de direitos administrativos no computador para instalar novos pacotes de R.

+ Outros ambientes de cliente

    Se você estiver instalando um novo pacote de R em um computador que está sendo usado como uma estação de trabalho de R e o computador **não** tiver uma instância de [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] instalada, você ainda precisará de direitos administrativos no computador para Instale o pacote. Após a instalação do pacote, você pode executá-lo localmente.

## <a name="managing-or-viewing-installed-packages"></a>Gerenciar ou exibir os pacotes instalados

Há várias maneiras que você pode obter uma lista completa dos pacotes instalados no momento. Para obter mais informações, consulte [determinar quais pacotes estão instalados no SQL Server](determine-which-packages-are-installed-on-sql-server.md).
