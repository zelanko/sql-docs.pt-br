---
title: sys.fn_cdc_has_column_changed (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_has_column_changed_TSQL
- sys.fn_cdc_has_column_changed
- fn_cdc_has_column_changed_TSQL
- fn_cdc_has_column_changed
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_cdc_has_column_changed
- fn_cdc_has_column_changed
ms.assetid: 2b9e6278-050d-4ffc-8d1a-09606180facc
author: rothja
ms.author: jroth
ms.openlocfilehash: 4e5ad2f17c31508b8d712474723af169becd794b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760240"
---
# <a name="sysfn_cdc_has_column_changed-transact-sql"></a>sys.fn_cdc_has_column_changed (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Identifica se a máscara de atualização especificada indica que a coluna especificada foi atualizada na linha de alteração associada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_cdc_has_column_changed ( 'capture_instance','column_name' , update_mask )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *capture_instance* **'**  
 É o nome da instância de captura. *capture_instance* é **sysname**.  
  
 **'** *column_name* **'**  
 É a coluna capturada da instância de captura especificada a ser relatada. *column_name* é **sysname**.  
  
 *update_mask*  
 É a máscara que identifica colunas atualizadas em qualquer linha de alteração associada. *update_mask* é **varbinary (128)**.  
  
## <a name="return-type"></a>Tipo de retorno  
 **bit**  
  
## <a name="remarks"></a>Comentários  
 Você pode usar esta função para extrair informações de uma máscara de atualização retornada em uma consulta para obter dados de alteração. A máscara de atualização é muito útil na pós-execução, quando é preciso saber se uma coluna particular na linha de alteração associada foi modificada. Para obter mais informações, veja [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md).  
  
 Quando essas informações forem retornadas como parte de uma consulta de dados de alteração, recomendamos que você use as funções [Sys. fn_cdc_get_column_ordinal](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md) e [Sys. fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) em vez dessa função. Use a função fn_cdc_get_column_ordinal antes de consultar os dados de alteração, de forma que a ordinal da coluna desejada seja computada somente uma vez. Use fn_cdc_is_bit_set dentro da consulta para extrair as informações da máscara de atualização de cada linha retornada.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin ou na função de banco de dados fixa db_owner. Para todos os outros usuários, requer a permissão SELECT em todas as colunas capturadas na tabela de origem e, se uma função associada para a instância de captura tiver sido definida, faça associação nessa função de banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [CDC. &#60;capture_instance&#62;_CT &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)   
 [cdc.captured_columns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-captured-columns-transact-sql.md)  
  
  
