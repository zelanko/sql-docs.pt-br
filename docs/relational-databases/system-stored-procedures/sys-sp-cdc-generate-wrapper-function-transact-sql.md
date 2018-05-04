---
title: sys. sp_cdc_generate_wrapper_function (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cdc_generate_wrapper_function_TSQL
- sp_cdc_generate_wrapper_function
- sys.sp_cdc_generate_wrapper_function_TSQL
- sys.sp_cdc_generate_wrapper_function
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_generate_wrapper_function
- sp_cdc_generate_wrapper_function
ms.assetid: 85bc086d-8a4e-4949-a23b-bf53044b925c
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3b2d86105f6ebe44865a0a31d3eedfefe4838bfe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysspcdcgeneratewrapperfunction-transact-sql"></a>sys.sp_cdc_generate_wrapper_function (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gera scripts para criar funções de wrapper para as funções de consulta de captura de dados de alteração disponíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A API suportada nos wrappers gerados permite que o intervalo de consulta a ser especificado como um intervalo de data e hora. Isso torna a função adequada para uso em vários aplicativos de warehousing, incluindo aqueles que são desenvolvidas pela [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tecnologia para determinar carga incremental de captura de designers de pacotes que estão usando dados de alteração.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_generate_wrapper_function  
    [ [ @capture_instance sysname = ] 'capture_instance'  
    [ , [ @closed_high_end_point = ] closed_high_end_pt  
    [ , [ @column_list = ] 'column_list'  
```  
  
```  
  
[ , [ @update_flag_list = ] 'update_flag_list'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @capture_instance=] '*capture_instance*'  
 É a instância de captura para a qual os scripts serão gerados. *capture_instance* é **sysname** e tem um valor padrão de NULL. Se um valor for omitido ou explicitamente definido como NULL, serão gerados scripts de wrapper para todas as instâncias de captura.  
  
 [ @closed_high_end_point=] *high_end_pt_flag*  
 É o bit de sinalizador que indica se as alterações que têm um horário de confirmação igual ao ponto de extremidade alto serão incluídas dentro do intervalo de extração pelo procedimento gerado. *high_end_pt_flag* é **bit** e tem um valor padrão de 1, o que indica que o ponto de extremidade deve ser incluído. Um valor de 0 indica que todas as horas de confirmação serão estritamente anteriores ao ponto de extremidade alto.  
  
 [ @column_list=] '*column_list*'  
 É uma lista de colunas capturadas a serem incluídas no conjunto de resultados, que é retornado pela função de wrapper. *column_list* é **nvarchar (max)** e tem um valor padrão de NULL. Quando NULL for especificado, todas as colunas capturadas serão incluídas.  
  
 [ @update_flag_list=] '*update_flag_list*'  
 É a lista de colunas incluídas para as quais um sinalizador de atualização é incluído no conjunto de resultados retornado pela função wrapper. *update_flag_list* é **nvarchar (max)** e tem um valor padrão de NULL. Quando NULL for especificado, nenhum sinalizador de atualização será incluído.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de coluna|Description|  
|-----------------|-----------------|-----------------|  
|**function_name**|**nvarchar(145)**|Nome da função gerada.|  
|**create_script**|**nvarchar(max)**|É o script que cria a função de wrapper da instância de captura.|  
  
## <a name="remarks"></a>Remarks  
 O script que cria a função para incluir a consulta de todas as alterações para uma instância de captura sempre é gerado. Se a instância de captura oferecer suporte a consultas das alterações puras, também será gerado o script para gerar um wrapper para essa consulta.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra como é possível usar `sys.sp_cdc_generate_wrapper_function` para criar wrappers para todas as funções de captura de dados de alteração.  
  
```  
DECLARE @wrapper_functions TABLE (  
    function_name sysname,  
    create_script nvarchar(max));  
  
INSERT INTO @wrapper_functions  
EXEC sys.sp_cdc_generate_wrapper_function;  
  
DECLARE @create_script nvarchar(max);  
DECLARE #hfunctions CURSOR LOCAL fast_forward  
FOR   
    SELECT create_script FROM @wrapper_functions;  
  
OPEN #hfunctions;  
FETCH #hfunctions INTO @create_script;  
WHILE (@@fetch_status <> -1)  
BEGIN  
    EXEC sp_executesql @create_script  
    FETCH #hfunctions INTO @create_script  
END;  
  
CLOSE #hfunctions;  
DEALLOCATE #hfunctions;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de captura de dados de alterações &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [O Change Data Capture &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)  
  
  
