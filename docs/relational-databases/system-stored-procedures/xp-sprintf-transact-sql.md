---
title: xp_sprintf (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xp_sprintf_TSQL
- xp_sprintf
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sprintf
ms.assetid: 1eedd65c-03cc-4eab-b76e-04684fdfec52
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dcd807fca603c8ecb47a8333f2dcc27b52302bad
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="xpsprintf-transact-sql"></a>xp_sprintf (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Formata e armazena uma série de caracteres e valores no parâmetro de saída de cadeia de caracteres. Cada argumento do formato é substituído pelo argumento correspondente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_sprintf { string OUTPUT , format }  
     [ , argument [ ,...n ] ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *cadeia de caracteres*  
 É um **varchar** variável que recebe a saída.  
  
 OUTPUT  
 Quando for especificado, põe o valor da variável no parâmetro de saída.  
  
 *formato*  
 É uma cadeia de caracteres de formato com espaços reservados para *argumento* valores, semelhantes ao suporte de linguagem C **sprintf** função. Atualmente, é oferecido suporte apenas para o argumento de formato %s.  
  
 *argumento*  
 É uma cadeia de caracteres que representa o valor do argumento de formato correspondente.  
  
 *n*  
 É um espaço reservado que indica que no máximo 50 argumentos podem ser especificados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **xp_sprintf** retorna a seguinte mensagem:  
  
 `The command(s) completed successfully.`  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Estendidos gerais procedimentos armazenados &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_sscanf &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-sscanf-transact-sql.md)  
  
  
