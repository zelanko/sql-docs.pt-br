---
title: "Conectar a uma fonte de dados MySQL (Assistente de exportação e importação do SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3d7c5a38-18d3-4cc9-a241-04422cb250d3
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3df56fcda5b39c2895de83feac4f302686b1adf3
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-mysql-data-source-sql-server-import-and-export-wizard"></a>Conectar a uma fonte de dados MySQL (Assistente de exportação e importação do SQL Server)
Este tópico mostra como se conectar a um **MySQL** da fonte de dados do **escolher uma fonte de dados** ou **escolha um destino** página do Assistente para exportação e importação do SQL Server. Há vários provedores de dados que você pode usar para se conectar ao MySQL.

> [!IMPORTANT]
> Os requisitos detalhados e pré-requisitos para se conectar a um banco de dados MySQL estão além do escopo deste artigo da Microsoft. Este artigo pressupõe que você já tiver software de cliente do MySQL instalada e que você já pode conectar com êxito para o banco de dados do MySQL de destino. Para obter mais informações, consulte seu administrador de banco de dados MySQL ou a documentação do MySQL.

## <a name="get-the-mysql-connectors"></a>Obter os conectores do MySQL
Baixe os provedores e drivers descritos neste tópico do [MySQL conectores](https://dev.mysql.com/downloads/connector/) página.

## <a name="connect-to-mysql-with-the-net-framework-data-provider-for-mysql"></a>Conectar ao MySQL com o .net Framework Data Provider para MySQL
Depois de selecionar **.NET Framework Data Provider para MySQL** no **escolher uma fonte de dados** ou **escolha um destino** página do assistente, a página apresenta uma lista agrupada das opções para o provedor. Esses são nomes amigáveis e configurações familiarizadas. Felizmente, você só precisa fornecer algumas partes de informações. Você pode ignorar os valores padrão para as outras configurações.

> [!NOTE]
> As opções de conexão para este provedor de dados são os mesmos se MySQL é sua fonte ou destino. Ou seja, as opções exibidas são os mesmos em ambos os **escolher uma fonte de dados** e o **escolha um destino** páginas do assistente.

|Informações necessárias|.NET framework Data Provider para a propriedade do MySQL|
|---|---|
|Nome do servidor|**Servidor**|
|Nome do banco de dados|**Banco de dados**|
|Informações de autenticação (logon)|**Id de usuário** e **senha**|

Você não precisa inserir a cadeia de conexão do **ConnectionString** campo da lista. Depois de inserir valores individuais para o nome do servidor MySQL (**Server**) e informações de logon, o assistente reúne a cadeia de caracteres de conexão das propriedades individuais e seus valores. 

![Conectar ao MySQL com o provedor de .NET, 1 de 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-1-of-2.png)

![Conectar ao MySQL com o provedor de .NET, 2 de 2](../../integration-services/import-export-data/media/connect-to-mysql-with-the-net-provider-2-of-2.png)

## <a name="connect-to-mysql-with-the-mysql-odbc-driver"></a>Conectar ao MySQL com o driver ODBC do MySQL
Drivers ODBC não estão listados na lista suspensa de fontes de dados. Para se conectar com um driver ODBC, comece selecionando o **.NET Framework Data Provider para ODBC** como a fonte de dados no **escolher uma fonte de dados** ou **escolha um destino** página. Este provedor atua como um wrapper em torno do driver ODBC.

Esta é a tela genérica que você vê imediatamente depois de selecionar o provedor de dados .NET Framework para ODBC.

![Conectar ao SQL com ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-mysql-odbc-driver"></a>Opções para especificar (MySQL ODBC Driver)

> [!NOTE]
> As opções de conexão para este provedor de dados e o driver ODBC são os mesmos se MySQL é sua fonte ou destino. Ou seja, as opções exibidas são os mesmos em ambos os **escolher uma fonte de dados** e o **escolha um destino** páginas do assistente.

Para se conectar ao MySQL com o driver ODBC do MySQL, monte uma cadeia de caracteres de conexão que inclui as seguintes configurações e seus valores. O formato de uma cadeia de conexão completa imediatamente após a lista de configurações.

> [!TIP]
> Obter ajuda para montar uma cadeia de caracteres de conexão certa. Em vez de fornecer uma cadeia de caracteres de conexão, forneça um DSN (nome de fonte de dados) de existente ou crie um novo. Para obter mais informações sobre essas opções, consulte [conectar a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Driver**  
O nome do driver ODBC.

**Servidor**  
O nome do servidor MySQL. 

**Banco de dados**  
O nome do banco de dados MySQL.

**UID** e **PWD**   
A id de usuário e senha para se conectar.

### <a name="connection-string-format"></a>Formato de cadeia de caracteres de Conexão
Aqui está o formato de uma cadeia de conexão típica.

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=<server>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>Insira a cadeia de caracteres de conexão
Insira a cadeia de conexão a **ConnectionString** campo ou digite o nome DSN no **Dsn** campo, o **escolher uma fonte de dados** ou **escolha um destino** página. Depois de inserir a cadeia de caracteres de conexão, o assistente analisa a cadeia de caracteres e exibe as propriedades individuais e seus valores na lista.

O exemplo a seguir usa essa cadeia de caracteres de conexão.

    ```
    Driver={MySQL ODBC 5.3 Unicode Driver};Server=127.0.0.1;Database=world;UID=root;PWD=********
    ```

Esta é a tela que você vê depois de inserir a cadeia de caracteres de conexão.

![Conectar ao MySQL com ODBC](../../integration-services/import-export-data/media/connect-to-mysql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>Outros provedores de dados e obter mais informações
Para obter informações sobre como se conectar ao MySQL com um provedor de dados não estiver listado aqui, consulte [cadeias de caracteres de conexão MySQL](https://www.connectionstrings.com/mysql/). Este site de terceiros também contém mais informações sobre os provedores de dados e os parâmetros de conexão descritos nesta página.

## <a name="see-also"></a>Consulte também
[Escolha uma fonte de dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolha um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


