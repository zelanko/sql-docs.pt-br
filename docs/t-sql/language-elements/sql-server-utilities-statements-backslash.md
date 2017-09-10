---
title: (Barra invertida) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- '\_TSQL'
- '\'
dev_langs:
- TSQL
helpviewer_keywords:
- backwhack
- backslash
- excape character
- hack character
- '\ (backslash)'
- backslant
- bash
- reverse slant
- slosh
- reversed virgule
- line continuation character
- reverse solidus
ms.assetid: c97fbb20-3d12-4d0b-9b52-62a229bc83c0
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 011025d20b6341b9fa43b25f6c14c91a135a6ffa
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-utilities-statements---backslash"></a>Instruções de utilitários do SQL Server - barra invertida
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]fornece comandos que não estão [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções, mas são reconhecidos pelo **sqlcmd** e **osql** utilitários e [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Editor de códigos. Estes comandos podem ser usados para facilitar a legibilidade e a execução de lotes e scripts.  
  
\ divide uma cadeia de caracteres longa constante em duas ou mais linhas para facilitar a leitura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<first section of string> \  
<continued section of string>  
```  
  
## <a name="arguments"></a>Argumentos  
 \<primeira seção da cadeia de caracteres >  
 É o início de uma cadeia de caracteres.  
  
 \<continuação de seção de cadeia de caracteres >  
 É a continuação de uma cadeia de caracteres.  
  
## <a name="remarks"></a>Comentários  
 Esse comando retorna a primeira seção e as seções contínuas da cadeia de caracteres como uma cadeia de caracteres, sem a barra invertida.  
  
 A barra invertida não é uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)]. É um comando reconhecido pelo **sqlcmd** e **osql** utilitários e [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Editor de códigos.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa uma barra invertida e um retorno de carro para dividir a cadeia de caracteres em duas linhas.  
  
```  
SELECT 'abc\  
def' AS ColumnResult;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ColumnResult  
 ------------  
 abcdef
 ```    
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [&#40; divisão &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/divide-transact-sql.md)   
 [&#40; dividir EQUALS &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [Composta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  

