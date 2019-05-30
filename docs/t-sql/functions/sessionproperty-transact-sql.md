---
title: SESSIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SESSIONPROPERTY
- SESSIONPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, SESSIONPROPERTY function
- SESSIONPROPERTY function
- sessions [SQL Server], SET options settings
ms.assetid: 1f3730b4-1495-4d3a-af43-e57952812df9
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: ba08b2273102d43eed26d7b383a285d6568a63d2
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65942889"
---
# <a name="sessionproperty-transact-sql"></a>SESSIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna as configurações de opções SET de uma sessão.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SESSIONPROPERTY (option)  
```  
  
## <a name="arguments"></a>Argumentos  
 *opção*  
 É a configuração de opção atual durante esta sessão. *option* pode ter qualquer um dos valores a seguir.  
  
|Opção|Descrição|  
|------------|-----------------|  
|ANSI_NULLS|Especifica se o comportamento da ISO de igual a (=) e não igual a (<>) em relação a valores nulos se aplica.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ANSI_PADDING|Controla como a coluna armazena valores menores que o tamanho definido da coluna e o modo como a coluna armazena valores com espaços em branco à direita em caracteres e dados binários.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ANSI_WARNINGS|Especifica se o comportamento padrão de ISO de gerar mensagens de erro ou avisos para determinadas condições, inclusive divisão por zero e estouro aritmético, aplica-se.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ARITHABORT|Determina se uma consulta será finalizada quando um erro de estouro ou divisão por zero ocorrer durante a execução da consulta.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|CONCAT_NULL_YIELDS_NULL|Controla se os resultados de concatenação serão tratados como valores de cadeia de caracteres nulos ou vazios.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|NUMERIC_ROUNDABORT|Especifica se são geradas mensagens de erro e avisos quando o arredondamento em uma expressão causar uma perda de precisão.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|QUOTED_IDENTIFIER|Especifica se as regras ISO referentes a como usar aspas para delimitar identificadores e cadeias de caracteres literais devem ser seguidas.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|\<Qualquer outra cadeia de caracteres>|NULL = A entrada não é válida.|  
  
## <a name="return-types"></a>Tipos de retorno  
 **sql_variant**  
  
## <a name="remarks"></a>Remarks  
 As opções SET são figuradas combinando as opções de nível de servidor, nível de banco de dados e as opções especificadas pelo usuário.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a configuração para a opção `CONCAT_NULL_YIELDS_NULL`.  
  
```  
SELECT   SESSIONPROPERTY ('CONCAT_NULL_YIELDS_NULL')  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)   
 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)   
 [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  
