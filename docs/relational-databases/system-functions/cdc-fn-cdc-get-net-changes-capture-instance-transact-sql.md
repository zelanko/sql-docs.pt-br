---
title: cdc.fn_cdc_get_net_changes_&lt;capture_instance&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_net_changes_<capture_instance>
- change data capture [SQL Server], querying metadata
- cdc.fn_cdc_get_net_changes_<capture_instance>
ms.assetid: 43ab0d1b-ead4-471c-85f3-f6c4b9372aab
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 27ad3ba5560be3fa547975d0d86099b3f4ab1450
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="cdcfncdcgetnetchangesltcaptureinstancegt-transact-sql"></a>cdc.fn_cdc_get_net_changes_&lt;capture_instance&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha de alteração líquida para cada linha de origem alterada dentro do intervalo de números de sequência de Log (LSN) especificado.  
  
 **Espera, o que é o LSN?** Cada registro de [log de transações do SQL Server](../logs/the-transaction-log-sql-server.md) é identificada exclusivamente por um número de sequência de log (LSN). Os LSNs são ordenados de tal modo que se LSN2 for maior do que LSN1, a alteração descrita pelo registro de log mencionado por LSN2 ocorreu **depois** da alteração descrita pelo registro de log LSN.  
  
 O LSN de um registro de log em que ocorreu um evento significativo pode ser útil para construir sequências de restauração corretas. Como os LSNs são ordenados, você pode compará-los para igualdade e desigualdade (isto é, \<, >, =, \<=, > =). Essas comparações são úteis ao construir sequências de restauração.  
  
 Quando uma linha de origem tiver várias alterações durante o intervalo de LSN, uma única linha que reflete o conteúdo final da linha é retornada pela função de enumeração descrita abaixo. Por exemplo, se uma transação insere uma linha na tabela de origem e uma transação subsequente dentro do intervalo LSN atualiza uma ou mais colunas na linha, a função retornará apenas **um** linha, que inclui os valores de coluna atualizada.  
  
 Essa função de enumeração é criada quando uma tabela de origem é habilitada para Change Data Capture e o rastreamento líquido é especificado. Para habilitar o rastreamento líquido, a tabela de origem deve ter uma chave primária ou índice exclusivo. O nome da função é derivado e usa o CDC. fn_cdc_get_net_changes_ formato*capture_instance*, onde *capture_instance* é o valor especificado para a instância de captura quando a tabela de origem habilitado para change data capture. Para obter mais informações, consulte [sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
cdc.fn_cdc_get_net_changes_capture_instance ( from_lsn , to_lsn , '<row_filter_option>' )  
  
<row_filter_option> ::=  
{ all  
 | all with mask  
 | all with merge  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *from_lsn*  
 O LSN que representa o ponto de extremidade inferior do intervalo de LSN para incluir no conjunto de resultados. *from_lsn* é **binário (10)**.  
  
 Apenas as linhas do [cdc.&#91; capture_instance&#93;CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) alterar tabela com um valor em _ $start_lsn maior que ou igual a *from_lsn* são incluídos no conjunto de resultados.  
  
 *to_lsn*  
 O LSN que representa o ponto de extremidade superior do intervalo de LSN para incluir no conjunto de resultados. *to_lsn* é **binário (10)**.  
  
 Apenas as linhas do [cdc.&#91; capture_instance&#93;CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) alterar tabela com um valor em _ $start_lsn menor ou igual a *from_lsn* ou igual a *to_lsn* são incluídos no conjunto de resultados.  
  
 *< row_filter_option >* :: = {todos | tudo com máscara | tudo com mesclagem}  
 Opção que rege o conteúdo das colunas de metadados, assim como as linhas retornadas no conjunto de resultados. Pode ser uma das seguintes opções:  
  
 all  
 Retorna o LSN da alteração final para a linha e a operação necessária para aplicar a linha nas colunas de metadados _ $start_lsn e \_ \_$operation. A coluna \_ \_$update_mask é sempre NULL.  
  
 all with mask  
 Retorna o LSN da alteração final para a linha e a operação necessária para aplicar a linha nas colunas de metadados _ $start_lsn e \_ \_$operation. Além disso, quando uma operação de atualização retorna (\_\_$operation = 4) as colunas capturadas modificadas na atualização são marcadas no valor retornado em \_ \_$update_mask.  
  
 all with merge  
 Retorna o LSN da alteração final para a linha nas colunas de metadados __$start_lsn. A coluna \_ \_$operation deve ser um dos dois valores: 1 para exclusão e 5 para indicar que a operação necessária para aplicar a alteração é uma inserção ou uma atualização. A coluna \_ \_$update_mask é sempre NULL.  
  
 Como a lógica para determinar a operação precisa de uma determinada alteração aumenta a complexidade de consulta, essa opção se destina a melhorar o desempenho de consulta quando for suficiente indicar se a operação necessária para aplicar os dados de alteração é uma inserção ou uma atualização, mas não for necessário distingui-las explicitamente. Essa opção é muito atraente em ambientes de destino em que uma operação de mesclagem está diretamente disponível, como um ambiente [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|__$start_lsn|**binary(10)**|LSN associado à transação de confirmação da alteração.<br /><br /> Todas as alterações confirmadas na mesma transação compartilham o mesmo LSN de confirmação. Por exemplo, se uma operação de atualização na tabela de origem modificar duas colunas em duas linhas, a tabela de alteração conterá quatro linhas, cada um com o mesmo start_lsnvalue de $ _.|  
|__$operation|**Int**|Identifica a operação DML (linguagem de manipulação de dados) necessária para aplicar a linha de dados de alteração à fonte de dados de destino.<br /><br /> Se o valor do parâmetro row_filter_option for tudo ou tudo com máscara, o valor desta coluna poderá ser um dos seguintes valores:<br /><br /> 1 = excluir<br /><br /> 2 = inserir<br /><br /> 4 = atualizar<br /><br /> Se o valor do parâmetro row_filter_option for tudo ou tudo com mesclagem, o valor desta coluna poderá ser um dos seguintes valores:<br /><br /> 1 = excluir|  
|__$update_mask|**varbinary(128)**|Uma máscara de bits com um bit correspondente a cada coluna capturada identificada para a instância de captura. Esse valor tem todos os bits definidos configurados como 1 quando __$operation = 1 ou 2. Quando \_ \_$operation = 3 ou 4, apenas os bits correspondentes às colunas que foram alteradas são configurados como 1.|  
|*\<colunas da tabela de origem capturada>*|varia|As colunas restantes retornadas pela função são as colunas da tabela de origem que foram identificadas como colunas capturadas quando a instância de captura foi criada. Se nenhuma coluna tiver sido especificada na lista de colunas capturadas, todas as colunas da tabela de origem serão retornadas.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin ou na função de banco de dados fixa db_owner. Para todos os outros usuários, requer a permissão SELECT em todas as colunas capturadas na tabela de origem e, se uma função associada para a instância de captura tiver sido definida, faça associação nessa função de banco de dados. Quando o chamador não tiver permissão para exibir os dados de origem, a função retornará o erro 208 (Nome de objeto inválido).  
  
## <a name="remarks"></a>Remarks  
 Se o intervalo de LSN especificado não cair dentro da linha do tempo do rastreamento de alterações da instância de captura, a função retornará o erro 208 (Nome de objeto inválido).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa a função `cdc.fn_cdc_get_net_changes_HR_Department` para relatar as alterações líquidas efetuadas na tabela de origem `HumanResources.Department` durante um intervalo de tempo específico.  
  
 Primeiro, a função `GETDATE` é usada para marcar o início do intervalo de tempo. Depois que diversas instruções DML são aplicadas à tabela de origem, a função `GETDATE` é chamada novamente para identificar o final do intervalo de tempo. A função [fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) é usado para mapear o intervalo de tempo para um intervalo de consulta de captura do alterar dados vinculado por valores LSN. Finalmente, a função `cdc.fn_cdc_get_net_changes_HR_Department` é consultada para obter as alterações líquidas efetuadas na tabela de origem nesse intervalo de tempo. Note que a linha que é inserida e, depois, excluída não aparece no conjunto de resultados retornado pela função. Isso porque uma linha inicialmente adicionada e, depois, excluída dentro de uma janela de consulta não produz nenhuma alteração líquida na tabela de origem nesse intervalo. Antes de executar este exemplo, primeiro você deve executar o exemplo B no [sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @begin_time datetime, @end_time datetime, @from_lsn binary(10), @to_lsn binary(10);  
-- Obtain the beginning of the time interval.  
SET @begin_time = GETDATE() -1;  
-- DML statements to produce changes in the HumanResources.Department table.  
INSERT INTO HumanResources.Department (Name, GroupName)  
VALUES (N'MyDept', N'MyNewGroup');  
  
UPDATE HumanResources.Department  
SET GroupName = N'Resource Control'  
WHERE GroupName = N'Inventory Management';  
  
DELETE FROM HumanResources.Department  
WHERE Name = N'MyDept';  
  
-- Obtain the end of the time interval.  
SET @end_time = GETDATE();  
-- Map the time interval to a change data capture query range.  
SET @from_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than or equal', @begin_time);  
SET @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);  
  
-- Return the net changes occurring within the query window.  
SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@from_lsn, @to_lsn, 'all');  
```  
  
## <a name="see-also"></a>Consulte também  
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_map_time_to_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
