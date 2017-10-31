---
title: QUOTENAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- QUOTENAME_TSQL
- QUOTENAME
dev_langs:
- TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- input strings [SQL Server]
- Unicode [SQL Server], delimited identifiers
- QUOTENAME function
- valid identifiers [SQL Server]
ms.assetid: 34d47f1e-2ac7-4890-8c9c-5f60f115e076
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f4e40797fc49e8a70b01162fc6959ad60475e8b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="quotename-transact-sql"></a>QUOTENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma cadeia de caracteres Unicode com os delimitadores adicionados para tornar a cadeia de caracteres de entrada um identificador delimitado válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
QUOTENAME ( 'character_string' [ , 'quote_character' ] )   
```  
  
## <a name="arguments"></a>Argumentos  
 '*character_string*'  
 É uma cadeia de caracteres de dados de caracteres Unicode. *character_string* é **sysname** e é limitado a 128 caracteres. Entradas maiores que 128 caracteres retornam NULL.  
  
 '*quote_character*'  
 É uma cadeia de um caractere a ser usada como o delimitador. Pode ser uma aspa simples ( **'** ), um colchete esquerdo ou direito ( **[]** ), ou aspas duplas ( **"** ). Se *quote_character* não for especificado, serão usados colchetes.  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar (258)**  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir obtém a cadeia de caracteres `abc[]def` e usa os caracteres `[` e `]` para criar um identificador delimitado válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT QUOTENAME('abc[]def');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc[]]def]  
  
(1 row(s) affected)  
```  
  
 Observe que o colchete direito na cadeia de caracteres `abc[]def` é duplicado para indicar um caractere de escape.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 O exemplo a seguir obtém a cadeia de caracteres `abc def` e usa os caracteres `[` e `]` para criar um identificador delimitado válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT QUOTENAME('abc def');   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc def]  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cadeia de caracteres &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


