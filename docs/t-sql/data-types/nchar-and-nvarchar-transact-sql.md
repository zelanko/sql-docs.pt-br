---
title: nchar e nvarchar (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- nvarchar data type
- nchar data type
ms.assetid: 81ee5637-ee31-4c4d-96d0-56c26a742354
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4c3f2e9ad1d63992be8f4e4a4c65d821fae73389
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar e nvarchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de dados que são de comprimento fixo, caracteres **nchar**, ou de comprimento variável, **nvarchar**, conjunto de caracteres de dados Unicode e usar o UNICODE UCS-2.
  
## <a name="arguments"></a>Argumentos  
**nchar** [(n)]  
Dados de cadeia de caracteres Unicode de comprimento fixo. *n*Define o comprimento da cadeia de caracteres e deve ser um valor de 1 a 4.000. O tamanho de armazenamento é duas vezes  *n*  bytes. Quando a página de código do agrupamento usa caracteres de byte duplo, o tamanho de armazenamento ainda será  *n*  bytes. Dependendo da cadeia de caracteres, o tamanho do armazenamento de  *n*  bytes pode ser menor que o valor especificado para  *n* . Os sinônimos ISO para **nchar** são **national char** e **caracteres nacionais**...
  
**nvarchar** [(n | **máximo** )]  
Dados de cadeia de caracteres Unicode de comprimento variável. *n*Define o comprimento da cadeia de caracteres e pode ser um valor de 1 a 4.000. **Max** indica que o tamanho máximo de armazenamento é 2 ^ 31-1 caracteres (2 GB). O tamanho de armazenamento, em bytes, é duas vezes o comprimento real dos dados digitados + 2 bytes. Os sinônimos ISO para **nvarchar** são **national char variados** e **variáveis de caractere nacional**.
  
## <a name="remarks"></a>Comentários  
Quando  *n*  não for especificado em uma definição de dados ou uma instrução de declaração de variável, o comprimento padrão é 1. Quando  *n*  não é especificado com a função CAST, o comprimento padrão é 30.
  
Use **nchar** quando os tamanhos das entradas de dados de coluna são provavelmente serão similares.
  
Use **nvarchar** quando os tamanhos das entradas de dados de coluna provavelmente irão variar consideravelmente.
  
**sysname** é um tipo de dados de definidas pelo usuário e fornecido pelo sistema que é funcionalmente equivalente à **nvarchar (128)**, exceto que não é anulável. **sysname** é usado para fazer referência a nomes de objeto de banco de dados.
  
Objetos que usam **nchar** ou **nvarchar** recebem o agrupamento padrão do banco de dados, a menos que recebe um agrupamento específico usando a cláusula COLLATE.
  
SET ANSI_PADDING é sempre ON para **nchar** e **nvarchar**. SET ANSI_PADDING OFF não se aplica a **nchar** ou **nvarchar** tipos de dados.
  
Prefixo de constantes de cadeia de caracteres Unicode com a letra N. Sem o prefixo N, a cadeia de caracteres é convertida para a página de código padrão do banco de dados. Essa página de código padrão pode não reconhecer certos caracteres.
 
> [!NOTE]  
>  Quando prefixar uma constante de cadeia de caracteres com a letra N, a conversão implícita resultará em uma cadeia de caracteres Unicode se converter a constante não exceda o tamanho máximo para um tipo de dados de cadeia de caracteres Unicode (4.000). Caso contrário, a conversão implícita resultará em um grande-valor Unicode (max).
  
> [!WARNING]  
>  Cada nulas **varchar (max)** ou **nvarchar (max)** coluna requer 24 bytes de alocação fixa adicional que conta em relação ao limite de linha de 8.060 bytes durante uma operação de classificação. Isso pode criar um limite implícito para o número de nulos **varchar (max)** ou **nvarchar (max)** colunas que podem ser criadas em uma tabela. Nenhum erro especial é fornecido quando a tabela é criada (além do aviso comum de que o tamanho máximo da linha excede o máximo permitido de 8060 bytes) ou no momento da inserção de dados. Esse tamanho de linha pode causar erros (por exemplo, o erro 512) durante algumas operações normais, como uma atualização de chave de índice clusterizado ou classificações do conjunto de colunas completo, que os usuários não podem prever até que uma operação seja executada.  
  
## <a name="converting-character-data"></a>Convertendo dados character  
Para obter informações sobre como converter dados de caractere, consulte [char e varchar &#40; Transact-SQL &#41; ](../../t-sql/data-types/char-and-varchar-transact-sql.md).
  
## <a name="examples"></a>Exemplos  
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyNCharColumn nchar(15)  
,MyNVarCharColumn nvarchar(20)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (N'Test data', N'More test data');  
GO  
SELECT MyNCharColumn, MyNVarCharColumn  
FROM dbo.MyTable;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyNCharColumn   MyNVarCharColumn  
--------------- --------------------  
Test data       More test data  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[COMO &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET ANSI_PADDING &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Suporte a agrupamentos e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)
  
  
