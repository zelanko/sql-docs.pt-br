---
description: HASHBYTES (Transact-SQL)
title: HASHBYTES (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b72eb876317282b421c64f0101c275970548f8f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97421792"
---
# <a name="hashbytes-transact-sql"></a>HASHBYTES (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna o hash de MD2, MD4, MD5, SHA, SHA1 ou SHA2 de sua entrada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
HASHBYTES ( '<algorithm>', { @input | 'input' } )  
  
<algorithm>::= MD2 | MD4 | MD5 | SHA | SHA1 | SHA2_256 | SHA2_512   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

`<algorithm>`  
Identifica o algoritmo de hash a ser usado para aplicar o hash à entrada. Este é um argumento exigido sem padrão. As aspas simples são obrigatórias. Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], todos os algoritmos, exceto SHA2_256 e SHA2_512, foram preteridos.  
  
`@input`  
Especifica uma variável que contém os dados a aceitar o hash. `@input` é **varchar**, **nvarchar** ou **varbinary**.  
  
'*input*'  
Especifica uma expressão que é avaliada para uma cadeia de caracteres binária ou um caractere que receberá hash.  
  
 A saída segue o padrão do algoritmo: 128 bits (16 bytes) para MD2, MD4 e MD5; 160 bits (20 bytes) para SHA e SHA1; 256 bits (32 bytes) para SHA2_256 e 512 bits (64 bytes) para SHA2_512.  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior
  
 Para o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e anterior, os valores de entrada permitidos estão limitados a 8.000 bytes.  
  
## <a name="return-value"></a>Valor retornado  
 **varbinary** (máximo de 8.000 bytes)  

## <a name="remarks"></a>Comentários  
Considere o uso de `CHECKSUM` ou `BINARY_CHECKSUM` como alternativas para calcular um valor de hash.

Os algoritmos MD2, MD4, MD5, SHA e SHA1 começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] são preteridos. Use SHA2_256 ou SHA2_512. Os algoritmos mais antigos continuarão funcionando, mas acionarão um evento de reprovação.

## <a name="examples"></a>Exemplos  
### <a name="return-the-hash-of-a-variable"></a>Retornar o hash de uma variável  
 O exemplo a seguir retorna o hash `SHA2_256` dos dados **nvarchar** armazenados na variável `@HashThis`.  
  
```sql  
DECLARE @HashThis NVARCHAR(32);  
SET @HashThis = CONVERT(NVARCHAR(32),'dslfdkjLK85kldhnv$n000#knf');  
SELECT HASHBYTES('SHA2_256', @HashThis);  
```  
  
### <a name="return-the-hash-of-a-table-column"></a>Retornar o hash de uma coluna de tabela  
 O exemplo a seguir retorna o hash SHA2_256 dos valores na coluna `c1` da tabela `Test1`.  
  
```sql  
CREATE TABLE dbo.Test1 (c1 NVARCHAR(32));  
INSERT dbo.Test1 VALUES ('This is a test.');  
INSERT dbo.Test1 VALUES ('This is test 2.');  
SELECT HASHBYTES('SHA2_256', c1) FROM dbo.Test1;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------------------------------  
0x741238C01D9DB821CF171BF61D72260B998F7C7881D90091099945E0B9E0C2E3 
0x91DDCC41B761ACA928C62F7B0DA61DC763255E8247E0BD8DCE6B22205197154D  
(2 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte Também  
[Escolha um algoritmo de criptografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)
[CHECKSUM_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-agg-transact-sql.md)
[CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)
[BINARY_CHECKSUM  &#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md)
