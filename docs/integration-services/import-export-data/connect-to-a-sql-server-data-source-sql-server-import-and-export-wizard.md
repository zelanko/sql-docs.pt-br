---
title: Conectar-se a uma fonte de dados do SQL Server (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 386cedbb-fae5-45ce-9363-c4a417f80a2f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 938a6d8ba779d1cef37b5fab767e609d00b4f022
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78339764"
---
# <a name="connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard"></a>Conectar-se a uma fonte de dados do SQL Server (Assistente de Importação e Exportação do SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Este tópico mostra como se conectar a uma fonte de dados do **Microsoft SQL Server** (arquivo de texto) por meio da página **Escolher uma Fonte de Dados** ou **Escolher um Destino** do Assistente de Importação e Exportação do SQL Server. Há vários provedores de dados que você pode usar para se conectar ao SQL Server.

> [!TIP]
> Se você estiver em uma rede com vários servidores, poderá ser mais fácil digitar o nome do servidor em vez de expandir a lista suspensa de servidores. Se você clicar na lista suspensa, poderá demorar muito tempo para consultar a rede em busca de todos os servidores disponíveis e o servidor desejado poderá não estar listado nos resultados.

## <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>Conectar-se ao SQL Server com o Provedor de Dados .NET Framework para SQL Server 
Depois de selecionar o **Provedor de Dados do .NET Framework para SQL Server** na página **Escolher uma Fonte de Dados** ou **Escolher um Destino** do assistente, a página apresenta uma lista agrupada das opções para o provedor. Muitas delas são nomes não amigáveis e configurações desconhecidas. Felizmente, para se conectar a qualquer banco de dados empresarial, em geral, você precisa fornecer apenas algumas poucas informações. Ignore os valores padrão para as outras configurações.

> [!NOTE]
> As opções de conexão para este provedor de dados serão as mesmas se o SQL Server for sua origem ou destino. Ou seja, as opções exibidas nas páginas **Escolher uma Fonte de Dados** e **Escolher um Destino** do assistente são as mesmas.

|Informações necessárias|Propriedade do Provedor de Dados do .NET Framework para SQL Server|
|---|---|
|Autenticação|Use o padrão **NotSpecified** como "Segurança Integrada" ou escolha outro modo de autenticação. Não há suporte para "Autenticação do Active Directory Interativa". |
|Nome do servidor|**Fonte de Dados**|
|Informações (logon) de Autenticação|**Segurança Integrada**; ou **ID de Usuário** e **Senha**<br/>Se você desejar ver uma lista suspensa de bancos de dados no servidor, primeiro você precisará fornecer informações de logon válidas.|
|Nome do banco de dados|**Catálogo Inicial**|

![Conectar-se ao SQL com o provedor de .NET](../../integration-services/import-export-data/media/connect-to-sql-with-net-provider.jpg)

### <a name="options-to-specify-net-framework-data-provider-for-sql-server"></a>Opções a especificar (Provedor de Dados do .NET Framework para SQL Server)

> [!NOTE]
> As opções de conexão para este provedor de dados serão as mesmas se o SQL Server for sua origem ou destino. Ou seja, as opções exibidas nas páginas **Escolher uma Fonte de Dados** e **Escolher um Destino** do assistente são as mesmas.

**Fonte de Dados**  
 Digite o nome ou endereço IP do servidor de origem ou de destino, ou então selecione um servidor na lista suspensa.  
 
 Para especificar uma porta TCP não padrão, digite uma vírgula após o nome do servidor ou endereço IP e, em seguida, digite o número da porta.
 
 **Catálogo Inicial**  
 Digite o nome do banco de dados de origem ou de destino, ou então selecione um banco de dados da lista suspensa.  
  
 **Segurança Integrada**  
 Especifique **True** para conectar-se usando a autenticação integrada do Windows (recomendado) ou **False** para conectar-se usando a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você especificar **False**, deverá inserir uma ID de usuário e uma senha. O valor padrão é **Falso**.  
  
 **ID de usuário**  
 Se você estiver usando a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], digite um nome de usuário.  
  
 **Senha**  
 Se você estiver usando a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], digite a senha.  

