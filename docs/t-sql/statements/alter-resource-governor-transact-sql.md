---
title: ALTER RESOURCE GOVERNOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER RESOURCE GOVERNOR
- ALTER_RESOURCE_GOVERNOR_TSQL
- ALTER RESOURCE GOVERNOR RECONFIGURE
- ALTER_RESOURCE_GOVERNOR_RECONFIGURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER RESOURCE GOVERNOR
- RECONFIGURE, ALTER RESOURCE GOVERNOR
ms.assetid: 442c54bf-a0a6-4108-ad20-db910ffa6e3c
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 312448ec80ce4f63a62cba9bee1db251655c7835
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="alter-resource-governor-transact-sql"></a>ALTER RESOURCE GOVERNOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Essa instrução é usada para executar as seguintes ações do Resource Governor no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Aplicar as alterações de configuração especificadas quando as instruções CREATE|ALTER|DROP WORKLOAD GROUP ou CREATE|ALTER|DROP RESOURCE POOL ou CREATE|ALTER|DROP EXTERNAL RESOURCE POOL forem emitidas.  
  
-   Habilitar ou desabilitar o Administrador de Recursos.  
  
-   Configurar a classificação de solicitações de entrada.  
  
-   Reiniciar o grupo de carga de trabalho e as estatísticas de pool de recursos.  
  
-   Define o máximo de operações de E/S por volume de disco.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER RESOURCE GOVERNOR   
      { DISABLE | RECONFIGURE }  
    | WITH ( CLASSIFIER_FUNCTION = { schema_name.function_name | NULL } )  
    | RESET STATISTICS  
    | WITH ( MAX_OUTSTANDING_IO_PER_VOLUME = value )   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 DISABLE  
 Desabilita o Administrador de Recursos. A desabilitação do Resource Governor gera os seguintes resultados:  
  
-   A função classificadora não é executada.  
  
-   Todas as conexões novas são automaticamente classificadas no grupo padrão.  
  
-   As solicitações iniciadas pelo sistema são classificadas no grupo de cargas de trabalho interno.  
  
-   Todas as configurações existentes do grupo de carga de trabalho e do pool de recursos são redefinidas para os valores padrão. Nesse caso, nenhum evento é acionado quando os limites são atingidos.  
  
-   O monitoramento normal do sistema não é afetado.  
  
-   As alterações de configuração podem ser feitas, mas as alterações não terão efeito até que o Resource Governor seja habilitado.  
  
-   Depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for reiniciado, o Administrador de Recursos não carregará sua configuração, mas em vez disso terá apenas os grupos e pools padrão e internos.  
  
 RECONFIGURE  
 Quando o Administrador de Recursos não está habilitado, RECONFIGURE habilita o Administrador de Recursos. A habilitação do Administrador de Recursos gera os seguintes resultados:  
  
-   A função de classificação é executada para conexões novas, de forma que a carga de trabalho possa ser atribuída a grupos de cargas de trabalho.  
  
-   Os limites de recursos especificados na configuração do Administrador de Recursos são cumpridos e impostos.  
  
-   As solicitações existentes antes da habilitação do Resource Governor são afetadas pelas alterações feitas na configuração quando o Resource Governor foi desabilitado.  
  
 Quando o Resource Governor estiver sendo executado, RECONFIGURE aplicará qualquer alteração de configuração solicitada quando as instruções CREATE|ALTER|DROP WORKLOAD GROUP or CREATE|ALTER|DROP RESOURCE POOL or CREATE|ALTER|DROP EXTERNAL RESOURCE POOL forem executadas.  
  
