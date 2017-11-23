---
title: "Conectar a uma fonte de dados PostgreSQL (Assistente de exportação e importação do SQL Server) | Microsoft Docs"
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
ms.assetid: b7a75a72-b267-444f-9eb8-d23eb333fc35
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4c82ae7eedc3e18e7591cf7ab30a507920695247
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard"></a>Conectar a uma fonte de dados PostgreSQL (Assistente de exportação e importação do SQL Server)
Este tópico mostra como se conectar a um **PostgreSQL** da fonte de dados do **escolher uma fonte de dados** ou **escolha um destino** página do Assistente para exportação e importação do SQL Server. 

> [!IMPORTANT]
> Os requisitos detalhados e pré-requisitos para se conectar a um banco de dados PostgreSQL estão além do escopo deste artigo da Microsoft. Este artigo pressupõe que você já tiver software de cliente PostgreSQL instalado e que você já pode conectar com êxito ao banco de dados PostgreSQL destino. Para obter mais informações, consulte seu administrador de banco de dados PostgreSQL ou a documentação de PostgreSQL.

## <a name="get-the-postgresql-odbc-driver"></a>Obtenha o driver ODBC PostgreSQL

### <a name="install-the-odbc-driver-with-stack-builder"></a>Instalar o driver ODBC com o construtor de pilha
Execute o construtor de pilha para adicionar o driver ODBC PostgreSQL (psqlODBC) para a instalação do PostgreSQL.

![Instalar PostgreSQL ODBC com o construtor de pilha](../../integration-services/import-export-data/media/install-postgresql-odbc-with-stack-builder.png)

### <a name="or-download-the-latest-odbc-driver"></a>Ou então, baixar o driver ODBC mais recente
Ou, baixe o Windows installer para a versão mais recente do driver ODBC PostgreSQL (psqlODBC) diretamente do site FTP - [https://www.postgresql.org/ftp/odbc/versions/msi/](https://www.postgresql.org/ftp/odbc/versions/msi/). Extraia os arquivos do arquivo. zip e execute o arquivo. msi.

## <a name="connect-to-postgresql-with-the-postgresql-odbc-driver-psqlodbc"></a>Conectar ao PostgreSQL com o driver ODBC PostgreSQL (psqlODBC)
Drivers ODBC não estão listados na lista suspensa de fontes de dados. Para se conectar com um driver ODBC, comece selecionando o **.NET Framework Data Provider para ODBC** como a fonte de dados no **escolher uma fonte de dados** ou **escolha um destino** página. Este provedor atua como um wrapper em torno do driver ODBC.

Esta é a tela genérica que você vê imediatamente depois de selecionar o provedor de dados .NET Framework para ODBC.

![Conecte-se ao PostgreSQL com ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-postgresql-odbc-driver"></a>Opções para especificar (PostgreSQL ODBC driver)

> [!NOTE]
> As opções de conexão para este provedor de dados e o driver ODBC são os mesmos se PostgreSQL é sua fonte ou destino. Ou seja, as opções exibidas são os mesmos em ambos os **escolher uma fonte de dados** e o **escolha um destino** páginas do assistente.

Para se conectar a PostgreSQL com o driver ODBC PostgreSQL, monte uma cadeia de caracteres de conexão que inclui as seguintes configurações e seus valores. O formato de uma cadeia de conexão completa imediatamente após a lista de configurações.

> [!TIP]
> Obter ajuda para montar uma cadeia de caracteres de conexão certa. Em vez de fornecer uma cadeia de caracteres de conexão, forneça um DSN (nome de fonte de dados) de existente ou crie um novo. Para obter mais informações sobre essas opções, consulte [conectar a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Driver**  
O nome do driver ODBC - o **PostgreSQL ODBC Driver(UNICODE)** ou **PostgreSQL ODBC Driver(ANSI)**.

**Servidor**  
O nome do servidor PostgreSQL. 

**Porta**  
A porta a ser usada para se conectar ao servidor PostgreSQL.

**Banco de dados**  
O nome do banco de dados PostgreSQL.

**UID** e **Pwd**   
O **Uid** (id de usuário) e **Pwd** (senha) para se conectar.

### <a name="connection-string-format"></a>Formato de cadeia de caracteres de Conexão
Aqui está o formato de uma cadeia de conexão típica. 

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=<server>;Port=<port>;Database=<database>;UID=<user id>;PWD=<password>
    ```

### <a name="enter-the-connection-string"></a>Insira a cadeia de caracteres de conexão
Insira a cadeia de conexão a **ConnectionString** campo ou digite o nome DSN no **Dsn** campo, o **escolher uma fonte de dados** ou **escolha um destino** página. Depois de inserir a cadeia de caracteres de conexão, o assistente analisa a cadeia de caracteres e exibe as propriedades individuais e seus valores na lista.

O exemplo a seguir usa essa cadeia de caracteres de conexão.

    ```
    Driver={PostgreSQL ODBC Driver(UNICODE)};Server=127.0.0.1;Port=5432;Database=postgres;UID=postgres;PWD=********
    ```

Esta é a tela que você vê depois de inserir a cadeia de caracteres de conexão.

![Conecte-se ao PostgreSQL com ODBC](../../integration-services/import-export-data/media/connect-to-postgresql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>Outros provedores de dados e obter mais informações
Para obter informações sobre como se conectar a PostgreSQL com um provedor de dados não estiver listado aqui, consulte [cadeias de caracteres de conexão PostgreSQL](https://www.connectionstrings.com/postgresql/). Este site de terceiros também contém mais informações sobre os provedores de dados e os parâmetros de conexão descritos nesta página.

## <a name="see-also"></a>Consulte também
[Escolha uma fonte de dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolha um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