## <a name="connect-to-sql-server-with-the-odbc-driver-for-sql-server"></a>Conectar-se ao SQL Server com o driver ODBC para SQL Server 
Drivers ODBC não estão listados na lista suspensa de fontes de dados. Para se conectar com um driver ODBC, comece selecionando o **Provedor de Dados do .NET Framework para ODBC** como a fonte de dados. Esse provedor atua como um wrapper em torno do driver ODBC.

> [!TIP]
> **Obtenha o driver mais recente**. Baixe o [Microsoft ODBC Driver 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339).

Esta é a tela genérica que você vê imediatamente depois de selecionar o Provedor de Dados do .NET Framework para ODBC.

![Conectar-se ao SQL com o ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-sql-server"></a>Opções a serem especificadas (criver ODBC para SQL Server)

> [!NOTE]
> As opções de conexão para o driver ODBC serão as mesmas se o SQL Server for sua origem ou destino. Ou seja, as opções exibidas nas páginas **Escolher uma Fonte de Dados** e **Escolher um Destino** do assistente são as mesmas.

Para se conectar ao SQL Server com o driver ODBC mais recente, monte uma cadeia de conexão que inclua as seguintes configurações e os respectivos valores. O formato de uma cadeia de conexão completa vem imediatamente após a lista de configurações.

> [!TIP]
> Obtenha ajuda para montar uma cadeia de conexão realmente certa. Em vez de fornecer uma cadeia de conexão, forneça um DSN (nome de fonte de dados) existente ou crie um novo. Para obter mais informações sobre essas opções, consulte [Conectar-se a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Driver**  
O nome do driver ODBC. O nome é diferente para diferentes versões do driver.

**Servidor**  
O nome do SQL Server.

**Backup de banco de dados**  
O nome do banco de dados.  

**Trusted_Connection**; ou **Uid** e **Pwd**  
Especifique **Trusted_Connection=Yes** para se conectar com a Autenticação Integrada do Windows; ou especifique **Uid** (ID de usuário) e **Pwd** (senha) para se conectar com a autenticação do SQL Server.

### <a name="connection-string-format"></a>Formato da cadeia de conexão
Aqui está o formato de uma cadeia de conexão que usa a Autenticação Integrada do Windows.

    `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;trusted_connection=Yes;`

Aqui está o formato de uma cadeia de conexão que usa a autenticação do SQL Server em vez da Autenticação Integrada do Windows.

     `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;uid=<user id>;pwd=<password>;`

### <a name="enter-the-connection-string"></a>Inserir a cadeia de conexão
Insira a cadeia de conexão no campo **ConnectionString** ou digite o nome DSN no campo **Dsn**, na página **Escolher uma Fonte de Dados** ou **Escolher um Destino**. Depois de inserir a cadeia de conexão, o assistente analisa a cadeia de caracteres e exibe as propriedades individuais e seus valores na lista.

O exemplo a seguir usa esta cadeia de conexão.

    `Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;`

Esta é a tela que você vê depois de inserir a cadeia de conexão.

![Conectar-se ao SQL com o ODBC após](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="connect-to-sql-server-with-the-microsoft-ole-db-provider-for-sql-server-or-sql-server-native-client"></a>Conectar-se ao SQL Server com o SQL Server Native Client ou o Provedor Microsoft OLE DB para SQL Server

> [!IMPORTANT]
> O Microsoft OLE DB Provider para SQL Server e SQL Server Native Client não são compatíveis com versões do SQL Server após o SQL Server 2012. Em vez disso, use o driver ODBC. Para saber mais sobre a transição para o driver ODBC, consulte as postagens de blog a seguir.
>   -   [A Microsoft está se adequando ao ODBC para acesso a dados relacionais nativos](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)
>   -   [Apresentando os Microsoft ODBC Drivers for SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)

## <a name="other-data-providers-and-more-info"></a>Outros provedores de dados e obter mais informações
Para obter informações sobre como se conectar ao SQL Server com um provedor de dados que não está listado aqui, consulte [Cadeias de conexão do SQL Server](https://www.connectionstrings.com/sql-server/). Este site de terceiros também contém mais informações sobre os provedores de dados e os parâmetros de conexão descritos nesta página.

## <a name="see-also"></a>Confira também
[Escolher uma Fonte de Dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolher um Destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

