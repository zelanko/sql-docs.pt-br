---
title: "Escolha um destino (Assistente de exportação e importação do SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.chooseadestination.f1
ms.assetid: 1898be15-3e69-42d3-8ecb-3733c9f6c8e3
caps.latest.revision: 104
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 4ff3c7c8413bd6b535e1c5f95e2a7b06b397c053
ms.contentlocale: pt-br
ms.lasthandoff: 08/28/2017

---
# <a name="choose-a-destination-sql-server-import-and-export-wizard"></a>Escolher um destino (Assistente de Importação e Exportação do SQL Server)
 Depois de fornecer informações sobre a fonte de dados e sobre como se conectar a ela, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra a página **Escolher um Destino**. Nessa página, você fornece informações sobre o destino dos dados e sobre como se conectar a ele.
  
Para obter informações sobre os destinos de dados que você pode usar, consulte [Quais fontes de dados e destinos posso usar?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources). 

## <a name="screen-shot-of-the-destination-page"></a>Captura de tela da página Destino
A captura de tela a seguir mostra a parte da página **Escolher um Destino** do assistente. O restante da página tem um número variável de opções que dependem de destino que você escolher aqui.

![Escolher destino](../../integration-services/import-export-data/media/choose-destination.png)

## <a name="choose-a-destination"></a>Escolher um Destino
 **Destino**  
 Especifique o destino selecionando um provedor de dados que pode importar dados no destino.
 
-   **O provedor de dados que você precisa é normalmente óbvio em seu nome**, porque o nome do provedor normalmente contém o nome do destino - por exemplo, *arquivo simples* destino, a Microsoft *Excel*, Microsoft *acesso*, .net Framework Data Provider para *SqlServer*, .net Framework Data Provider para *Oracle*.

-   **Se você tiver um driver ODBC para seu destino**, selecione o .net Framework Data Provider para ODBC. Em seguida, insira as informações específicas do driver. Drivers ODBC não estão listados na lista suspensa de destinos. O .net Framework Data Provider para ODBC atua como um wrapper em torno do driver ODBC. Para obter mais informações, consulte [conectar a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Pode haver mais de um provedor disponível para seu destino.** Normalmente, você pode selecionar qualquer provedor que funciona com o destino. Por exemplo, para se conectar à Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode usar o .NET Framework Data Provider para SQL Server ou o driver ODBC do SQL Server. (Outros provedores ainda estão na lista, mas não têm mais suporte.) 

## <a name="my-destination-isnt-in-the-list"></a>O destino não está na lista
-   **Talvez seja necessário baixar o provedor de dados** da Microsoft ou de terceiros. A lista de provedores de dados disponíveis no **destino** lista inclui somente os provedores instalados no seu computador. Para obter informações sobre os destinos que você pode usar, consulte [quais fontes de dados e destinos posso usar?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **Você tem um driver ODBC para seu destino?** Drivers ODBC não estão listados na lista suspensa de destinos. Se você tiver um driver ODBC para seu destino, selecione o .net Framework Data Provider para ODBC. Em seguida, insira as informações específicas do driver. O .net Framework Data Provider para ODBC atua como um wrapper em torno do driver ODBC. Para obter mais informações, consulte [conectar a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **provedores de 64 bits e 32 bits.** Se você estiver executando o Assistente de 64 bits, não verá os destinos para o qual um provedor de 32 bits está instalado e vice-versa.

> [!NOTE]
> Para usar a versão de 64 bits do SQL Server Assistente de importação e exportação, você precisa instalar o SQL Server. SQL Server Data Tools (SSDT) e SQL Server Management Studio (SSMS) são aplicativos de 32 bits, somente instalar os arquivos de 32 bits, incluindo a versão de 32 bits do assistente.

## <a name="after-you-choose-a-destination"></a>Depois de escolher um destino
Depois que você escolher um destino, o restante do **escolha um destino** página tem um número variável de opções que dependem do provedor de dados que você escolher.

Para se conectar a um destino usado, consulte uma das seguintes páginas.
-   [Conectar ao SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se ao Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se a arquivos simples (arquivos de texto)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se para o Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se para acesso](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se com ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar ao armazenamento de BLOBs do Azure](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Conecte-se ao PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar ao MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

Para obter informações sobre como se conectar a um destino que não esteja listado aqui, consulte [a referência de cadeias de caracteres de Conexão](https://www.connectionstrings.com/). Este site de terceiros contém cadeias de caracteres de conexão de exemplo e obter mais informações sobre provedores de dados e as informações de conexão que eles exigem.

## <a name="whats-next"></a>O que vem a seguir?  
 Depois de fornecer informações sobre o destino dos dados e sobre como se conectar a eles, a próxima página é **Especificar cópia ou consulta de tabela**. Nessa página, você especifica se quer copiar uma tabela inteira ou apenas algumas linhas. Para obter mais informações, consulte [Especificar cópia ou consulta de tabela](../../integration-services/import-export-data/specify-table-copy-or-query-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Consulte também
[Começar com esse exemplo simples de Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



