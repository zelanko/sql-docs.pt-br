---
title: "Solu&#231;&#227;o de problemas de configura&#231;&#227;o de espelhamento de banco de dados (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "espelhamento de banco de dados [SQL Server], implantação"
  - "pontos de extremidade, [SQL Server], espelhamento de banco de dados"
  - "espelhamento de banco de dados [SQL Server], solução de problemas"
  - "solução de problemas, [SQL Server], espelhamento de banco de dados"
ms.assetid: 87d3801b-dc52-419e-9316-8b1f1490946c
caps.latest.revision: 69
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 69
---
# Solu&#231;&#227;o de problemas de configura&#231;&#227;o de espelhamento de banco de dados (SQL Server)
  Este tópico fornece informações para ajudá-lo a solucionar problemas ao configurar uma sessão de espelhamento de banco de dados.  
  
> [!NOTE]  
>  Verifique se você atende a todos os [pré-requisitos do espelhamento de banco de dados](../../database-engine/database-mirroring/prerequisites-restrictions-and-recommendations-for-database-mirroring.md).  
  
|Problema|Resumo|  
|-----------|-------------|  
|Mensagem de erro 1418|Essa mensagem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indica que o endereço de rede de servidor não pode ser alcançado ou pode não existir, e sugere que você verifique o nome de endereço de rede e emita novamente o comando. Para obter mais informações, veja o tópico [MSSQLSERVER_1418](../Topic/MSSQLSERVER_1418.md).|  
|[Contas](#Accounts)|Discute os requisitos para configurar corretamente as contas nas quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será executado.|  
|[Pontos de extremidade](#Endpoints)|Discute os requisitos para configurar corretamente o ponto de extremidade do espelhamento de banco de dados de cada instância do servidor.|  
|[SystemAddress](#SystemAddress)|Resume as alternativas para especificar o nome de sistema de uma instância do servidor em uma configuração de espelhamento de banco de dados.|  
|[Acesso de rede](#NetworkAccess)|Documenta o requisito de cada instância do servidor para acessar as portas de outra instância do servidor ou instâncias no TCP.|  
|[Preparação do banco de dados espelho](#MirrorDbPrep)|Resume os requisitos para preparar o banco de dados espelho para habilitar o início do espelhamento.|  
|[Falha na operação para criar arquivo](#FailedCreateFileOp)|Descreve como responder a uma falha na operação para criar arquivo.|  
|[Iniciando o espelhamento usando Transact-SQL](#StartDbm)|Descreve a ordem exigida para as instruções ALTER DATABASE *nome_banco_dados* SET PARTNER **='***servidor_parceiro***'**.|  
|[Transações envolvendo todos os bancos de dados](#CrossDbTxns)|Um failover automático pode levar a uma resolução automática e possivelmente incorreta de transações duvidosas. Por esta razão, o espelhamento de banco de dados não dá suporte a transações envolvendo todos os bancos de dados.|  
  
##  <a name="Accounts"></a> Contas  
 As contas nas quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado devem ser configuradas corretamente.  
  
1.  As contas têm as permissões corretas?  
  
    1.  Se as contas estiverem sendo executadas nas mesmas contas de domínio, as chances de uma configuração incorreta são reduzidas.  
  
    2.  Se as contas estiverem executando em domínios diferentes ou não são contas de domínio, o logon de uma conta deve ser criado em **mestre** no outro computador e esse logon deve ter permissões concedidas em CONNECT no ponto de extremidade. Para obter mais informações, consulte [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage metadata when making a database available on another server.md). Isso inclui a conta de Serviço de Rede.  
  
2.  Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver executando como um serviço que está usando a conta Sistema Local, você deve usar certificados para autenticação. Para obter mais informações, consulte [Usar certificados para um ponto de extremidade do espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md).  
  
##  <a name="Endpoints"></a> Pontos de extremidade  
 Os pontos de extremidade devem ser configurados corretamente.  
  
1.  Verifique se cada instância do servidor (o servidor principal, servidor espelho e testemunha, se houver) tem um ponto de extremidade de espelhamento de banco de dados. Para obter mais informações, veja [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md) e, dependendo do formato de autenticação, [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md) ou [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md).  
  
2.  Verifique se os números da porta estão corretos.  
  
     Para identificar a porta atualmente associada ao ponto de extremidade do espelhamento de banco de dados de uma instância de servidor, use as exibições de catálogo [sys.database_mirroring_endpoints](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md) e [sys.tcp_endpoints](../../relational-databases/system-catalog-views/sys-tcp-endpoints-transact-sql.md).  
  
3.  Para os problemas da configuração de espelhamento de banco de dados que são difíceis de explicar, recomendamos que você inspecione cada instância do servidor para determinar se está escutando nas portas corretas. Para obter mais informações sobre como verificar a disponibilidade de porta, veja [MSSQLSERVER_1418](../Topic/MSSQLSERVER_1418.md).  
  
4.  Verifique se os pontos de extremidade foram iniciados (STATE=STARTED). Em cada instância do servidor, use a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
    ```  
    SELECT state_desc FROM sys.database_mirroring_endpoints  
    ```  
  
     Para obter mais informações sobre a coluna **state_desc**, veja [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md).  
  
     Para iniciar um ponto de extremidade, use a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
    ```  
    ALTER ENDPOINT Endpoint_Mirroring   
    STATE = STARTED   
    AS TCP (LISTENER_PORT = <port_number>)  
    FOR database_mirroring (ROLE = ALL);  
    GO  
    ```  
  
     Para obter mais informações, veja [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
5.  Verifique se o ROLE está correto. Em cada instância do servidor, use a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
    ```  
    SELECT role FROM sys.database_mirroring_endpoints;  
    GO  
    ```  
  
     Para obter mais informações, veja [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md).  
  
6.  O logon para a conta de serviço da outra instância de servidor exige permissão CONNECT. Verifique se o logon do outro servidor tem permissão CONNECT. Para determinar quem tem permissão CONNECT para um ponto de extremidade, em cada instância do servidor use a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] seguinte.  
  
    ```  
    SELECT 'Metadata Check';  
    SELECT EP.name, SP.STATE,   
       CONVERT(nvarchar(38), suser_name(SP.grantor_principal_id))   
          AS GRANTOR,   
       SP.TYPE AS PERMISSION,  
       CONVERT(nvarchar(46),suser_name(SP.grantee_principal_id))   
          AS GRANTEE   
       FROM sys.server_permissions SP , sys.endpoints EP  
       WHERE SP.major_id = EP.endpoint_id  
       ORDER BY Permission,grantor, grantee;   
    GO  
  
    ```  
  
##  <a name="SystemAddress"></a> Endereço de sistema  
 Para o nome de sistema de uma instância do servidor em uma configuração de espelhamento de banco de dados, você pode usar qualquer nome que inequivocamente identifique o sistema. O endereço de servidor pode ser um nome de sistema (se os sistemas estiverem no mesmo domínio), um nome de domínio totalmente qualificado ou um endereço de IP (preferivelmente, um endereço de IP estático). Usando o nome de domínio totalmente qualificado o funcionamento é garantido. Para obter mais informações, consulte [Especificar um endereço de rede do servidor &#40;Espelhamento de banco de dados&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md).  
  
##  <a name="NetworkAccess"></a> Acesso de rede  
 Cada instância do servidor deve poder acessar as portas da outra instância do servidor ou instâncias em TCP. Isso será especialmente importante se as instâncias do servidor estiverem em domínios diferentes que não confiam um no outro (domínios não confiáveis). Isso restringe muito da comunicação entre as instâncias do servidor.  
  
##  <a name="MirrorDbPrep"></a> Preparação do banco de dados espelho  
 Se iniciar o espelhamento pela primeira vez ou iniciá-lo novamente depois do espelhamento ser removido, verifique se o banco de dados espelho está preparado para o espelhamento.  
  
 Quando você criar o banco de dados espelho no servidor espelho, certifique-se de restaurar o backup do banco de dados principal especificando o mesmo nome de banco de dados WITH NORECOVERY. Além disso, deve-se aplicar também a todos os backups de log, criados depois que esse backup foi feito, WITH NORECOVERY novamente  
  
 Também recomendamos que, se possível, o caminho do arquivo (inclusive a letra da unidade) do banco de dados espelho seja idêntico ao caminho do banco de dados principal. Se os caminhos de arquivo precisarem ser diferentes, por exemplo, se o banco de dados principal estiver na unidade 'F': mas o sistema espelho não tiver uma unidade F:, será necessário incluir a opção MOVE na instrução RESTORE.  
  
> [!IMPORTANT]  
>  Se você mover os arquivos de banco de dados quando estiver criando o banco de dados espelho, pode não ser capaz de acrescentar arquivos posteriormente ao banco de dados sem a suspensão do espelhamento.  
  
 Se o espelhamento de banco de dados foi interrompido, todos os backups de logs subsequentes do banco de dados principal devem ser aplicados ao banco de dados espelho antes que o espelhamento possa ser reinicializado.  
  
 Para obter mais informações, consulte [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
##  <a name="FailedCreateFileOp"></a> Falha na operação criar arquivo  
 Para que a inclusão de um arquivo não afete uma sessão de espelhamento, o caminho do arquivo deve existir nos dois servidores. Portanto, se você mover os arquivos de banco de dados quando estiver criando o banco de dados espelho, uma operação adicionar arquivo posterior pode não funcionar no banco de dados espelho e causar a suspensão do espelhamento.  
  
 Para corrigir o problema:  
  
1.  O proprietário do banco de dados deve remover a sessão de espelhamento e restaurar o backup completo do grupo de arquivos que contém o arquivo adicionado.  
  
2.  O proprietário do banco de dados deve fazer backup do log que contém a operação adicionar arquivo no servidor principal e restaurar manualmente o backup do log no banco de dados espelho usando as opções WITH NORECOVERY e WITH MOVE. Isso criará o caminho de arquivo especificado no servidor espelho e irá restaurar o novo arquivo nesse local.  
  
3.  Para preparar o banco de dados para a nova sessão de espelhamento, o proprietário também deve restaurar usando WITH NORECOVERY todos os backups de log pendentes a partir do servidor principal.  
  
 Para obter mais informações, veja [Remover o espelhamento de banco de dados&#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md), [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md), [Estabelecer uma sessão de espelhamento de banco de dados com a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md), [Usar certificados para um ponto de extremidade do espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md) ou [Estabelecer uma sessão de espelhamento de banco de dados com a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish database mirroring session - windows authentication.md).  
  
##  <a name="StartDbm"></a> Iniciando o espelhamento usando Transact-SQL  
 A ordem na qual as instruções ALTER DATABASE *nome_banco_dados* SET PARTNER **='***servidor_parceiro***'** são emitidas é muito importante.  
  
1.  A primeira instrução deve ser executada no servidor espelho. Quando essa instrução for emitida, o servidor espelho não tenta contatar qualquer outra instância do servidor. Em vez disso, o servidor espelho instrui seu banco de dados para esperar até que o servidor espelho seja contatado pelo servidor principal.  
  
2.  A segunda instrução ALTER DATABASE deve ser executada no servidor principal. Essa instrução faz o servidor principal tentar se conectar ao servidor espelho. Depois que essa conexão é criada, o espelho, então, tenta conectar ao servidor principal em outra conexão.  
  
 Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
> [!NOTE]  
>  Para obter informações sobre como usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para iniciar o espelhamento, veja [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish database mirroring session - windows authentication.md).  
  
##  <a name="CrossDbTxns"></a> Transações envolvendo todos os bancos de dados  
 Quando um banco de dados está sendo espelhado no modo de alta-segurança com failover automático, um failover automático pode levar a uma resolução automática e possivelmente incorreta de transações incertas. Se um failover automático acontecer em qualquer banco de dados enquanto uma transação envolvendo todos os bancos de dados está sendo confirmada, poderão ocorrer inconsistências lógicas entre os bancos de dados.  
  
 Os tipos de transações envolvendo todos os bancos de dados que podem ser afetadas por um failover automático incluem o seguinte:  
  
-   Uma transação que está atualizando vários bancos de dados na mesma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Transações que usam MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)]).  
  
 Para obter mais informações, consulte [Transações entre bancos de dados e transações distribuídas para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions - always on availability and database mirroring.md).  
  
## Consulte também  
 [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [Segurança de transporte para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport security - database mirroring - always on availability.md)  
  
  