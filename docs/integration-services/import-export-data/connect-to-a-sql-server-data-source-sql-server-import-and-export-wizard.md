---
title: "Conecte-se a uma fonte de dados SQL Server (SQL Server Assistente de importação e exportação) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 386cedbb-fae5-45ce-9363-c4a417f80a2f
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 17910c8e30dee98f39e977896fb67774b54a798d
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard"></a>Conecte-se a uma fonte de dados SQL Server (Assistente de exportação e importação do SQL Server)
Este tópico mostra como se conectar a um **Microsoft SQL Server** da fonte de dados do **escolher uma fonte de dados** ou **escolha um destino** página do Assistente para exportação e importação do SQL Server. Há vários provedores de dados que você pode usar para se conectar ao SQL Server.

> [!TIP]
> Se você estiver em uma rede com vários servidores, pode ser mais fácil de digitar o nome do servidor, em vez de expandir a lista suspensa de servidores. Se você clicar na lista suspensa, pode levar muito tempo para consultar todos os servidores disponíveis na rede e os resultados não podem incluir até mesmo no servidor desejado.

## <a name="connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server"></a>Conectar-se ao SQL Server com o Provedor de Dados .NET Framework para SQL Server 
Depois de selecionar **.NET Framework Data Provider para SQL Server** no **escolher uma fonte de dados** ou **escolha um destino** página do assistente, a página exibe uma lista agrupada das opções para o provedor. Esses são nomes amigáveis e configurações familiarizadas. Felizmente, para se conectar a qualquer banco de dados da empresa, geralmente você precisa fornecer apenas algumas partes de informações. Você pode ignorar os valores padrão para as outras configurações.

> [!NOTE]
> As opções de conexão para este provedor de dados são os mesmos, independentemente do SQL Server é a fonte ou destino. Ou seja, as opções exibidas são os mesmos em ambos os **escolher uma fonte de dados** e o **escolha um destino** páginas do assistente.

|Informações necessárias|.NET framework Data Provider para a propriedade do SQL Server|
|---|---|
|Nome do servidor|**Fonte de dados**|
|Informações de autenticação (logon)|**Segurança integrada**; ou, **ID de usuário** e **senha**<br/>Se você quiser ver uma lista suspensa de bancos de dados no servidor, primeiro você precisa fornecer as informações de logon válido.|
|Nome do banco de dados|**Catálogo Inicial**|

![Conectar-se ao SQL com o provedor de .NET](../../integration-services/import-export-data/media/connect-to-sql-with-net-provider.jpg)

### <a name="options-to-specify-net-framework-data-provider-for-sql-server"></a>Opções para especificar (.NET Framework Data Provider para SQL Server)

> [!NOTE]
> As opções de conexão para este provedor de dados são os mesmos, independentemente do SQL Server é a fonte ou destino. Ou seja, as opções exibidas são os mesmos em ambos os **escolher uma fonte de dados** e o **escolha um destino** páginas do assistente.

**Fonte de dados**  
 Digite o nome ou endereço IP do servidor de origem ou destino, ou selecione um servidor na lista suspensa.  
 
 Para especificar uma porta TCP não padrão, digite uma vírgula após o nome do servidor ou endereço IP, em seguida, insira o número da porta.
 
 **Catálogo Inicial**  
 Digite o nome do banco de dados de origem ou destino, ou selecione um banco de dados na lista suspensa.  
  
 **Segurança Integrada**  
 Especifique **True** para se conectar com a autenticação integrada do Windows (recomendada) ou **False** para se conectar com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação. Se você especificar **False**, deverá inserir uma ID de usuário e uma senha. O valor padrão é **Falso**.  
  
 **ID de usuário**  
 Insira um nome de usuário, se você estiver usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.  
  
 **Senha**  
 Digite a senha, se você estiver usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.  

## <a name="connect-to-sql-server-with-the-odbc-driver-for-sql-server"></a>Conectar ao SQL Server com o driver ODBC para SQL Server 
Drivers ODBC não estão listados na lista suspensa de fontes de dados. Para se conectar com um driver ODBC, comece selecionando o **.NET Framework Data Provider para ODBC** como a fonte de dados. Este provedor atua como um wrapper em torno do driver ODBC.

