---
title: Escolher um destino (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 86b2cf26c7af957579c5368ed70262e43db005f1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285872"
---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>Escolher um destino (Assistente de Importação e Exportação do SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 Depois de fornecer informações sobre a fonte de dados e sobre como se conectar a ela, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra a página **Escolher um Destino**. Nessa página, você fornece informações sobre o destino dos dados e sobre como se conectar a ele.
  
Para obter informações sobre os destinos de dados que você pode usar, consulte [Quais fontes de dados e destinos posso usar?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources). 

## <a name="screen-shot-of-the-destination-page"></a>Captura de tela da página Destino
A captura de tela a seguir mostra a parte da página **Escolher um Destino** do assistente. O restante da página tem um número variável de opções que dependem do destino que você escolhe aqui.

![Escolher destino](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>Escolher um Destino
 **Destino**  
 Especifique o destino selecionando um provedor de dados que pode importar dados no destino.
 
-   **O provedor de dados de que você precisa é normalmente óbvio pelo respectivo nome**, porque o nome do provedor normalmente contém o nome do destino – por exemplo, destino de *arquivo simples*, Microsoft *Excel*, Microsoft *Access*, Provedor de Dados do .NET Framework para *SqlServer*, Provedor de Dados do .NET Framework para *Oracle*.

-   **Se você tiver um driver ODBC para o destino**, selecione o Provedor de Dados do .NET Framework para ODBC. Em seguida, insira as informações específicas do driver. Drivers ODBC não estão listados na lista suspensa de destinos. O Provedor de Dados do .NET Framework para ODBC atua como um wrapper em torno do driver ODBC. Para obter mais informações, consulte [Conectar-se a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Pode haver mais de um provedor disponível para seu destino.** Normalmente, você pode selecionar qualquer provedor que funciona com o destino. Por exemplo, para se conectar ao Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode usar o Provedor de dados do .NET Framework para SQL Server ou o driver ODBC do SQL Server. (Outros provedores ainda estão na lista, mas não são mais compatíveis.) 

## <a name="my-destination-isnt-in-the-list"></a>O destino não está na lista
-   **Talvez você precise baixar o provedor de dados** da Microsoft ou de terceiros. A lista de provedores de dados disponíveis na lista **Destino** inclui somente os provedores instalados em seu computador. Para obter informações sobre os destinos que você pode usar, consulte [Quais fontes de dados e destinos posso usar?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **Você tem um driver ODBC para seu destino?** Drivers ODBC não estão listados na lista suspensa de destinos. Se você tiver um driver ODBC para o destino, selecione o Provedor de Dados do .NET Framework para ODBC. Em seguida, insira as informações específicas do driver. O Provedor de Dados do .NET Framework para ODBC atua como um wrapper em torno do driver ODBC. Para obter mais informações, consulte [Conectar-se a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Provedores de 32 e de 64 bits.** Se você estiver executando o assistente de 64 bits, você não verá os destinos para os quais um provedor de 32 bits está instalado e vice-versa.

> [!NOTE]
> Para usar a versão de 64 bits do Assistente de Importação e Exportação do SQL Server, você precisa instalar o SQL Server. O SSDT (SQL Server Data Tools) e o SSMS (SQL Server Management Studio) são aplicativos de 32 bits e somente instalam arquivos de 32 bits, incluindo a versão de 32 bits do assistente.

## <a name="after-you-choose-a-destination"></a>Depois de escolher um destino
Depois de escolher um destino, o restante da página **Escolher um Destino** apresenta opções variáveis que dependem do provedor de dados escolhido.

Para se conectar a um destino usado com frequência, consulte uma das páginas a seguir.
-   [Conectar ao SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se a arquivos simples (arquivos de texto)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao Armazenamento de Blobs do Azure](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

Para obter informações sobre como se conectar a um destino que não está listado aqui, consulte [A referência de cadeias de conexão](https://www.connectionstrings.com/). Esse site de terceiros contém cadeias de conexão de exemplo e mais informações sobre provedores de dados e as informações de conexão exigidas por elas.

## <a name="whats-next"></a>O que vem a seguir?  
 Depois de fornecer informações sobre o destino dos dados e sobre como se conectar a eles, a próxima página é **Especificar cópia ou consulta de tabela**. Nessa página, você especifica se quer copiar uma tabela inteira ou apenas algumas linhas. Para obter mais informações, consulte [Especificar cópia ou consulta de tabela](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Confira também
[Começar com esse exemplo simples de Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


