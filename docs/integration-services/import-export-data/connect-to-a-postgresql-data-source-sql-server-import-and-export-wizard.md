---
title: Conectar-se a uma fonte de dados do PostgreSQL (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b7a75a72-b267-444f-9eb8-d23eb333fc35
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0890fbce533a540300ebd6b7da37a1fc26572a52
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768062"
---
# <a name="connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard"></a>Conectar-se a uma fonte de dados do PostgreSQL (Assistente de Importação e Exportação do SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Este tópico mostra como se conectar a uma fonte de dados do **PostgreSQL** (arquivo de texto) por meio da página **Escolher uma Fonte de Dados** ou **Escolher um Destino** do Assistente de Importação e Exportação do SQL Server. 

> [!IMPORTANT]
> Os requisitos detalhados e pré-requisitos para se conectar a um banco de dados PostgreSQL estão além do escopo deste artigo da Microsoft. Este artigo pressupõe que você já tem software cliente PostgreSQL instalado e que você já pode se conectar com êxito ao banco de dados do PostgreSQL de destino. Para obter mais informações, consulte o administrador do banco de dados PostgreSQL ou a documentação do PostgreSQL.

## <a name="get-the-postgresql-odbc-driver"></a>Obter o driver ODBC PostgreSQL

### <a name="install-the-odbc-driver-with-stack-builder"></a>Instalar o driver ODBC com o construtor de pilha
Execute o construtor de pilha para adicionar o driver ODBC PostgreSQL (psqlODBC) para a sua instalação do PostgreSQL.

![Instalar o PostgreSQL ODBC com o construtor de pilha](../../integration-services/import-export-data/media/install-postgresql-odbc-with-stack-builder.png)

### <a name="or-download-the-latest-odbc-driver"></a>Ou então, baixar o driver ODBC mais recente
Ou baixe o Windows Installer para obter a versão mais recente do driver do ODBC PostgreSQL (psqlODBC) diretamente deste site FTP: [https://www.postgresql.org/ftp/odbc/versions/msi/](https://www.postgresql.org/ftp/odbc/versions/msi/). Extraia os arquivos do arquivo .zip e execute o arquivo .msi.

## <a name="connect-to-postgresql-with-the-postgresql-odbc-driver-psqlodbc"></a>Conecte-se ao PostgreSQL com o driver ODBC PostgreSQL (psqlODBC)
Drivers ODBC não estão listados na lista suspensa de fontes de dados. Para se conectar com um driver ODBC, comece selecionando o **Provedor de Dados do .NET Framework para ODBC** como a fonte de dados na página **Escolher uma Fonte de Dados** ou **Escolher um Destino**. Esse provedor atua como um wrapper em torno do driver ODBC.

Esta é a tela genérica que você vê imediatamente depois de selecionar o Provedor de Dados do .NET Framework para ODBC.

![Conecte-se ao PostgreSQL com o ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-postgresql-odbc-driver"></a>Opções a serem especificadas (Driver ODBC para PostgreSQL)

> [!NOTE]
> As opções de conexão para este provedor de dados e driver ODBC serão as mesmas se o PostgreSQL for sua origem ou seu destino. Ou seja, as opções exibidas nas páginas **Escolher uma Fonte de Dados** e **Escolher um Destino** do assistente são as mesmas.

Para se conectar ao PostgreSQL com o Driver ODBC do PostgreSQL, monte uma cadeia de conexão que inclua as seguintes configurações e os respectivos valores. O formato de uma cadeia de conexão completa vem imediatamente após a lista de configurações.

> [!TIP]
> Obtenha ajuda para montar uma cadeia de conexão realmente certa. Em vez de fornecer uma cadeia de conexão, forneça um DSN (nome de fonte de dados) existente ou crie um novo. Para obter mais informações sobre essas opções, consulte [Conectar-se a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Driver**  
O nome do driver ODBC – um entre **PostgreSQL ODBC Driver(UNICODE)** e **PostgreSQL ODBC Driver(ANSI)** .

**Servidor**  
O nome do servidor PostgreSQL. 

**Porta**  
A porta a ser usada para se conectar ao servidor PostgreSQL.

**Backup de banco de dados**  
O nome do banco de dados PostgreSQL.

**Uid** e **Pwd**   
A **Uid** (ID de usuário) e **Pwd** (senha) para se conectar.

### <a name="connection-string-format"></a>Formato da cadeia de conexão
Aqui está o formato de uma cadeia de conexão típica. 

```console
Driver={PostgreSQL ODBC Driver(UNICODE)};Server=<server>;Port=<port>;Database=<database>;UID=<user id>;PWD=<password>
```

### <a name="enter-the-connection-string"></a>Inserir a cadeia de conexão
Insira a cadeia de conexão no campo **ConnectionString** ou digite o nome DSN no campo **Dsn**, na página **Escolher uma Fonte de Dados** ou **Escolher um Destino**. Depois de inserir a cadeia de conexão, o assistente analisa a cadeia de caracteres e exibe as propriedades individuais e seus valores na lista.

O exemplo a seguir usa esta cadeia de conexão.

```console
Driver={PostgreSQL ODBC Driver(UNICODE)};Server=127.0.0.1;Port=5432;Database=postgres;UID=postgres;PWD=********
```

Esta é a tela que você vê depois de inserir a cadeia de conexão.

![Conectar-se ao PostgreSQL com o ODBC](../../integration-services/import-export-data/media/connect-to-postgresql-with-odbc.png)

## <a name="other-data-providers-and-more-info"></a>Outros provedores de dados e obter mais informações
Para obter informações sobre como se conectar ao PostgreSQL com um provedor de dados que não está listado aqui, consulte [Cadeias de conexão PostgreSQL](https://www.connectionstrings.com/postgresql/). Este site de terceiros também contém mais informações sobre os provedores de dados e os parâmetros de conexão descritos nesta página.

## <a name="see-also"></a>Confira também
[Escolher uma Fonte de Dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolher um Destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

