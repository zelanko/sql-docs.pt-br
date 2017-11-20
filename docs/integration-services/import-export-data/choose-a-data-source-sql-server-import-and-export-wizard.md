---
title: "Escolha uma fonte de dados (SQL Server Assistente de importação e exportação) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
caps.latest.revision: 124
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 80d35cb294fd900611c73ca37bba2a66baef0767
ms.contentlocale: pt-br
ms.lasthandoff: 08/28/2017

---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>Escolher uma fonte de dados (Assistente de Importação e Exportação do SQL Server)
  Após a página de boas-vindas, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra **Escolher uma fonte de dados**. Nessa página, você fornece informações sobre a fonte de dados e sobre como se conectar a ela.
  
Para obter informações sobre as fontes de dados que você pode usar, consulte [Quais fontes de dados e destinos posso usar?](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

## <a name="screen-shot-of-the-choose-a-data-source-page"></a>Captura de tela da página Escolher uma Fonte de Dados 
A captura de tela a seguir mostra a primeira parte da página **Escolher uma Fonte de Dados** do assistente. O restante da página tem um número variável de opções que dependem da fonte de dados que você escolhe aqui.

![Escolher fonte](../../integration-services/import-export-data/media/choose-source.png)

## <a name="choose-a-data-source"></a>Escolher uma fonte de dados
 **Fonte de dados**  
Especifique a fonte de dados selecionando um provedor de dados que pode conectar à fonte.

-   **O provedor de dados que você precisa é normalmente óbvio em seu nome**, porque o nome do provedor normalmente contém o nome da fonte de dados - por exemplo, *arquivo simples* fonte, Microsoft *Excel*, Microsoft *acesso*, .net Framework Data Provider para *SqlServer*, .net Framework Data Provider para *Oracle*.

-   **Se você tiver um driver ODBC para a fonte de dados**, selecione o .net Framework Data Provider para ODBC. Em seguida, insira as informações específicas do driver. Drivers ODBC não estão listados na lista suspensa de fontes de dados. O .net Framework Data Provider para ODBC atua como um wrapper em torno do driver ODBC. Para obter mais informações, consulte [conectar a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Pode haver mais de um provedor disponível para sua fonte de dados.** Normalmente, você pode selecionar qualquer provedor que funciona com sua origem. Por exemplo, para se conectar à Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode usar o .NET Framework Data Provider para SQL Server ou o driver ODBC do SQL Server. (Outros provedores ainda estão na lista, mas não têm mais suporte.) 

## <a name="my-data-source-isnt-in-the-list"></a>Minha fonte de dados não está na lista
-   **Talvez seja necessário baixar o provedor de dados** da Microsoft ou de terceiros. A lista de provedores de dados disponíveis no **fonte de dados** lista inclui somente os provedores instalados no seu computador. Para obter informações sobre as fontes de dados que você pode usar, consulte [Quais fontes de dados e destinos posso usar?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **Você tem um driver ODBC para a fonte de dados?** Drivers ODBC não estão listados na lista suspensa de fontes de dados. Se você tiver um driver ODBC para a fonte de dados, selecione o .net Framework Data Provider para ODBC. Em seguida, insira as informações específicas do driver. O .net Framework Data Provider para ODBC atua como um wrapper em torno do driver ODBC. Para obter mais informações, consulte [conectar a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **provedores de 64 bits e 32 bits.** Se você estiver executando o Assistente de 64 bits, você não verá as fontes de dados para o qual um provedor de 32 bits está instalado e vice-versa.

> [!NOTE]
> Para usar a versão de 64 bits do SQL Server Assistente de importação e exportação, você precisa instalar o SQL Server. SQL Server Data Tools (SSDT) e SQL Server Management Studio (SSMS) são aplicativos de 32 bits, somente instalar os arquivos de 32 bits, incluindo a versão de 32 bits do assistente.

## <a name="after-you-choose-a-data-source"></a>Depois de escolher uma fonte de dados
Depois que você escolher uma fonte de dados, o restante do **escolher uma fonte de dados** página tem um número variável de opções que dependem do provedor de dados que você escolher.

Para se conectar a uma fonte de dados usadas com frequência, consulte uma das seguintes páginas.
-   [Conectar ao SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se ao Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se a arquivos simples (arquivos de texto)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se para o Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se para acesso](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Conecte-se com ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar ao armazenamento de BLOBs do Azure](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Conecte-se ao PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar ao MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

Para obter informações sobre como se conectar a uma fonte de dados que não esteja listada aqui, consulte [a referência de cadeias de caracteres de Conexão](https://www.connectionstrings.com/). Este site de terceiros contém cadeias de caracteres de conexão de exemplo e obter mais informações sobre provedores de dados e as informações de conexão que eles exigem.

## <a name="whats-next"></a>O que vem a seguir?  
 Depois de fornecer informações sobre a fonte de dados e sobre como se conectar a ela, a próxima página será **Escolher um Destino**. Nessa página, você fornece informações sobre o destino dos dados e sobre como se conectar a ele. Para obter mais informações, consulte [Escolher um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).
 
## <a name="see-also"></a>Consulte também
[Começar com esse exemplo simples de Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



