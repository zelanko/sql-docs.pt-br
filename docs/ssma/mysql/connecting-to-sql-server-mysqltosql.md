---
title: Conectando-se ao SQL Server (MySQLToSQL) | Microsoft Docs
description: Saiba como se conectar a uma instância de destino do SQL Server para migrar bancos de dados MySQL. O SSMA obtém metadados sobre bancos de dados no SQL Server.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- connecting to SQL Server 2008, SQL Server permission
- connecting to SQL Server 2008, synchronization
ms.assetid: 08233267-693e-46e6-9ca3-3a3dfd3d2be7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 462b209d73f48217cf9941adf2e3af45d62371cd
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394281"
---
# <a name="connecting-to-sql-server-mysqltosql"></a>Conectar-se ao SQL Server (MySQLToSQL)
Para migrar bancos de dados MySQL para SQL Server, você deve se conectar à instância de destino do SQL Server. Quando você se conecta, o SSMA obtém metadados sobre todos os bancos de dados na instância do SQL Server e exibe os metadados do banco de dados no SQL Server Gerenciador de metadados. O SSMA armazena informações da instância do SQL Server ao qual você está conectado, mas não armazena senhas.  
  
Sua conexão com SQL Server permanece ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao SQL Server se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar os objetos de banco de dados em SQL Server e migrar.  
  
Os metadados sobre a instância do SQL Server não são sincronizados automaticamente. Em vez disso, para atualizar os metadados no SQL Server Gerenciador de metadados, você deve atualizar manualmente os metadados de SQL Server. Para obter mais informações, consulte a seção "sincronizando metadados de SQL Server" mais adiante neste tópico.  
  
## <a name="required-sql-server-permissions"></a>Permissões de SQL Server necessárias  
A conta usada para se conectar ao SQL Server requer permissões diferentes dependendo das ações que a conta executa:  
  
-   Para converter objetos MySQL em [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, para atualizar metadados de SQL Server ou para salvar a sintaxe convertida em scripts, a conta deve ter permissão para fazer logon na instância do SQL Server.  
  
-   Para carregar objetos de banco de dados em SQL Server, o requisito mínimo de permissão é a associação na função de banco de dados **db_owner** no banco de dados de destino.  
  
## <a name="establishing-a-sql-server-connection"></a>Estabelecendo uma conexão SQL Server  
Antes de converter objetos de banco de dados MySQL para SQL Server sintaxe, você deve estabelecer uma conexão com a instância do SQL Server em que você deseja migrar o banco de dados MySQL ou bancos.  
  
Ao definir as propriedades de conexão, você também especifica o banco de dados em que os objetos e data serão migrados. Você pode personalizar esse mapeamento no nível de esquema do MySQL depois de se conectar ao SQL Server. Para obter mais informações, consulte [mapeando bancos de dados MySQL para esquemas de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> Antes de tentar se conectar ao SQL Server, verifique se a instância do SQL Server está em execução e pode aceitar conexões.  
  
**Para se conectar ao SQL Server**  
  
1.  No menu **arquivo** , selecione **conectar-se a SQL Server** (essa opção é habilitada após a criação de um projeto).  
  
    Se você tiver se conectado anteriormente ao SQL Server, o nome do comando será **reconectado ao SQL Server**.  
  
2.  Na caixa de diálogo conexão, digite ou selecione o nome da instância do SQL Server.  
  
    -   Se você estiver se conectando à instância padrão no computador local, poderá inserir **localhost** ou um ponto (**.**).  
  
    -   Se você estiver se conectando à instância padrão em outro computador, insira o nome do computador.  
  
    -   Se você estiver se conectando a uma instância nomeada em outro computador, insira o nome do computador seguido por uma barra invertida e, em seguida, o nome da instância, como MyServer\MyInstance.  
  
3.  Se sua instância do SQL Server estiver configurada para aceitar conexões em uma porta não padrão, insira o número da porta que é usado para SQL Server conexões na caixa **porta do servidor** . Para a instância padrão do SQL Server, o número da porta padrão é 1433. Para instâncias nomeadas, o SSMA tentará obter o número da porta do serviço de SQL Server Browser.  
  
4.  Na caixa **autenticação** , selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta atual do Windows, selecione **autenticação do Windows**. Para usar um logon SQL Server, selecione SQL Server autenticação e, em seguida, forneça o nome de logon e a senha.  
  
5.  Para conexão segura, dois controles são adicionados, as caixas de seleção **criptografar conexão** e **TrustServerCertificate** . Somente quando a opção **criptografar conexão** está marcada, a caixa de seleção **TrustServerCertificate** está visível. Quando **criptografar conexão** está marcado (true) e **TrustServerCertificate** está desmarcado (false), ele validará o SQL Server certificado SSL. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para garantir isso, um certificado deve ser instalado no lado do cliente, bem como no lado do servidor.  
  
6.  Clique em Conectar.  
  
**Compatibilidade de versão superior**  
  
É permitido conectar/reconectar-se a versões mais recentes do SQL Server.  
  
1.  Você poderá se conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto criado for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
2.  Você poderá se conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto criado for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, mas não tiver permissão para se conectar a versões inferiores, ou seja, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
3.  Você poderá se conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto criado for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012.  
  
4.  Você poderá se conectar somente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto criado for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014.  
  
5.  A compatibilidade de versão superior não é válida para "SQL Azure".  
  
|TIPO de projeto versus versão do servidor de destino|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (Versão: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (Versão: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012<br />(Versão: 11. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014<br />(Versão: 12. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016<br />(Versão: 13. x)|SQL Azure|  
|-|-|-|-|-|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|Sim|Sim|Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||Sim|Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016|||||Sim||  
|SQL Azure||||||Sim|  
  
> [!IMPORTANT]  
> A conversão dos objetos de banco de dados é executada de acordo com o tipo de projeto, mas não de acordo com a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conectado ao. No caso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] projeto 2005, a conversão é realizada de acordo com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, embora você esteja conectado a uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizando metadados de SQL Server  
Metadados sobre bancos de dados SQL Server não são atualizados automaticamente. Os metadados no SQL Server Gerenciador de metadados é um instantâneo dos metadados quando você se conecta pela primeira vez ao SQL Server, ou a última vez que você atualizou os metadados manualmente. Você pode atualizar os metadados manualmente para todos os bancos de dados ou para qualquer banco de dados ou objeto de banco de dados individual.  
  
**Para sincronizar metadados**  
  
1.  Verifique se você está conectado a SQL Server.  
  
2.  No SQL Server Gerenciador de metadados, marque a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.  
  
    Por exemplo, para atualizar os metadados de todos os bancos de dados, selecione a caixa ao lado de bancos de dados.  
  
3.  Clique com o botão direito do mouse em bancos de dados ou em um esquema ou banco de dados individual e selecione **sincronizar com Banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa na migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento entre os esquemas do MySQL e os esquemas e bancos de dados do SQL Server, consulte [mapeando bancos de dados MySQL para esquemas de SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Para personalizar as opções de configuração para os projetos, consulte [definir opções de projeto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeando MySQL e SQL Server tipos de dados &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Se você não precisar executar nenhuma dessas tarefas, poderá converter as definições do objeto de banco de dados MySQL em SQL Server definições de objeto. Para obter mais informações, consulte [convertendo bancos de dados MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados MySQL para SQL Server-BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
