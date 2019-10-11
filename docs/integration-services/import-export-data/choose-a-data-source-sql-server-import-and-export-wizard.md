---
title: Escolher uma fonte de dados (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.chooseadatasource.f1
ms.assetid: ebf28a62-dfc1-4b39-9db5-df1919e5fccb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b707b2b31c15c565353f0ff581ca1f4d7308a25b
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71951940"
---
# <a name="choose-a-data-source-sql-server-import-and-export-wizard"></a>Escolher uma fonte de dados (Assistente de Importação e Exportação do SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Após a página de boas-vindas, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibe **Escolher uma Fonte de Dados**. Nessa página, você fornece informações sobre a fonte de dados e sobre como se conectar a ela.
  
Para obter informações sobre as fontes de dados que você pode usar, consulte [Quais fontes de dados e destinos posso usar?](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

> [!NOTE]
> O Assistente de Importação e Exportação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza o SSIS (SQL Server Integration Services). Portanto, as mesmas limitações que se aplicam ao SSIS também se aplicam ao assistente.  Por exemplo, as colunas ErrorCode e ErrorColumn, que são adicionadas por padrão, conforme descrito em [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md).

## <a name="screen-shot-of-the-choose-a-data-source-page"></a>Captura de tela da página Escolher uma Fonte de Dados 
A imagem a seguir mostra a primeira parte da página **Escolher uma Fonte de Dados** do assistente. O restante da página tem um número variável de opções que dependem da fonte de dados que você escolhe aqui.

![Escolher fonte](../../integration-services/import-export-data/media/choose-source.png)

## <a name="choose-a-data-source"></a>Escolher uma fonte de dados
 **Fonte de dados**  
Especifique a fonte de dados selecionando um provedor de dados que pode conectar à fonte.

-   **O provedor de dados de que você precisa é normalmente óbvio pelo respectivo nome**, porque o nome do provedor normalmente contém o nome da fonte de dados – por exemplo, fonte de dados de *arquivo simples*, Microsoft *Excel*, Microsoft *Access*, Provedor de Dados do .NET Framework para *SqlServer*, Provedor de Dados do .NET Framework para *Oracle*.

-   **Se você tiver um driver ODBC para sua fonte de dados**, selecione o Provedor de Dados do .NET Framework para ODBC. Em seguida, insira as informações específicas do driver. Drivers ODBC não estão listados na lista suspensa de fontes de dados. O Provedor de Dados do .NET Framework para ODBC atua como um wrapper em torno do driver ODBC. Para obter mais informações, consulte [Conectar-se a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Pode haver mais de um provedor disponível para sua fonte de dados.** Normalmente, você pode selecionar qualquer provedor que funciona com sua origem. Por exemplo, para se conectar ao Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode usar o Provedor de dados do .NET Framework para SQL Server ou o driver ODBC do SQL Server. (Outros provedores ainda estão na lista, mas não são mais compatíveis.) 

## <a name="my-data-source-isnt-in-the-list"></a>Minha fonte de dados não está na lista
-   **Talvez você precise baixar o provedor de dados** da Microsoft ou de terceiros. A lista de provedores de dados disponíveis na lista **Fonte de dados** inclui somente os provedores instalados em seu computador. Para obter informações sobre as fontes de dados que você pode usar, consulte [Quais fontes de dados e destinos posso usar?](import-and-export-data-with-the-sql-server-import-and-export-wizard.md#wizardSources)

-   **Você tem um driver ODBC para sua fonte de dados?** Drivers ODBC não estão listados na lista suspensa de fontes de dados. Se você tiver um driver ODBC para sua fonte de dados, selecione o Provedor de Dados do .NET Framework para ODBC. Em seguida, insira as informações específicas do driver. O Provedor de Dados do .NET Framework para ODBC atua como um wrapper em torno do driver ODBC. Para obter mais informações, consulte [Conectar-se a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

-   **Provedores de 32 e de 64 bits.** Se você estiver executando o assistente de 64 bits, você não verá as fontes de dados para as quais um provedor de 32 bits está instalado e vice-versa.

> [!NOTE]
> Para usar a versão de 64 bits do Assistente de Importação e Exportação do SQL Server, você precisa instalar o SQL Server. O SSDT (SQL Server Data Tools) e o SSMS (SQL Server Management Studio) são aplicativos de 32 bits e somente instalam arquivos de 32 bits, incluindo a versão de 32 bits do assistente.

## <a name="after-you-choose-a-data-source"></a>Depois de escolher uma fonte de dados
Depois de escolher uma fonte de dados, o restante da página **Escolher uma Fonte de Dados** apresenta opções variáveis que dependem do provedor de dados escolhido.

Para se conectar a uma fonte de dados usada com frequência, consulte uma das páginas a seguir.
-   [Conectar ao SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se a arquivos simples (arquivos de texto)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao Armazenamento de Blobs do Azure](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar-se ao MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

Para obter informações sobre como se conectar a uma fonte de dados que não está listada aqui, consulte [A referência de cadeias de conexão](https://www.connectionstrings.com/). Esse site de terceiros contém cadeias de conexão de exemplo e mais informações sobre provedores de dados e as informações de conexão exigidas por elas.

## <a name="whats-next"></a>O que vem a seguir?
 Depois de fornecer informações sobre a fonte de dados e sobre como se conectar a ela, a próxima página será **Escolher um Destino**. Nessa página, você fornece informações sobre o destino dos dados e sobre como se conectar a ele. Para obter mais informações, consulte [Escolher um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md).

## <a name="see-also"></a>Confira também
[Começar com esse exemplo simples de Assistente de Importação e Exportação](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../../includes/paragraph-content/contribute-to-content.md)]
