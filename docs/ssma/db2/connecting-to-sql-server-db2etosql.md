---
title: Conectando ao SQL Server (DB2eToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: b59803cb-3cc6-41cc-8553-faf90851410e
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 26410a933c7432189f664c2b04d2b41e3e31c9c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298987"
---
# <a name="connecting-to-sql-server-db2etosql"></a>Conectando ao SQL Server (DB2eToSQL)
Migrar bancos de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 ou do Azure SQL DB que você deve se conectar a qualquer uma dessas instâncias de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando você se conectar, o SSMA obtém metadados sobre todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exibe metadados de banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados. O SSMA armazena informações sobre qual instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão conectados ao, mas não armazena as senhas.  
  
Sua conexão ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanece ativa até você fechar o projeto. Quando você reabrir o projeto, você deve se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se você quiser que uma conexão ativa com o servidor. Você pode trabalhar offline até que você carrega objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e migrar dados.  
  
Metadados sobre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não será sincronizado automaticamente. Em vez disso, para atualizar os metadados na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, você deve atualizar manualmente o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados. Para obter mais informações, consulte o "Sincronizando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados" seção mais adiante neste tópico.  
  
## <a name="required-sql-server-permissions"></a>Permissões de servidor necessários do SQL  
A conta que é usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exige permissões diferentes, dependendo das ações que executa a conta:  
  
-   Para converter objetos DB2 [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, para atualizar os metadados da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ou para salvar a sintaxe convertido em scripts, a conta deve ter permissão para fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Carregar objetos de banco de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a conta deve ser um membro do **sysadmin** função de servidor. Isso é necessário para instalar assemblies do CLR.  
  
-   A migração de dados a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a conta deve ser um membro do **sysadmin** função de servidor. Isso é necessário para executar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pacotes de migração de dados do agente.  
  
-   Para executar o código que é gerado pelo SSMA, a conta deve ter **Execute** permissões para todas as funções definidas pelo usuário na **ssma_DB2** esquema do banco de dados de destino. Essas funções fornecem funcionalidade equivalente de funções de sistema do DB2 e são usadas por objetos convertidos.  
  
Se a conta que é usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é para executar a migração de todas as tarefas, a conta deve ser um membro do **sysadmin** função de servidor.  
  
## <a name="establishing-a-sql-server-connection"></a>Estabelecer uma Conexão de servidor SQL  
Antes de converter objetos de banco de dados DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe, você deve estabelecer uma conexão à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde você deseja migrar os bancos de dados ou banco de dados DB2.  
  
Quando você define as propriedades de conexão, você também especificar o banco de dados onde objetos e dados serão migrados. Você pode personalizar esse mapeamento no nível de esquema do DB2 depois de conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [mapeando esquemas do DB2 para esquemas SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md).  
  
> [!IMPORTANT]  
> Antes de tentar se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verifique se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução e pode aceitar conexões.  
  
**Para se conectar ao SQL Server**  
  
1.  Sobre o **arquivo** menu, selecione **conectar ao SQL Server**.  
  
    Se conectado anteriormente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o nome do comando será **reconectar-se ao SQL Server**.  
  
2.  Na caixa de diálogo de conexão, insira ou selecione o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Se você estiver se conectando à instância padrão no computador local, você pode inserir **localhost** ou um ponto ( **.** ).  
  
    -   Se você estiver se conectando à instância padrão em outro computador, digite o nome do computador.  
  
    -   Se você estiver se conectando a uma instância nomeada em outro computador, insira o nome do computador seguido por uma barra invertida e, em seguida, o nome de instância, como MyServer\MyInstance.  
  
3.  Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para aceitar conexões em uma porta não padrão, insira o número da porta que é usado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexões na **porta do servidor** caixa. Para a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o número da porta padrão é 1433. Para instâncias nomeadas, o SSMA tentará obter o número da porta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço localizador.  
  
4.  No **banco de dados** , digite o nome do banco de dados de destino.  
  
    Essa opção não está disponível quando você se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  No **autenticação** , selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta atual do Windows, selecione **autenticação do Windows**. Para usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login, selecione **autenticação do SQL Server**e, em seguida, forneça o nome de logon e senha.  
  
6.  Para uma conexão segura, dois controles são adicionados, o **criptografar Conexão** e **TrustServerCertificate** caixas de seleção. Somente quando **criptografar Conexão** estiver marcada, o **TrustServerCertificate** caixa de seleção está visível. Quando **criptografar Conexão** estiver marcada (true) e **TrustServerCertificate** está desmarcado (false), ele validará o certificado SSL do SQL Server. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para garantir isso, um certificado deve ser instalado no lado do cliente, bem como no lado do servidor.  
  
7.  Clique em **Conectar**.  
  
**Maior compatibilidade de versão**  
  
-   Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto de migração criado é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto de migração criado é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, mas não será capaz de se conectar a versões anteriores, ou seja, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Você poderá se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto criado é o SQL Server 2012.  
  
||||||  
|-|-|-|-|-|  
|**VERSÃO do servidor de destino do projeto tipo Vs**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Version:13.x)|Azure SQL DB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014|||Sim||  
|Azure SQL DB||||Sim|  
  
> [!IMPORTANT]  
> Conversão dos objetos de banco de dados é executada, de acordo com o tipo de projeto, mas não de acordo com a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] você está conectado. No caso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados SQL 2016 ou do Azure.  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizando os metadados do SQL Server  
Metadados sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados não são atualizados automaticamente. Os metadados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados é um instantâneo dos metadados quando você conectou primeiro à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ou a última vez em que você metadados atualizados manualmente. Você pode atualizar manualmente os metadados para todos os bancos de dados ou para qualquer banco de dados individual ou um objeto de banco de dados.  
  
**Para sincronizar os metadados**  
  
1.  Certifique-se de que você está conectado à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, marque a caixa de seleção ao lado do banco de dados ou que você deseja atualizar o esquema de banco de dados.  
  
    Por exemplo, para atualizar os metadados para todos os bancos de dados, marque a caixa próxima **bancos de dados**.  
  
3.  Clique com botão direito **bancos de dados**, ou o banco de dados individual ou esquema de banco de dados e selecione **sincronizar com o banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa da migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento entre os esquemas do DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados e esquemas, consulte [mapeamento de esquemas do DB2 para esquemas SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-schemas-to-sql-server-schemas-db2tosql.md).  
  
-   Para personalizar opções de configuração para os projetos, consulte [configurações do projeto &#40;conversão&#41; &#40;DB2ToSQL&#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md) e seções relacionadas.  
  
-   Para personalizar o mapeamento de tipos de dados de origem e destino, consulte [DB2 de mapeamento e tipos de dados do SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
-   Se você não precisa executar qualquer uma dessas tarefas, você pode converter as definições de objeto de banco de dados do DB2 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definições de objeto. Para obter mais informações, consulte [converter esquemas do DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
## <a name="see-also"></a>Consulte também  
[Bancos de dados do DB2 migrando para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
