---
title: Habilitar e desabilitar o Change Data Capture (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: track-changes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- change data capture [SQL Server], enabling tables
- change data capture [SQL Server], enabling databases
- change data capture [SQL Server], disabling databases
- change data capture [SQL Server], disabling tables
ms.assetid: b741894f-d267-4b10-adfe-cbc14aa6caeb
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 86c13345caa59dfb4ef9dad6f9c9cdb0ea324472
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="enable-and-disable-change-data-capture-sql-server"></a>Habilitar e desabilitar o Change Data Capture (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Este tópico descreve como habilitar e desabilitar o Change Data Capture para um banco de dados e uma tabela.  
  
## <a name="enable-change-data-capture-for-a-database"></a>Habilitar o Change Data Capture para um banco de dados  
 Para que uma instância de captura possa ser criada para tabelas individuais, um membro da função fixa de servidor **sysadmin** deve primeiro habilitar o banco de dados para a captura de dados de alteração. Isso é feito usando o procedimento armazenado [sys.sp_cdc_enable_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md) no contexto de banco de dados. Para determinar se um banco de dados está habilitado, consulte a coluna **is_cdc_enabled** na exibição de catálogo **sys.databases**.  
  
 Quando um banco de dados está habilitado para a captura de dados de alteração, o esquema **cdc** , usuário **cdc** , as tabelas de metadados e outros objetos de sistema são criados para o banco de dados. O esquema **cdc** contém as tabelas de metadados da captura de dados de alteração e, depois que as tabelas de origem são habilitadas para a captura de dados de alteração, as tabelas de alterações individuais atuam como repositório para os dados de alteração. O esquema **cdc** também contém funções de sistema associadas usadas para consultar dados de alteração.  
  
 A captura de dados de alteração requer o uso exclusivo do esquema **cdc** e do usuário **cdc** . Se um esquema ou usuário de banco de dados denominado *cdc* existir atualmente em um banco de dados, o banco de dados não poderá ser habilitado para Change Data Capture até que o esquema e/ou o usuário sejam descartados ou renomeados.  
  
 Consulte o modelo Habilitar Banco de dados para Change Data Capture para obter um exemplo de como habilitar um banco de dados.  
  
> [!IMPORTANT]  
>  Para localizar os modelos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], vá para **Exibir**, clique em **Explorador de Modelos**e selecione **Modelos do SQL Server**. **Change Data Capture** é uma subpasta. Nesta pasta, você encontrará todos os modelos referenciados neste tópico. Também há um ícone do **Explorador de Modelos** na barra de ferramentas [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
```sql  
-- ====  
-- Enable Database for CDC template   
-- ====  
USE MyDB  
GO  
EXEC sys.sp_cdc_enable_db  
GO  
```  
  
## <a name="disable-change-data-capture-for-a-database"></a>Desabilitar o Change Data Capture para um banco de dados  
 Um membro da função de servidor fixa **sysadmin** pode executar o procedimento armazenado [sys.sp_cdc_disable_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) no contexto de banco de dados para desabilitar a captura de dados de alterações de um banco de dados. Não é necessário desabilitar tabelas individuais antes de desabilitar o banco de dados. A desabilitação do banco de dados removerá todos os metadados de captura de dados de alteração associados, inclusive o usuário **cdc** e o esquema e os trabalhos da captura de dados de alteração. No entanto, qualquer função associada criada pelo Change Data Capture não será removida automaticamente e deverá ser excluída explicitamente. Para determinar se um banco de dados está habilitado, consulte a coluna **is_cdc_enabled** na exibição de catálogo sys.databases.  
  
 Se um banco de dados habilitado do Change Data Capture for descartado, os trabalhos de Change Data Capture serão removidos automaticamente.  
  
 Consulte o modelo Desabilitar Banco de dados para Change Data Capture para obter um exemplo de como desabilitar um banco de dados.  
  
> [!IMPORTANT]  
>  Para localizar os modelos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], vá para **Exibir**, clique em **Explorador de Modelos**e em **Modelos do SQL Server**. **Change Data Capture** é uma subpasta na qual você encontrará todos os modelos referenciados neste tópico. Também há um ícone do **Explorador de Modelos** na barra de ferramentas [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
```sql  
-- =======  
-- Disable Database for Change Data Capture template   
-- =======  
USE MyDB  
GO  
EXEC sys.sp_cdc_disable_db  
GO  
```  
  
## <a name="enable-change-data-capture-for-a-table"></a>Habilitar o Change Data Capture para uma tabela  
 Após a habilitação de um banco de dados para captura de dados de alteração, os membros da função de banco de dados fixa **db_owner** poderão criar uma instância de captura para tabelas de origem individuais usando o procedimento armazenado **sys.sp_cdc_enable_table**. Para determinar se uma tabela de origem já foi habilitada para a captura de dados de alterações, examine a coluna is_tracked_by_cdc na exibição de catálogo **sys.tables** .  
  
 As seguintes opções podem ser especificadas durante a criação de uma instância de captura:  
  
 **Colunas na tabela de origem a serem capturadas**.  
  
 Por padrão, todas as colunas na tabela de origem são identificadas como colunas capturadas. Se for necessário rastrear apenas um subconjunto das colunas, por questões de privacidade ou desempenho, use o parâmetro *@captured_column_list* para especificar o subconjunto de colunas.  
  
 **Um grupo de arquivos para conter a tabela de alteração.**  
  
 Por padrão, a tabela de alteração está localizada no grupo de arquivos padrão do banco de dados. Proprietários de banco de dados que queiram controlar o posicionamento de tabelas de alterações individuais podem usar o parâmetro *@filegroup_name* para especificar determinado grupo de arquivos para a tabela de alterações associada à instância de captura. O grupo de arquivos nomeado já deve existir. Geralmente, é recomendável que tabelas de alterações sejam colocadas em um grupo de arquivos separado das tabelas de origem. Confira o modelo **Habilitar uma tabela especificando a opção de grupo de arquivos** para obter um exemplo que mostra o uso do parâmetro *@filegroup_name* .  
  
```sql  
-- =========  
-- Enable a Table Specifying Filegroup Option Template  
-- =========  
USE MyDB  
GO  
  
EXEC sys.sp_cdc_enable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@role_name     = N'MyRole',  
@filegroup_name = N'MyDB_CT',  
@supports_net_changes = 1  
GO  
```  
  
 **Uma função para controlar o acesso a uma tabela de alteração.**  
  
 O propósito da função nomeada é controlar o acesso aos dados de alteração. A função especificada pode ser uma função de servidor fixa existente ou uma função de banco de dados. Se a função especificada ainda não existir, uma função de banco de dados com esse nome será criada automaticamente. Os membros da função **sysadmin** ou **db_owner** têm acesso completo aos dados nas tabelas de alterações. Todos os outros usuários devem ter a permissão SELECT em todas as colunas capturadas da tabela de origem. Além disso, quando uma função é especificada, os usuários que não são membros da função **sysadmin** ou **db_owner** também devem ser membros da função especificada.  
  
 Se você não quiser usar uma função associada, defina explicitamente o parâmetro *@role_name* como NULL. Confira o modelo **Habilitar uma tabela sem uma função associada** para obter um exemplo de como habilitar uma tabela sem uma função associada.  
  
```sql  
-- =========  
-- Enable a Table Without Using a Gating Role template   
-- =========  
USE MyDB  
GO  
EXEC sys.sp_cdc_enable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@role_name     = NULL,  
@supports_net_changes = 1  
GO  
  
```  
  
 **Uma função para consultar alterações líquidas.**  
  
 Uma instância de captura sempre incluirá uma função com valor de tabela para retornar todas as entradas de tabela de alterações que ocorreram dentro de um intervalo definido. Essa função é denominada com a anexação do nome da instância de captura para "cdc.fn_cdc_get_all_changes_". Para obter mais informações, veja [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md).  
  
 Se o parâmetro *@supports_net_changes* for definido como 1, uma função de alterações globais também será gerada para a instância de captura. Essa função retorna apenas uma alteração para cada linha distinta alterada no intervalo especificado na chamada. Para obter mais informações, veja [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md).  
  
 Para dar suporte às consultas de entradas, a tabela de origem deve ter uma chave primária ou índice exclusivo para identificar linhas. Se um índice exclusivo for usado, o nome do índice deverá ser especificado com o uso do parâmetro *@index_name* . As colunas definidas na chave primária ou índice exclusivo deverão ser incluídas na lista de colunas de origem a serem capturadas.  
  
 Confira o modelo **Habilitar uma tabela para tudo e consultas de alterações líquidas** para obter um exemplo que demonstra a criação de uma instância de captura com ambas as funções de consulta.  
  
```sql  
-- =============  
-- Enable a Table for All and Net Changes Queries template   
-- =============  
USE MyDB  
GO  
EXEC sys.sp_cdc_enable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@role_name     = N'MyRole',  
@supports_net_changes = 1  
GO  
```  
  
> [!NOTE]  
>  Se a captura de dados de alterações for habilitada em uma tabela com a chave primária existente e o parâmetro *@index_name* não for usado para identificar um índice exclusivo alternativo, o recurso captura de dados de alterações usará a chave primária. Alterações subsequentes à chave primária não serão permitidas sem a desabilitação primeiro do Change Data Capture para a tabela. Isso é verdadeiro quer o suporte para consultas de alterações globais tenha sido solicitado ou não durante a configuração do Change Data Capture. Se não houver nenhuma chave primária em uma tabela quando ela for habilitada para o Change Data Capture, a adição subsequente de uma chave primária será ignorada pelo Change Data Capture. Como o Change Data Capture não usará uma chave primária criada após a habilitação da tabela, a chave e as colunas de chave poderão ser removidas sem restrições.  
  
## <a name="disable-change-data-capture-for-a-table"></a>Desabilitar o Change Data Capture para uma tabela  
 Os membros da função de banco de dados fixa **db_owner** podem remover uma instância de captura para tabelas de origem individuais usando o procedimento armazenado **sys.sp_cdc_disable_table**. Para determinar se uma tabela de origem no momento está habilitada para a captura de dados de alteração, examine a coluna **is_tracked_by_cdc** na exibição de catálogo **sys.tables** . Se não houver tabelas habilitadas para o banco de dados após a desabilitação, os trabalhos do Change Data Capture também serão removidos.  
  
 Se uma tabela habilitado do Change Data Capture for descartada, os metadados associados à tabela de Change Data Capture serão removidos automaticamente.  
  
 Consulte o modelo Desabilitar uma Instância de Captura para uma Tabela para obter um exemplo de como desabilitar uma tabela.  
  
```sql  
-- =====  
-- Disable a Capture Instance for a Table template   
-- =====  
USE MyDB  
GO  
EXEC sys.sp_cdc_disable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@capture_instance = N'dbo_MyTable'  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Controle de alterações de dados &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [Trabalhar com dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)   
 [Administrar e monitorar a captura de dados de alteração &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
