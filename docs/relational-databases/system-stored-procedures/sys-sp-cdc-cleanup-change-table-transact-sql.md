---
description: sys.sp_cdc_cleanup_change_table (Transact-SQL)
title: sys. sp_cdc_cleanup_change_table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_cleanup_change_table
- sp_cdc_cleanup_change_table_TSQL
- sys.sp_cdc_cleanup_change_table
- sys.sp_cdc_cleanup_change_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_cleanup_change_tables
- sp_cdc_cleanup_change_tables
ms.assetid: 02295794-397d-4445-a3e3-971b25e7068d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fe0e83a4a74be15c405da6b9a95456b71b46e2c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492855"
---
# <a name="syssp_cdc_cleanup_change_table-transact-sql"></a>sys.sp_cdc_cleanup_change_table (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Remove linhas da tabela de alteração no banco de dados atual com base no valor de *low_water_mark* especificado. Esse procedimento armazenado é fornecido para usuários que desejam gerenciar diretamente o processo de limpeza da tabela de alteração. Porém, é necessário ter cuidado, porque o procedimento afeta todos os consumidores de dados na tabela de alteração.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_cleanup_change_table   
  [ @capture_instance = ] 'capture_instance',   
  [ @low_water_mark = ] low_water_mark ,  
  [ @threshold = ]'delete threshold'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @capture_instance =] '*capture_instance*'  
 É o nome da instância de captura associada à tabela de alteração. *capture_instance* é **sysname**, sem padrão, e não pode ser nulo.  
  
 *capture_instance* deve nomear uma instância de captura que existe no banco de dados atual.  
  
 [ @low_water_mark =] *low_water_mark*  
 É um LSN (número de sequência de log) que deve ser usado como a nova marca d' água baixa para a *instância de captura*. *low_water_mark* é **binary (10)**, sem padrão.  
  
 Se o valor for não nulo, ele deverá aparecer como o valor start_lsn de uma entrada atual na tabela [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) . Se outras entradas no cdc.lsn_time_mapping compartilharem a mesma hora de confirmação que a entrada identificada pela nova marca d’água baixa, o menor LSN associado àquele grupo de entradas será escolhido como a marca d’água baixa.  
  
 Se o valor for definido explicitamente como NULL, a *marca d' água baixa* atual da *instância de captura* será usada para definir o limite superior para a operação de limpeza.  
  
 [ @threshold =] '*excluir limite*'  
 É o número máximo de entradas de exclusão que podem ser excluídas usando uma única instrução na limpeza. *delete_threshold* é **bigint**, com um padrão de 5000.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 sys.sp_cdc_cleanup_change_table executa as operações seguintes:  
  
1.  Se o @low_water_mark parâmetro não for nulo, ele definirá o valor de start_lsn para a *instância de captura* para a nova *marca d' água baixa*.  
  
    > [!NOTE]  
    >  A nova marca d’água baixa pode não ser a marca d’água baixa especificada na chamada do procedimento armazenado. Se outras entradas na tabela cdc.lsn_time_mapping compartilharem a mesma hora de confirmação, o menor start_1sn representado no grupo de entradas será selecionado como a marca d’água baixa ajustada. Se o @low_water_mark parâmetro for nulo ou a marca d' água baixa atual for maior do que o novo LowWatermark, o valor start_lsn para a instância de captura permanecerá inalterado.  
  
2.  As entradas da tabela de alteração com valores __$start_lsn menores do que a marca d’água baixa são excluídas. O limite de exclusão é usado para limitar o número de linhas excluídas em uma única transação. Uma falha ao excluir as entradas é relatada, mas não afeta nenhuma alteração na marca d’água baixa da instância de captura que pode ter sido feita com base na chamada.  

 Use sys.sp_cdc_cleanup_change_table nas seguintes circunstâncias:  
  
-   O trabalho do Agente de limpeza relata falhas de exclusão.  
  
     Um administrador pode executar esse procedimento armazenado explicitamente para tentar novamente a operação com falha. Para repetir a limpeza para uma determinada instância de captura, execute sys. sp_cdc_cleanup_change_table e especifique NULL para o @low_water_mark parâmetro.  
  
-   A política baseada em retenção simples usada pelo trabalho do Agente de limpeza não é adequada.  
  
     Como esse procedimento armazenado faz a limpeza de uma única instância de captura, ele pode ser usado para criar uma estratégia de limpeza personalizada que ajusta as regras de limpeza para a instância de captura individual.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa db_owner.  
  
## <a name="see-also"></a>Consulte Também  
 [CDC. fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [sys. fn_cdc_get_min_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [sys.fn_cdc_increment_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md)  
  
  
