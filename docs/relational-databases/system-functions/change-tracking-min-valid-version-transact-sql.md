---
title: CHANGE_TRACKING_MIN_VALID_VERSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_CLEANUP_VERSION
- CHANGE_TRACKING_CLEANUP_VERSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHANGE_TRACKING_MIN_VALID_VERSION
- change tracking [SQL Server], CHANGE_TRACKING_MIN_VALID_VERSION
ms.assetid: 5a43d23f-adcf-4c0b-95ad-07cee03c1f9d
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d2858c61ea7316b1bafa06a1181b31e97b0724b3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47766630"
---
# <a name="changetrackingminvalidversion-transact-sql"></a>CHANGE_TRACKING_MIN_VALID_VERSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna a versão mínima no cliente que é válido para usar na obtenção de informações controle de alterações da tabela especificada, quando você estiver usando o [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md) função.  
    
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CHANGE_TRACKING_MIN_VALID_VERSION ( table_object_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 *table_object_id*  
 É a ID de objeto da tabela. *table_object_id* é um **int**.  
  
## <a name="return-type"></a>Tipo de retorno  
 **bigint**  
  
## <a name="remarks"></a>Comentários  
 Use esta função para validar o valor do *last_sync_version* parâmetro para CHANGETABLE. Se *last_sync_version* é menor que o valor relatado por essa função, os resultados retornados de uma chamada posterior a CHANGETABLE podem não ser válidos.  
  
 CHANGE_TRACKING_MIN_VALID_VERSION usa as seguintes informações para determinar o valor de retorno:  
  
-   Quando a tabela foi habilitada para o controle de alterações.  
  
-   Quando uma tarefa de limpeza em segundo plano foi executada para remover informações de controle de alterações mais antigas que o período de retenção especificado para o banco de dados.  
  
-   Se a tabela foi truncada. Isso remove todas as informações de controle de alterações associadas à tabela.  
  
 A função retornará NULL se uma das condições a seguir for verdadeira:  
  
-   O controle de alterações não está habilitado para o banco de dados.  
  
-   O ID de objeto da tabela especificado não é válido para o banco de dados atual.  
  
-   Permissão inadequada para a tabela especificada pelo ID de objeto.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir determina se uma versão especificada é uma versão válida. O exemplo obtém a versão válida mínima da tabela `dbo.Employees` e a compara com o valor da variável `@last_sync_version`. Se o valor de `@last_sync_version` for menor que o de `@min_valid_version`, a lista de linhas alteradas não será válida.  
  
> [!NOTE]  
>  Em geral, você obtém o valor de uma tabela ou de outro local onde está armazenado o número da versão mais recente usada para sincronizar os dados.  
  
```  
-- The tracked change is tagged with the specified context   
DECLARE @min_valid_version bigint, @last_sync_version bigint;  
  
SET @min_valid_version =   
CHANGE_TRACKING_MIN_VALID_VERSION(OBJECT_ID('dbo.Employees'));  
  
SET @last_sync_version = 11  
IF (@last_sync_version < @min_valid_version)  
-- Error � do not obtain changes  
ELSE  
-- Obtain changes using CHANGETABLE(CHANGES ...)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções do controle de alterações &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)  
  
  
