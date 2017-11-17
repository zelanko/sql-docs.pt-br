---
title: HASHBYTES (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HASHBYTES_TSQL
- HASHBYTES
dev_langs:
- TSQL
helpviewer_keywords:
- hash input
- HASHBYTES
ms.assetid: 0ea6a4d1-313e-4f70-b939-dd2cd570f6d6
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4826936736685a46e8df8604339a7d4a878981ee
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="hashbytes-transact-sql"></a>HASHBYTES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna o hash de MD2, MD4, MD5, SHA, SHA1 ou SHA2 de sua entrada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HASHBYTES ( '<algorithm>', { @input | 'input' } )  
  
<algorithm>::= MD2 | MD4 | MD5 | SHA | SHA1 | SHA2_256 | SHA2_512   
```  
  
## <a name="arguments"></a>Argumentos  
 **'**\<algoritmo >**'**  
 Identifica o algoritmo de hash a ser usado para aplicar o hash à entrada. Este é um argumento exigido sem padrão. As aspas simples são obrigatórias. Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], todos os algoritmos diferentes SHA2_256 e SHA2_512 são preteridos. Algoritmos mais antigos (não recomendados) continuarão a funcionar, mas eles irá gerar um evento de substituição.  
  
 **@input**  
 Especifica uma variável que contém os dados a aceitar o hash. **@input**é **varchar**, **nvarchar**, ou **varbinary**.  
  
 **'** *entrada* **'**  
 Especifica uma expressão que é avaliada para uma cadeia de caracteres binária ou um caractere que receberá hash.  
  
 A saída segue o padrão do algoritmo: 128 bits (16 bytes) para MD2, MD4 e MD5; 160 bits (20 bytes) para SHA e SHA1; 256 bits (32 bytes) para SHA2_256 e 512 bits (64 bytes) para SHA2_512.  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e versões anteriores, permitidos valores de entrada são limitados a 8000 bytes.  
  
## <a name="return-value"></a>Valor de retorno  
 **varbinary** (máximo de 8000 bytes)  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-return-the-hash-of-a-variable"></a>R: retornar o hash de uma variável  
 O exemplo a seguir retorna o `SHA1` hash do **nvarchar** dados armazenados na variável `@HashThis`.  
  
```  
DECLARE @HashThis nvarchar(4000);  
SET @HashThis = CONVERT(nvarchar(4000),'dslfdkjLK85kldhnv$n000#knf');  
SELECT HASHBYTES('SHA1', @HashThis);  
  
```  
  
### <a name="b-return-the-hash-of-a-table-column"></a>B: retornar o hash de uma coluna de tabela  
 O exemplo a seguir retorna o hash SHA1 dos valores na coluna `c1` da tabela `Test1`.  
  
```  
CREATE TABLE dbo.Test1 (c1 nvarchar(50));  
INSERT dbo.Test1 VALUES ('This is a test.');  
INSERT dbo.Test1 VALUES ('This is test 2.');  
SELECT HASHBYTES('SHA1', c1) FROM dbo.Test1;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
-------------------------------------------  
0x0E7AAB0B4FF0FD2DFB4F0233E2EE7A26CD08F173  
0xF643A82F948DEFB922B12E50B950CEE130A934D6  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Escolher um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  

