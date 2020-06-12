---
title: Conectando-se ao SQL Server (AccessToSQL) | Microsoft Docs
description: Saiba como se conectar a uma instância de destino do banco de dados SQL para migrar bancos de dados do Access. O SSMA Obtém os metadados sobre os bancos de dados no SQL Database.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- authentication
- instance of SQL Server
- metadata, refreshing
- ports
- refreshing metadata
- spaces in database names
- special characters
- SQL Server
- SQL Server, connecting
- SQL Server, connecting to
- SQL Server, reconnecting
ms.assetid: f84cf007-ddf1-4396-a07c-3e0729abc769
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 6266eb0596b351a7ef54baed6a7a76a7a655ac60
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293083"
---
# <a name="connecting-to-sql-server-accesstosql"></a>Conectando-se ao SQL Server (AccessToSQL)
Para migrar bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, você deve se conectar à instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando você se conecta, o SSMA obtém metadados sobre os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exibe os metadados do banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados. O SSMA armazena informações sobre a instância do à qual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] você está conectado, mas não armazena senhas.  
  
Sua conexão com SQL Server permanece ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao SQL Server se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar os objetos de banco de dados em SQL Server e migrar.  
  
Os metadados sobre a instância do SQL Server não são sincronizados automaticamente. Em vez disso, para atualizar os metadados no SQL Server Gerenciador de metadados, você deve atualizar manualmente os metadados de SQL Server. Para obter mais informações, consulte a seção "sincronizando metadados de SQL Server" mais adiante neste tópico.  
  
## <a name="required-sql-server-permissions"></a>Permissões de SQL Server necessárias  
A conta usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer permissões diferentes dependendo das ações que são executadas por essa conta.  
  
-   Para converter objetos do Access em [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, para atualizar metadados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou para salvar a sintaxe convertida em scripts, a conta deve ter permissão para fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para carregar objetos de banco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados no e para migrar para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, o requisito mínimo de permissão é a associação na função de banco de **db_owner** no banco de dados de destino.  
  
## <a name="establishing-a-sql-server-connection"></a>Estabelecendo uma conexão SQL Server  
Antes de converter objetos de banco de dados do Access em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe, você deve estabelecer uma conexão com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde você deseja migrar os bancos de dados do Access.  
  
Ao definir as propriedades de conexão, você também especifica o banco de dados em que os objetos e data serão migrados. Você pode personalizar esse mapeamento no nível do banco de dados do Access depois de se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [mapeando bancos de dados de origem e de destino](mapping-source-and-target-databases-accesstosql.md).  
  
> [!IMPORTANT]  
> Antes de se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , verifique se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução e pode aceitar conexões. Para obter mais informações, consulte "conectando-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados" nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manuais online do.  
  
**Para se conectar ao SQL Server**  
  
1.  No menu **arquivo** , selecione **conectar-se a SQL Server**.  
  
    Se você se conectou anteriormente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o nome do comando será **reconectado a SQL Server**.  
  
2.  Na caixa **nome do servidor** , digite ou selecione o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Se você estiver se conectando à instância padrão no computador local, poderá inserir **localhost** ou um ponto (**.**).  
  
    -   Se você estiver se conectando à instância padrão em outro computador, insira o nome do computador.  
  
    -   Se você estiver se conectando a uma instância nomeada, insira o nome do computador, uma barra invertida e o nome da instância. Por exemplo: MyServer\MyInstance.  
  
    -   Para se conectar a uma instância de usuário ativa do [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] , conecte-se usando o protocolo de pipes nomeados e especificando o nome do pipe, como \\ \\ chamado .\pipe\sql\query. Para obter mais informações, consulte a documentação do [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)].  
  
3.  Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurada para aceitar conexões em uma porta não padrão, insira o número da porta que é usado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexões na caixa **porta do servidor** . Para a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o número da porta padrão é 1433. Para instâncias nomeadas, o SSMA tentará obter o número da porta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador.  
  
4.  Na caixa **de dados,** digite o nome do banco de dados de destino para a migração de objeto e data.  
  
    Essa opção não está disponível ao reconectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    O nome do banco de dados de destino não pode conter espaços ou caracteres especiais. Por exemplo, você pode migrar bancos de dados do Access para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados chamado "ABC". Mas você não pode migrar bancos de dados do Access para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados denominado "a b-c".  
  
    Você pode personalizar esse mapeamento por banco de dados depois de se conectar. Para obter mais informações, consulte [mapeando bancos de dados de origem e de destino](mapping-source-and-target-databases-accesstosql.md)  
  
5.  No menu suspenso **autenticação** , selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta atual do Windows, selecione **autenticação do Windows**. Para usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon, selecione **SQL Server autenticação**e, em seguida, forneça um nome de usuário e uma senha.  
  
6.  Para conexão segura, dois controles são adicionados, caixa de seleção **criptografar conexão** e caixa de seleção **TrustServerCertificate** . Somente quando a caixa de seleção **criptografar conexão** está marcada, a caixa de seleção **TrustServerCertificate** está visível. Quando a opção **criptografar conexão** está marcada (true) e **TrustServerCertificate** está desmarcada (false), o validará o SQL Server certificado SSL. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para garantir isso, um certificado deve ser instalado no lado do cliente, bem como no lado do servidor.  
  
7.  Clique em **Conectar**.  
  
**Compatibilidade de versão superior**  
  
É permitido conectar/reconectar-se a versões mais recentes do SQL Server.  
  
1.  Você poderá se conectar ao SQL Server 2008 ou SQL Server 2012 quando o projeto criado for SQL Server 2005.  
  
2.  Você poderá se conectar ao SQL Server 2012 quando o projeto criado for SQL Server 2008, mas não tiver permissão para se conectar a versões anteriores, ou seja, SQL Server 2005.  
  
3.  Você poderá se conectar somente a SQL Server 2012 quando o projeto criado for SQL Server 2012.  
  
4.  A compatibilidade de versão superior não é válida para SQL Azure.  
  
||||||||
|-|-|-|-|-|-|-|
|**TIPO de projeto vs. versão do servidor de destino**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 (versão: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008 (versão: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 (versão: 11. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 (versão: 12. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 (versão: 13. x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|Sim|Sim|Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||Sim|Sim|Sim|Sim||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||Sim|Sim|Sim||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||Sim|Sim||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||Yes||
|SQL Azure||||||Yes|
  
> [!IMPORTANT]  
> A conversão dos objetos de banco de dados é executada de acordo com o tipo de projeto, mas não de acordo com a versão do SQL Server conectado ao. No caso do projeto SQL Server 2005, a conversão é realizada de acordo com SQL Server 2005, mesmo que você esteja conectado a uma versão superior do SQL Server (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizando metadados de SQL Server  
Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os esquemas forem alterados após a conexão, você poderá sincronizar os metadados com o servidor.  
  
**Para sincronizar SQL Server metadados**  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, clique com o botão direito do mouse em **bancos**de dados e, em seguida, selecione **sincronizar com Database**.  
  
## <a name="reconnecting-to-sql-server"></a>Reconectando ao SQL Server  
Sua conexão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanecerá ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar os objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados no e migrar.  
  
O procedimento para reconectar-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é o mesmo que o procedimento para estabelecer uma conexão.  
  
## <a name="next-steps"></a>Próximas etapas  
Se você quiser personalizar o mapeamento entre os bancos de dados de origem e de destino, consulte [mapeando bancos](mapping-source-and-target-databases-accesstosql.md) de dados de origem e de destino de outra forma, a próxima etapa é converter objetos de Database para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe usando [converter objetos de banco de dados](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
