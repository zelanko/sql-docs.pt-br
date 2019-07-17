---
title: DM external_script_execution_stats | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_external_script_execution_stats
- sys.dm_external_script_execution_stats_TSQL
- dm_external_script_execution_stats
- dm_external_script_execution_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_external_script_execution_stats dynamic management view
ms.assetid: 2e99f026-ceb2-42a2-a549-c71d31ed0cf4
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 06b8e29e9aaf02c8e82f541a9113d5943b829b3b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262163"
---
# <a name="sysdmexternalscriptexecutionstats"></a>sys.dm_external_script_execution_stats
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Retorna uma linha para cada tipo de solicitação de script externo. As solicitações de script externo são agrupadas pela linguagem de script externo com suporte. Uma linha é gerada para cada função de script externo registrada. Funções de script externo arbitrárias não são registradas, exceto se forem enviadas por um processo pai, como `rxExec`.
  
> [!NOTE]  
> Este modo de exibição de gerenciamento dinâmico (DMV) está disponível somente se você tiver instalado e habilitado o recurso que dá suporte à execução de script externo. Para obter mais informações, consulte [R Services no SQL Server 2016](../../advanced-analytics/r/sql-server-r-services.md) e [serviços Machine Learning (R, Python) no SQL Server 2017](../../advanced-analytics/what-is-sql-server-machine-learning.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|language|**nvarchar**|Nome da linguagem de script externo registrada. Cada script externo deve especificar a linguagem na solicitação de script para iniciar o inicializador associado. |  
|counter_name|**nvarchar**|Nome de uma função de script externo registrada. Não permite valor nulo.|  
|counter_value|**inteiro**|Número total de instâncias nas quais a função de script externo registrada foi chamada no servidor. Esse valor é cumulativo, começando com a hora em que o recurso foi instalado na instância, e não pode ser redefinido.|  

  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STATE no servidor.  
  
> [!NOTE]  
>  Os usuários que executam scripts externos devem ter a permissão adicional EXECUTE ANY EXTERNAL SCRIPT; no entanto, essa DMV pode ser usada por administradores sem essa permissão. 
  
## <a name="remarks"></a>Comentários  
  Essa DMV é fornecida para telemetria interna, a fim de monitorar o uso geral do novo recurso de execução de script externo no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. O serviço de telemetria é iniciado quando o LaunchPad é iniciado e incrementa um contador baseado em disco sempre que uma função de script externo registrada é chamada.

Em geral, os contadores de desempenho são válidos somente enquanto o processo que os gerou está ativo. Portanto, uma consulta em uma DMV não pode mostrar dados detalhados de serviços que foram interrompidos. Por exemplo, se um iniciador executa um script externo e ainda assim conclui-los muito rapidamente, uma DMV convencional poderá não mostrar nenhum dado.

Portanto, os contadores acompanhados por esta DMV são mantidos em execução, e o estado de sys.dm_external_script_requests é preservado usando gravações em disco, mesmo se a instância é desligada.

   
  
### <a name="counter-values"></a>Valores de contador
No SQL Server 2016, a única linguagem externa suportada é R e as solicitações de script externo são manipuladas pelo [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]. No SQL Server 2017, R e Python é externos de idiomas com suporte e as solicitações de script externo são manipuladas pelo [!INCLUDE[rsql_productname_md](../../includes/rsql-productnamenew-md.md)].

Para R, essa DMV registra o número de chamadas de R que são feitas em uma instância. Por exemplo, se `rxLinMod` for chamado e executado em paralelo, o contador será incrementado em 1.
 
Na linguagem R, os valores de contador exibidos no campo *counter_name* representam os nomes das funções ScaleR registradas. Os valores do campo *counter_value* representam o número cumulativo de instâncias da função ScaleR específica. 

Para o Python, essa DMV registra o número de chamadas do Python que são feitas em uma instância.

A contagem é iniciada quando o recurso é instalado e habilitado na instância e é cumulativa até que o arquivo que mantém o estado seja excluído ou substituído por um administrador. Portanto, em geral, não é possível redefinir os valores de *counter_value*. Se você desejar monitorar o uso por sessão, horários do calendário ou outros intervalos, recomendamos que você capture as contagens em uma tabela.

### <a name="registration-of-external-script-functions-in-r"></a>Registro de funções de script externo no R

R dá suporte a scripts arbitrários, e a comunidade de R fornece muitos milhares de pacotes, cada um com suas próprias funções e métodos. No entanto, essa DMV monitora apenas as funções ScaleR instaladas no SQL Server R Services.

O registro dessas funções é executado quando o recurso é instalado, e as funções registradas não podem ser adicionadas nem excluídas.

## <a name="examples"></a>Exemplos  
  
### <a name="viewing-the-number-of-r-scripts-run-on-the-server"></a>Exibindo o número de scripts do R executados no servidor  
 O exemplo a seguir exibe o número cumulativo de execuções de script externo da linguagem R.  
  
```  
SELECT counter_name, counter_value   
FROM sys.dm_external_script_execution_stats   
WHERE language = 'R';
```  

### <a name="viewing-the-number-of-python-scripts-run-on-the-server"></a>Exibindo o número de Python scripts são executados no servidor  
 O exemplo a seguir exibe o número cumulativo de execuções de script externo para a linguagem Python.  
  
```  
SELECT counter_name, counter_value   
FROM sys.dm_external_script_execution_stats   
WHERE language = 'Python';
```  

  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md) 
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  