> [!TIP]
> **Obtenha o driver mais recente**. Baixe o [Microsoft ODBC Driver 13 para SQL Server](https://www.microsoft.com/download/details.aspx?id=53339).

Esta é a tela genérica que você vê imediatamente depois de selecionar o provedor de dados .NET Framework para ODBC.

![Conectar ao SQL com ODBC antes de](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

### <a name="options-to-specify-odbc-driver-for-sql-server"></a>Opções para especificar (driver ODBC para SQL Server)

> [!NOTE]
> As opções de conexão para o driver ODBC são os mesmos, independentemente do SQL Server é a fonte ou destino. Ou seja, as opções exibidas são os mesmos em ambos os **escolher uma fonte de dados** e o **escolha um destino** páginas do assistente.

Para se conectar ao SQL Server com o driver ODBC mais recente, monte uma cadeia de caracteres de conexão que inclui as seguintes configurações e seus valores. O formato de uma cadeia de conexão completa imediatamente após a lista de configurações.

> [!TIP]
> Obter ajuda para montar uma cadeia de caracteres de conexão certa. Em vez de fornecer uma cadeia de caracteres de conexão, forneça um DSN (nome de fonte de dados) de existente ou crie um novo. Para obter mais informações sobre essas opções, consulte [conectar a uma fonte de dados ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).

**Driver**  
O nome do driver ODBC. O nome é diferente para diferentes versões do driver.

**Servidor**  
O nome do SQL Server.

**Banco de dados**  
O nome do banco de dados.  

**Trusted_Connection**; ou, **Uid** e **Pwd**  
Especifique **Trusted_Connection = Yes** para se conectar com a autenticação integrada do Windows; ou especifique **Uid** (id de usuário) e **Pwd** (senha) para se conectar com a autenticação do SQL Server.

### <a name="connection-string-format"></a>Formato de cadeia de caracteres de Conexão
Aqui está o formato de uma cadeia de conexão que usa autenticação integrada do Windows.

    `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;trusted_connection=Yes;`

Aqui está o formato de uma cadeia de conexão que usa a autenticação do SQL Server em vez da autenticação integrada do Windows.

     `Driver={ODBC Driver 13 for SQL Server};server=<server>;database=<database>;uid=<user id>;pwd=<password>;`

### <a name="enter-the-connection-string"></a>Insira a cadeia de caracteres de conexão
Insira a cadeia de conexão a **ConnectionString** campo ou digite o nome DSN no **Dsn** campo, o **escolher uma fonte de dados** ou **escolha um destino** página. Depois de inserir a cadeia de caracteres de conexão, o assistente analisa a cadeia de caracteres e exibe as propriedades individuais e seus valores na lista.

O exemplo a seguir usa essa cadeia de caracteres de conexão.

    `Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;`

Esta é a tela que você vê depois de inserir a cadeia de caracteres de conexão.

![Conectar ao SQL com ODBC após](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="connect-to-sql-server-with-the-microsoft-ole-db-provider-for-sql-server-or-sql-server-native-client"></a>Conecte-se ao SQL Server com o Microsoft OLE DB Provider para SQL Server ou SQL Server Native Client

> [!IMPORTANT]
> O Microsoft OLE DB Provider para SQL Server e SQL Server Native Client não têm suporte em versões do SQL Server após o SQL Server 2012. Use o driver ODBC. Para saber mais sobre a transição para o driver ODBC, consulte as postagens de blog a seguir.
>   -   [Microsoft está se adequando ao ODBC para acesso a dados relacionais nativos](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)
>   -   [Apresentando os novos Drivers de ODBC da Microsoft para SQL Server](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/)

## <a name="other-data-providers-and-more-info"></a>Outros provedores de dados e obter mais informações
Para obter informações sobre como conectar-se ao SQL Server com um provedor de dados não estiver listado aqui, consulte [cadeias de conexão do SQL Server](https://www.connectionstrings.com/sql-server/). Este site de terceiros também contém mais informações sobre os provedores de dados e os parâmetros de conexão descritos nesta página.

## <a name="see-also"></a>Consulte também
[Escolha uma fonte de dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolha um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


