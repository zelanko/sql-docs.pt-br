---
title: Conectar-se a uma fonte de dados do Oracle (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b0bd1f5a-34dd-4be3-9ac8-f9f87727781b
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1f15cffa118a8783b02a1d04fcd953aa4dbb14b4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-an-oracle-data-source-sql-server-import-and-export-wizard"></a>Conectar-se a uma fonte de dados do Oracle (Assistente de Importação e Exportação do SQL Server)
Este tópico mostra como se conectar a uma fonte de dados do **Oracle** (arquivo de texto) por meio da página **Escolher uma Fonte de Dados** ou **Escolher um Destino** do Assistente de Importação e Exportação do SQL Server. Há vários provedores de dados que você pode usar para se conectar ao Oracle.

> [!IMPORTANT]
> Os requisitos detalhados e pré-requisitos para se conectar a um banco de dados Oracle estão além do escopo deste artigo da Microsoft. Este artigo pressupõe que você já tem software cliente Oracle instalado e que você já pode se conectar com êxito ao banco de dados do Oracle de destino. Para obter mais informações, consulte o administrador do banco de dados Oracle ou a documentação do Oracle.

## <a name="connect-to-oracle-with-the-net-framework-data-provider-for-oracle"></a>Conectar-se ao Oracle com o Provedor de Dados .NET Framework para Oracle
Depois de selecionar o **Provedor de dados .NET Framework para Oracle** na página **Escolher uma fonte de dados** ou **Escolher um destino** do assistente, a página apresenta uma lista agrupada das opções para o provedor. Muitas delas são nomes não amigáveis e configurações desconhecidas. Felizmente, você só precisa fornecer duas ou três informações. Ignore os valores padrão para as outras configurações.

> [!NOTE]
> As opções de conexão para este provedor de dados serão as mesmas se o Oracle for sua origem ou seu destino. Ou seja, as opções exibidas nas páginas **Escolher uma Fonte de Dados** e **Escolher um Destino** do assistente são as mesmas.

|Informações necessárias|Propriedade Provedor de Dados .NET Framework para Oracle|
|---|---|
|Nome do servidor|**Fonte de dados**|
|Informações (logon) de Autenticação|**ID de Usuário** e **Senha**; ou **Segurança Integrada**|

Você não precisa inserir a cadeia de conexão no campo **ConnectionString** da lista. Depois de inserir valores individuais para o nome do servidor Oracle (**fonte de dados**) e informações de logon, o assistente monta a cadeia de conexão das propriedades individuais e dos respectivos valores. 

![Conectar-se ao Oracle com o provedor de .NET](../../integration-services/import-export-data/media/connect-to-oracle-with-net-provider.jpg)

## <a name="connect-to-oracle-with-the-microsoft-odbc-driver-for-oracle"></a>Conectar-se ao Oracle com o driver ODBC da Microsoft para Oracle
Drivers ODBC não estão listados na lista suspensa de fontes de dados. Para se conectar com um driver ODBC, comece selecionando o **Provedor de Dados do .NET Framework para ODBC** como a fonte de dados na página **Escolher uma Fonte de Dados** ou **Escolher um Destino**. Esse provedor atua como um wrapper em torno do driver ODBC.

Esta é a tela genérica que você vê imediatamente depois de selecionar o Provedor de Dados do .NET Framework para ODBC.

![Conectar-se ao Oracle com o ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-oracle"></a>Opções a serem especificadas (Driver ODBC para Oracle)

> [!NOTE]
> As opções de conexão para este provedor de dados e driver ODBC serão as mesmas se o Oracle for sua origem ou seu destino. Ou seja, as opções exibidas nas páginas **Escolher uma Fonte de Dados** e **Escolher um Destino** do assistente são as mesmas.

Para se conectar ao Oracle com o Driver ODBC do Oracle, monte uma cadeia de conexão que inclua as seguintes configurações e os respectivos valores. O formato de uma cadeia de conexão completa vem imediatamente após a lista de configurações.

> [!TIP]
> Obtenha ajuda para montar uma cadeia de conexão realmente certa. Em vez de fornecer uma cadeia de conexão, forneça um DSN (nome de fonte de dados) existente ou crie um novo. Para obter mais informações sobre essas opções, consulte [Conectar-se a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Driver**  
O nome do driver ODBC, **Microsoft ODBC para Oracle**.

**Servidor**  
O nome do servidor Oracle. 

**Uid** e **Pwd**   
A ID de usuário e senha para se conectar.

### <a name="connection-string-format"></a>Formato da cadeia de conexão
Aqui está o formato de uma cadeia de conexão típica.

    ```
    Driver={Microsoft ODBC for Oracle};Server=myServerAddress;Uid=myUsername;Pwd=myPassword;
    ```

### <a name="enter-the-connection-string"></a>Inserir a cadeia de conexão
Insira a cadeia de conexão no campo **ConnectionString** ou digite o nome DSN no campo **Dsn**, na página **Escolher uma Fonte de Dados** ou **Escolher um Destino**. Depois de inserir a cadeia de conexão, o assistente analisa a cadeia de caracteres e exibe as propriedades individuais e seus valores na lista.

Esta é a tela que você vê depois de inserir a cadeia de conexão.

![Conectar-se ao Oracle com o ODBC](../../integration-services/import-export-data/media/connect-to-oracle-with-odbc.jpg)

## <a name="whats-my-oracle-server-name"></a>O que é o meu nome do servidor Oracle?
Execute uma das consultas a seguir para obter o nome do servidor Oracle.

`SELECT host_name FROM v$instance`

ou em

`SELECT sys_context('USERENV','SERVER_HOST') FROM dual`

## <a name="other-data-providers-and-more-info"></a>Outros provedores de dados e obter mais informações
Para obter informações sobre como se conectar ao Oracle com um provedor de dados que não está listado aqui, consulte [Cadeias de conexão Oracle](https://www.connectionstrings.com/oracle/). Este site de terceiros também contém mais informações sobre os provedores de dados e os parâmetros de conexão descritos nesta página.

## <a name="see-also"></a>Confira também
[Escolher uma Fonte de Dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolher um Destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

