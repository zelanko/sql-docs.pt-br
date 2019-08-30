---
title: managed_backup.fn_get_health_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_get_health_status_TSQL
- smart_admin.fn_get_health_status_TSQL
- smart_admin.fn_get_health_status
- fn_get_health_status
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_get_health_status
- fn_get_health_status
ms.assetid: b376711d-444a-4b5e-b483-8df323b4e31f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bc2bfdbd8714bf4211373e921c1b054ed224feb3
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155811"
---
# <a name="managed_backupfn_get_health_status-transact-sql"></a>managed_backup.fn_get_health_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Retorna uma tabela 0, uma ou mais linhas de contagem agregada dos erros relatados pelos Eventos Estendidos por um período especificado.  
  
 A função é usada para relatar o status de integridade dos serviços em administrador inteligente.  No [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] momento, há suporte para a proteção do administrador inteligente. Portanto, os erros retornados são relacionados a [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
managed_backup.fn_get_health_status([@begin_time = ] 'time_1' , [ @end_time = ] 'time_2')  
```  
  
##  <a name="Arguments"></a> Argumentos  
 [@begin_time]  
 O início do período a partir do qual a contagem agregada de erros é calculada.  O @begin_time parâmetro é DateTime. O valor padrão é NULL. Quando o valor for NULL, a função processará os eventos reportados a partir de 30 minutos antes da hora atual.  
  
 [ @end_time]  
 O fim do período a partir do qual a contagem agregada de erros é calculada. O @end_time parâmetro é DateTime com um valor padrão de NULL. Quando o valor for NULL, a função processará os eventos estendidos até a hora atual.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|number_of_storage_connectivity_errors|int|Número de erros de conexão quando o programa se conecta à conta de armazenamento do Azure.|  
|number_of_sql_errors|int|O número de erros retornados quando o programa se conectar ao SQL Server Engine.|  
|number_of_invalid_credential_errors|int|O número de erros retornados quando o programa tentar realizar a autenticação usando Credenciais SQL.|  
|number_of_other_errors|int|Número de erros em outras categorias, além de conectividade, SQL ou credencial.|  
|number_of_corrupted_or_deleted_backups|int|Número de arquivos de backup excluídos ou corrompidos.|  
|number_of_backup_loops|int|O número de vezes que o agente de backup verifica todos os bancos de dados configurados com o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].|  
|number_of_retention_loops|int|O número de vezes que os bancos de dados são verificados para avaliar o período de retenção definido.|  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Essas contagens agregadas podem ser usadas para monitorar a integridade do sistema. Por exemplo, se a coluna number_ of_retention_loops for 0 por 30 minutos, possivelmente o gerenciamento de retenção está demorando ou talvez nem esteja funcionando corretamente. As colunas de erro diferentes de zero podem indicar problemas, e os logs dos Eventos estendidos devem ser verificados para detectar qualquer problema. Como alternativa, use o procedimento armazenado **managed_backup. sp_get_backup_diagnostics** para obter uma lista de eventos estendidos para localizar os detalhes do erro.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer permissões **Select** na função.  
  
## <a name="examples"></a>Exemplos  
  
-   O exemplo a seguir retorna contagens de erro agregadas referentes aos últimos 30 minutos a partir do momento em que foram executadas.  
  
    ```  
    SELECT *  
    FROM managed_backup.fn_get_health_status(NULL, NULL)  
  
    ```  
  
-   O exemplo a seguir retorna as contagens de erro agregadas referente à semana atual:  
  
    ```  
    Use msdb  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
    SELECT *  
    FROM managed_backup.fn_get_health_status(@startofweek, @endofweek)  
  
    ```  
  
  
