---
title: "Conectar a uma fonte de dados Oracle (SQL Server Assistente de importação e exportação) | Microsoft Docs"
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
ms.assetid: b0bd1f5a-34dd-4be3-9ac8-f9f87727781b
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e589e7f7a0262d258342bf887ec84c57d57dc978
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-oracle-data-source-sql-server-import-and-export-wizard"></a>Conectar a uma fonte de dados Oracle (Assistente de exportação e importação do SQL Server)
Este tópico mostra como se conectar a um **Oracle** da fonte de dados do **escolher uma fonte de dados** ou **escolha um destino** página do Assistente para exportação e importação do SQL Server. Há vários provedores de dados que você pode usar para se conectar ao Oracle.

> [!IMPORTANT]
> Os requisitos detalhados e pré-requisitos para se conectar a um banco de dados Oracle estão além do escopo deste artigo da Microsoft. Este artigo pressupõe que você já tem software cliente Oracle instalado e que você já pode conectar com êxito para o banco de dados do Oracle de destino. Para obter mais informações, consulte o administrador do banco de dados Oracle ou a documentação do Oracle.

## <a name="connect-to-oracle-with-the-net-framework-data-provider-for-oracle"></a>Conecte-se ao Oracle com o .net Framework Data Provider for Oracle
Depois de selecionar **.NET Framework Data Provider for Oracle** no **escolher uma fonte de dados** ou **escolha um destino** página do assistente, a página apresenta uma lista agrupada das opções para o provedor. Esses são nomes amigáveis e configurações familiarizadas. Felizmente, você só precisa fornecer dois ou três partes de informações. Você pode ignorar os valores padrão para as outras configurações.

> [!NOTE]
> As opções de conexão para este provedor de dados são os mesmos se Oracle é sua fonte ou destino. Ou seja, as opções exibidas são os mesmos em ambos os **escolher uma fonte de dados** e o **escolha um destino** páginas do assistente.

|Informações necessárias|.NET framework Data Provider para propriedade de Oracle|
|---|---|
|Nome do servidor|**Fonte de dados**|
|Informações de autenticação (logon)|**ID de usuário** e **senha**; ou, **segurança integrada**|

Você não precisa inserir a cadeia de conexão do **ConnectionString** campo da lista. Depois de inserir valores individuais para o nome do servidor Oracle (**fonte de dados**) e informações de logon, o assistente reúne a cadeia de caracteres de conexão das propriedades individuais e seus valores. 

![Conecte-se ao Oracle com o provedor de .NET](../../integration-services/import-export-data/media/connect-to-oracle-with-net-provider.jpg)

## <a name="connect-to-oracle-with-the-microsoft-odbc-driver-for-oracle"></a>Conecte-se ao Oracle com o driver ODBC da Microsoft para Oracle
Drivers ODBC não estão listados na lista suspensa de fontes de dados. Para se conectar com um driver ODBC, comece selecionando o **.NET Framework Data Provider para ODBC** como a fonte de dados no **escolher uma fonte de dados** ou **escolha um destino** página. Este provedor atua como um wrapper em torno do driver ODBC.

Esta é a tela genérica que você vê imediatamente depois de selecionar o provedor de dados .NET Framework para ODBC.

![Conecte-se ao Oracle com ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-oracle"></a>Opções para especificar (Driver de ODBC para Oracle)

> [!NOTE]
> As opções de conexão para este provedor de dados e o driver ODBC são os mesmos se Oracle é sua fonte ou destino. Ou seja, as opções exibidas são os mesmos em ambos os **escolher uma fonte de dados** e o **escolha um destino** páginas do assistente.

Para se conectar ao Oracle com o Driver ODBC do Oracle, monte uma cadeia de caracteres de conexão que inclui as seguintes configurações e seus valores. O formato de uma cadeia de conexão completa imediatamente após a lista de configurações.

> [!TIP]
> Obter ajuda para montar uma cadeia de caracteres de conexão certa. Em vez de fornecer uma cadeia de caracteres de conexão, forneça um DSN (nome de fonte de dados) de existente ou crie um novo. Para obter mais informações sobre essas opções, consulte [conectar a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Driver**  
O nome do driver ODBC, **Microsoft ODBC para Oracle**.

**Servidor**  
O nome do servidor Oracle. 

**UID** e **Pwd**   
A id de usuário e senha para se conectar.

### <a name="connection-string-format"></a>Formato de cadeia de caracteres de Conexão
Aqui está o formato de uma cadeia de conexão típica.

    ```
    Driver={Microsoft ODBC for Oracle};Server=myServerAddress;Uid=myUsername;Pwd=myPassword;
    ```

### <a name="enter-the-connection-string"></a>Insira a cadeia de caracteres de conexão
Insira a cadeia de conexão a **ConnectionString** campo ou digite o nome DSN no **Dsn** campo, o **escolher uma fonte de dados** ou **escolha um destino** página. Depois de inserir a cadeia de caracteres de conexão, o assistente analisa a cadeia de caracteres e exibe as propriedades individuais e seus valores na lista.

Esta é a tela que você vê depois de inserir a cadeia de caracteres de conexão.

![Conecte-se ao Oracle com ODBC](../../integration-services/import-export-data/media/connect-to-oracle-with-odbc.jpg)

## <a name="whats-my-oracle-server-name"></a>O que é o nome do servidor Oracle?
Execute uma das consultas a seguir para obter o nome do servidor Oracle.

`SELECT host_name FROM v$instance`

ou

`SELECT sys_context('USERENV','SERVER_HOST') FROM dual`

## <a name="other-data-providers-and-more-info"></a>Outros provedores de dados e obter mais informações
Para obter informações sobre como conectar-se ao Oracle com um provedor de dados não estiver listado aqui, consulte [cadeias de caracteres de conexão Oracle](https://www.connectionstrings.com/oracle/). Este site de terceiros também contém mais informações sobre os provedores de dados e os parâmetros de conexão descritos nesta página.

## <a name="see-also"></a>Consulte também
[Escolha uma fonte de dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolha um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