> [!IMPORTANT]  
>  ALTER RESOURCE GOVERNOR RECONFIGURE deve ser emitida para que qualquer alteração de configuração entre em vigor.  
  
 CLASSIFIER_FUNCTION = { *schema_name ***.*** function_name* | NULL }  
 Registra a função de classificação especificada por *schema_name.function_name*. Essa função classifica cada sessão nova e atribui as solicitações e consultas de sessão a um grupo de carga de trabalho. Quando NULL é usado, novas sessões são automaticamente atribuídas ao grupo de carga de trabalho padrão.  
  
 RESET STATISTICS  
 Redefine as estatísticas em todos os grupos de carga de trabalho e pools de recursos. Para obter mais informações, consulte [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md) e [sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md).  
  
 MAX_OUTSTANDING_IO_PER_VOLUME = *value*  
 **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Define o máximo de operações de E/S na fila por volume de disco. Essas operações de E/S podem ser leituras ou gravações de qualquer tamanho.  O valor máximo para MAX_OUTSTANDING_IO_PER_VOLUME é 100. Não é uma porcentagem. Essa configuração é criada para ajustar a administração do recurso de E/S às características de E/S de um volume de disco. Recomendamos fazer experiências com valores diferentes e considerar o uso de uma ferramenta de calibração como o IOMeter, [DiskSpd](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223) ou SQLIO (preterido) para identificar o valor máximo do subsistema de armazenamento. Essa configuração fornece uma verificação de segurança no nível do sistema que permite ao SQL Server atender ao mínimo de IOPS para pools de recursos mesmo se outros pools tiverem o MAX_IOPS_PER_VOLUME definido como ilimitado. Para obter mais informações sobre MAX_IOPS_PER_VOLUME, consulte [CREATE RESOURCE POOL](../../t-sql/statements/create-resource-pool-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 ALTER RESOURCE GOVERNOR DISABLE, ALTER RESOURCE GOVERNOR RECONFIGURE, e ALTER RESOURCE GOVERNOR RESET STATISTICS não podem ser usados em uma transação de usuário.  
  
 O parâmetro RECONFIGURE faz parte da sintaxe do Resource Governor e não deve ser confundido com [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md), que é uma instrução DDL separada.  
  
 Recomendamos que você esteja familiarizado com os estados do Administrador de recursos antes de executar as instruções DDL. Para obter mais informações, consulte [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-starting-the-resource-governor"></a>A. Iniciando o Administrador de Recursos  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for instalado primeiro, o Administrador de recursos será desabilitado. O exemplo a seguir inicia o Administrador de Recursos. Depois de executada a instrução, o Administrador de Recursos está em execução e pode usar os grupos de cargas de trabalho e pools de recursos predefinidos.  
  
```  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
```  
  
### <a name="b-assigning-new-sessions-to-the-default-group"></a>B. Atribuindo novas sessões ao grupo padrão  
 O exemplo a seguir atribui todas as sessões novas ao grupo de carga de trabalho padrão, removendo qualquer função de classificação existente da configuração do Administrador de Recursos. Quando nenhuma função é designada como uma função de classificação, todas as sessões novas são atribuídas ao grupo de carga de trabalho padrão. Essa alteração só se aplica a sessões novas. As sessões existentes não são afetadas.  
  
```  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION = NULL);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
```  
  
### <a name="c-creating-and-registering-a-classifier-function"></a>C. Criando e registrando uma função de classificação  
 O exemplo a seguir cria uma função de classificação chamada `dbo.rgclassifier_v1`. A função classifica cada sessão nova com base no nome de usuário ou nome de aplicativo e atribui as consultas e solicitações de sessão a um grupo de carga de trabalho específico. As sessões que não são mapeadas para o usuário especificado ou nomes de aplicativos são atribuídas ao grupo de carga de trabalho padrão. A função de classificação é registrada e a alteração de configuração é aplicada.  
  
```  
-- Store the classifier function in the master database.  
USE master;  
GO  
SET ANSI_NULLS ON;  
GO  
SET QUOTED_IDENTIFIER ON;  
GO  
CREATE FUNCTION dbo.rgclassifier_v1() RETURNS sysname   
WITH SCHEMABINDING  
AS  
BEGIN  
-- Declare the variable to hold the value returned in sysname.  
    DECLARE @grp_name AS sysname  
-- If the user login is 'sa', map the connection to the groupAdmin  
-- workload group.   
    IF (SUSER_NAME() = 'sa')  
        SET @grp_name = 'groupAdmin'  
-- Use application information to map the connection to the groupAdhoc  
-- workload group.  
    ELSE IF (APP_NAME() LIKE '%MANAGEMENT STUDIO%')  
        OR (APP_NAME() LIKE '%QUERY ANALYZER%')  
            SET @grp_name = 'groupAdhoc'  
-- If the application is for reporting, map the connection to  
-- the groupReports workload group.  
    ELSE IF (APP_NAME() LIKE '%REPORT SERVER%')  
        SET @grp_name = 'groupReports'  
-- If the connection does not map to any of the previous groups,  
-- put the connection into the default workload group.  
    ELSE  
        SET @grp_name = 'default'  
    RETURN @grp_name  
END;  
GO  
-- Register the classifier user-defined function and update the   
-- the in-memory configuration.  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION=dbo.rgclassifier_v1);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
### <a name="d-resetting-statistics"></a>D. Redefinindo as estatísticas  
 O exemplo a seguir redefine todas as estatísticas do grupo de carga de trabalho e pool de recursos.  
  
```  
ALTER RESOURCE GOVERNOR RESET STATISTICS;  
```  
  
### <a name="e-setting-the-maxoutstandingiopervolume-option"></a>E. Definindo a opção de MAX_OUTSTANDING_IO_PER_VOLUME  
 O exemplo a seguir define a opção de MAX_OUTSTANDING_IO_PER_VOLUME para 20.  
  
```  
ALTER RESOURCE GOVERNOR  
WITH (MAX_OUTSTANDING_IO_PER_VOLUME = 20);   
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [Administrador de Recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)   
 [sys.dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)  
  
  
