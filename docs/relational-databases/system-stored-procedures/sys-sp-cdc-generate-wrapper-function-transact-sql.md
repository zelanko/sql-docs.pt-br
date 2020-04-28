---
title: sys. sp_cdc_generate_wrapper_function (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 074e114f81db6615a04240f10447a3f711a51cf7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68083749"
---
# <a name="syssp_cdc_generate_wrapper_function-transact-sql"></a>sys.sp_cdc_generate_wrapper_function (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gera scripts para criar funções de wrapper para as funções de consulta de captura de dados de alteração disponíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A API suportada nos wrappers gerados permite a especificação do intervalo de consulta como um intervalo datetime. Isso torna a função boa para uso em muitos aplicativos de warehouse, incluindo aquelas que são desenvolvidas por [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] projetistas de pacote que estão usando a tecnologia de captura de dados de alterações para determinar a carga incremental.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ @capture_instance= ] '*capture_instance*'  
 É a instância de captura para a qual os scripts serão gerados. *capture_instance* é **sysname** e tem um valor padrão de NULL. Se um valor for omitido ou explicitamente definido como NULL, serão gerados scripts de wrapper para todas as instâncias de captura.  
  
 [ @closed_high_end_point= ] *high_end_pt_flag*  
 É o bit de sinalizador que indica se as alterações que têm um horário de confirmação igual ao ponto de extremidade alto serão incluídas dentro do intervalo de extração pelo procedimento gerado. *high_end_pt_flag* é **bit** e tem um valor padrão de 1, que indica que o ponto de extremidade deve ser incluído. Um valor de 0 indica que todas as horas de confirmação serão estritamente anteriores ao ponto de extremidade alto.  
  
 [ @column_list= ] '*column_list*'  
 É uma lista de colunas capturadas a serem incluídas no conjunto de resultados, que é retornado pela função de wrapper. *column_list* é **nvarchar (max)** e tem um valor padrão de NULL. Quando NULL for especificado, todas as colunas capturadas serão incluídas.  
  
 [ @update_flag_list= ] '*update_flag_list*'  
 É a lista de colunas incluídas para as quais um sinalizador de atualização é incluído no conjunto de resultados retornado pela função wrapper. *update_flag_list* é **nvarchar (max)** e tem um valor padrão de NULL. Quando NULL for especificado, nenhum sinalizador de atualização será incluído.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de coluna|Descrição|  
|-----------------|-----------------|-----------------|  
|**function_name**|**nvarchar (145)**|Nome da função gerada.|  
|**create_script**|**nvarchar(max)**|É o script que cria a função de wrapper da instância de captura.|  
  
## <a name="remarks"></a>Comentários  
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
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de captura de dados de alterações &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [Captura de dados de alterações &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)  
  
  
