---
title: Conectar-se a uma fonte de dados do MySQL (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3d7c5a38-18d3-4cc9-a241-04422cb250d3
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b07dc7322a8bc09ecd344aef76163b911c06c866
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35411288"
---
# <a name="connect-to-a-mysql-data-source-sql-server-import-and-export-wizard"></a>Conectar-se a uma fonte de dados do MySQL (Assistente de Importação e Exportação do SQL Server)
Este tópico mostra como se conectar a uma fonte de dados do **MySQL** (arquivo de texto) por meio da página **Escolher uma Fonte de Dados** ou **Escolher um Destino** do Assistente de Importação e Exportação do SQL Server. Há vários provedores de dados que você pode usar para se conectar ao MySQL.

> [!IMPORTANT]
> Os requisitos e pré-requisitos detalhados para se conectar a um banco de dados MySQL estão além do escopo deste artigo da Microsoft. Este artigo pressupõe que você já tem software cliente MySQL instalado e que você já pode se conectar com êxito ao banco de dados do MySQL de destino. Para obter mais informações, consulte o administrador do banco de dados MySQL ou a documentação do MySQL.

## <a name="get-the-mysql-connectors"></a>Obter os conectores do MySQL
Baixe os provedores e drivers descritos neste tópico da página [Conectores MySQL](https://dev.mysql.com/downloads/connector/).

## <a name="connect-to-mysql-with-the-net-framework-data-provider-for-mysql"></a>Conectar-se ao MySQL com o provedor de dados do .NET Framework para MySQL
Depois de selecionar o **Provedor de Dados do .NET Framework para MySQL** na página **Escolher uma Fonte de Dados** ou **Escolher um Destino** do assistente, a página apresenta uma lista agrupada das opções para o provedor. Muitas delas são nomes não amigáveis e configurações desconhecidas. Felizmente, você só precisa fornecer algumas poucas informações. Ignore os valores padrão para as outras configurações.

> [!NOTE]
> As opções de conexão para este provedor de dados serão as mesmas se o MySQL for sua origem ou seu destino. Ou seja, as opções exibidas nas páginas **Escolher uma Fonte de Dados** e **Escolher um Destino** do assistente são as mesmas.

|Informações necessárias|Propriedade Provedor de Dados do .NET Framework para MySQL|
|---|---|
|Nome do servidor|**Servidor**|
|Nome do banco de dados|**Backup de banco de dados**|
|Informações (logon) de Autenticação|**ID de usuário** e **Senha**|

Você não precisa inserir a cadeia de conexão no campo **ConnectionString** da lista. Depois de inserir valores individuais para o nome do servidor MySQL (**Servidor**) e informações de logon, o assistente monta a cadeia de conexão das propriedades individuais e dos respectivos valores. 

![Conectar-se ao MySQL com o provedor de .NET, 1 de 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-1-of-2.png)

![Conectar-se ao MySQL com o provedor de .NET, 2 de 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-2-of-2.png)

## <a name="connect-to-mysql-with-the-mysql-odbc-driver"></a>Conectar-se ao MySQL com o driver ODBC do MySQL
Drivers ODBC não estão listados na lista suspensa de fontes de dados. Para se conectar com um driver ODBC, comece selecionando o **Provedor de Dados do .NET Framework para ODBC** como a fonte de dados na página **Escolher uma Fonte de Dados** ou **Escolher um Destino**. Esse provedor atua como um wrapper em torno do driver ODBC.

Esta é a tela genérica que você vê imediatamente depois de selecionar o Provedor de Dados do .NET Framework para ODBC.

![Conectar-se ao SQL com o ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-mysql-odbc-driver"></a>Opções a serem especificadas (Driver ODBC do MySQL)

> [!NOTE]
> As opções de conexão para este provedor de dados e driver ODBC serão as mesmas se o MySQL for sua origem ou seu destino. Ou seja, as opções exibidas nas páginas **Escolher uma Fonte de Dados** e **Escolher um Destino** do assistente são as mesmas.

Para se conectar ao MySQL com o Driver ODBC do MySQL, monte uma cadeia de conexão que inclua as seguintes configurações e os respectivos valores. O formato de uma cadeia de conexão completa vem imediatamente após a lista de configurações.

> [!TIP]
> Obtenha ajuda para montar uma cadeia de conexão realmente certa. Em vez de fornecer uma cadeia de conexão, forneça um DSN (nome de fonte de dados) existente ou crie um novo. Para obter mais informações sobre essas opções, consulte [Conectar-se a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Driver**  
O nome do driver ODBC.

**Servidor**  
O nome do servidor MySQL. 

**Backup de banco de dados**  
O nome do banco de dados MySQL.

**UID** e **PWD**   
A ID de usuário e senha para se conectar.

### <a name="connection-string-format"></a>Formato da cadeia de conexão
Aqui está o formato de uma cadeia de conexão típica.

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=<server>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>Inserir a cadeia de conexão
Insira a cadeia de conexão no campo **ConnectionString** ou digite o nome DSN no campo **Dsn**, na página **Escolher uma Fonte de Dados** ou **Escolher um Destino**. Depois de inserir a cadeia de conexão, o assistente analisa a cadeia de caracteres e exibe as propriedades individuais e seus valores na lista.

O exemplo a seguir usa esta cadeia de conexão.

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=127.0.0.1;Database=world;UID=root;PWD=********
    ```

Esta é a tela que você vê depois de inserir a cadeia de conexão.

![Conectar-se ao MySQL com ODBC](../../integration-services/import-export-data/media/connect-to-mysql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>Outros provedores de dados e obter mais informações
Para obter informações sobre como se conectar ao MySQL com um provedor de dados que não está listado aqui, consulte [Cadeias de conexão MySQL](https://www.connectionstrings.com/mysql/). Este site de terceiros também contém mais informações sobre os provedores de dados e os parâmetros de conexão descritos nesta página.

## <a name="see-also"></a>Confira também
[Escolher uma Fonte de Dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolher um Destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

