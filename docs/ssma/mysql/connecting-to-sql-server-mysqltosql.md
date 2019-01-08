---
title: Conectando ao SQL Server (MySQLToSQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 64dd3fae9776c09f81571a721aa53753e34fbb17
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52412283"
---
# <a name="connecting-to-sql-server-mysqltosql"></a>Conectar-se ao SQL Server (MySQLToSQL)
Para migrar bancos de dados MySQL para o SQL Server, você deve se conectar à instância de destino do SQL Server. Quando você se conectar, o SSMA obtém metadados sobre todos os bancos de dados na instância do SQL Server e exibe metadados de banco de dados no Pesquisador de metadados do SQL Server. O SSMA armazena as informações da instância do SQL Server está conectado ao, mas não armazena as senhas.  
  
Sua conexão ao SQL Server permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve se reconectar ao SQL Server se você quiser que uma conexão ativa com o servidor. Você pode trabalhar offline até que você carregar objetos de banco de dados no SQL Server e migra os dados.  
  
Metadados sobre a instância do SQL Server não será sincronizado automaticamente. Em vez disso, para atualizar os metadados no Gerenciador de metadados do SQL Server, você deve atualizar manualmente os metadados do SQL Server. Para obter mais informações, consulte a seção "Sincronização de metadados do SQL Server", mais adiante neste tópico.  
  
## <a name="required-sql-server-permissions"></a>Permissões de servidor necessários do SQL  
A conta que é usada para se conectar ao SQL Server exige permissões diferentes, dependendo das ações que executa a conta:  
  
-   Para converter objetos do MySQL para [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts de sintaxe, para atualizar os metadados do SQL Server ou para salvar a sintaxe a ser convertido, a conta deve ter permissão para fazer logon na instância do SQL Server.  
  
-   Para carregar objetos de banco de dados no SQL Server, o requisito mínimo de permissão é a associação à **db_owner** função de banco de dados no banco de dados de destino.  
  
## <a name="establishing-a-sql-server-connection"></a>Estabelecer uma Conexão de servidor SQL  
Antes de converter objetos de banco de dados MySQL para sintaxe do SQL Server, você deve estabelecer uma conexão à instância do SQL Server em que você deseja migrar o banco de dados MySQL ou bancos de dados.  
  
Quando você define as propriedades de conexão, você também especificar o banco de dados onde objetos e dados serão migrados. Você pode personalizar esse mapeamento no nível de esquema MySQL depois de se conectar ao SQL Server. Para obter mais informações, consulte [mapeamento de bancos de dados MySQL para esquemas SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
> [!IMPORTANT]  
> Antes de tentar se conectar ao SQL Server, certifique-se de que a instância do SQL Server está em execução e pode aceitar conexões.  
  
**Para se conectar ao SQL Server**  
  
1.  Sobre o **arquivo** menu, selecione **conectar ao SQL Server** (essa opção é habilitada após a criação de um projeto).  
  
    Se você tiver se conectado anteriormente ao SQL Server, o nome do comando será **reconectar-se ao SQL Server**.  
  
2.  Na caixa de diálogo de conexão, insira ou selecione o nome da instância do SQL Server.  
  
    -   Se você estiver se conectando à instância padrão no computador local, você pode inserir **localhost** ou um ponto (**.**).  
  
    -   Se você estiver se conectando à instância padrão em outro computador, digite o nome do computador.  
  
    -   Se você estiver se conectando a uma instância nomeada em outro computador, insira o nome do computador seguido por uma barra invertida e, em seguida, o nome de instância, como MyServer\MyInstance.  
  
3.  Se sua instância do SQL Server está configurada para aceitar conexões em uma porta não padrão, insira o número da porta que é usado para conexões do SQL Server no **porta do servidor** caixa. Para a instância padrão do SQL Server, o número da porta padrão é 1433. Para instâncias nomeadas, o SSMA tentará obter o número da porta do serviço navegador do SQL Server.  
  
4.  No **autenticação** , selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta atual do Windows, selecione **autenticação do Windows**. Para usar um logon do SQL Server, selecione autenticação do SQL Server e, em seguida, forneça o nome de logon e senha.  
  
5.  Para uma conexão segura, dois controles são adicionados, o **criptografar Conexão** e **TrustServerCertificate** caixas de seleção. Somente quando **criptografar Conexão** estiver marcada, o **TrustServerCertificate** caixa de seleção está visível. Quando **criptografar Conexão** estiver marcada (true) e **TrustServerCertificate** está desmarcado (false), ele validará o certificado SSL do SQL Server. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para garantir isso, um certificado deve ser instalado no lado do cliente, bem como no lado do servidor.  
  
6.  Clique em Conectar.  
  
**Maior compatibilidade de versão**  
  
Ele tem permissão para conectar-se/reconectar-se para versões superiores do SQL Server.  
  
1.  Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto criado é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
2.  Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto criado é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, mas ele não tem permissão para se conectar a versões anteriores ou seja, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
3.  Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto criado é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012.  
  
4.  Você poderá se conectar a apenas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto criado é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014.  
  
5.  Maior compatibilidade de versão não é válida para "do SQL Azure".  
  
||||||||  
|-|-|-|-|-|-|-|  
|**VERSÃO do servidor de destino do projeto tipo Vs**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (Versão: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (Versão: 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012<br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014<br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016<br />(Version:13.x)|SQL Azure|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|Sim|Sim|Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||Sim|Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016|||||Sim||  
|SQL Azure||||||Sim|  
  
> [!IMPORTANT]  
> Conversão dos objetos de banco de dados é executada, de acordo com o tipo de projeto, mas não de acordo com a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conectado ao. No caso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] projeto de 2005, conversão é executada de acordo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 mesmo que você está conectado a uma versão posterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizando os metadados do SQL Server  
Metadados sobre bancos de dados do SQL Server não é atualizado automaticamente. Os metadados no Gerenciador de metadados do SQL Server são um instantâneo dos metadados quando você primeiro conectado ao SQL Server ou a última vez que você manualmente atualizado metadados. Você pode atualizar manualmente os metadados para todos os bancos de dados ou para qualquer banco de dados individual ou um objeto de banco de dados.  
  
**Para sincronizar os metadados**  
  
1.  Certifique-se de que você está conectado ao SQL Server.  
  
2.  No Gerenciador de metadados do SQL Server, marque a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.  
  
    Por exemplo, para atualizar os metadados para todos os bancos de dados, marque a caixa ao lado de bancos de dados.  
  
3.  Bancos de dados, ou o banco de dados individual ou o esquema de banco de dados e, em seguida, selecione **sincronizar com o banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento entre esquemas de MySQL e bancos de dados do SQL Server e esquemas, consulte [mapeamento de bancos de dados MySQL para esquemas SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
-   Para personalizar opções de configuração para os projetos, consulte [definir opções do projeto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)  
  
-   Para personalizar o mapeamento de tipos de dados de origem e destino, consulte [MySQL de mapeamento e tipos de dados do SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
-   Se você não precisa executar qualquer uma dessas tarefas, você pode converter as definições de objeto de banco de dados MySQL em definições de objeto do SQL Server. Para obter mais informações, consulte [conversão de bancos de dados MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando MySQL bancos de dados para o SQL Server – BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
