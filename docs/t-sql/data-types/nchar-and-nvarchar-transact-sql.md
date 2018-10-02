---
title: nchar e nvarchar (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- nvarchar data type
- nchar data type
ms.assetid: 81ee5637-ee31-4c4d-96d0-56c26a742354
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5ca8eb44756561bd8a4a4a0ddce43f6f321bdf72
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47733494"
---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar e nvarchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Os tipos de dados de caractere que são dados Unicode de comprimento fixo, **nchar** ou de tamanho variável, **nvarchar**, e usam o conjunto de caracteres UNICODE UCS-2.
  
## <a name="arguments"></a>Argumentos  
**nchar** [ ( n ) ]  
Dados de cadeia de caracteres Unicode de comprimento fixo. *n* define o tamanho da cadeia de caracteres e deve ser um valor de 1 a 4.000. O tamanho do armazenamento é duas vezes *n* bytes. Quando a página de código de agrupamento usar caracteres de dois bytes, o tamanho do armazenamento ainda será *n* bytes. Dependendo da cadeia de caracteres, o tamanho do armazenamento de *n* bytes pode ser inferior ao valor especificado para *n*. Os sinônimos ISO para **nchar** são **char nacional** e **caractere nacional**.
  
**nvarchar** [ ( n | **max** ) ]  
Dados de cadeia de caracteres Unicode de comprimento variável. *n* define o tamanho da cadeia de caracteres e pode ser um valor de 1 a 4.000. **max** indica que o tamanho de armazenamento máximo é de 2^30-1 caracteres.  O tamanho de armazenamento máximo em bytes é 2 GB. O tamanho de armazenamento real, em bytes, é duas vezes o número de caracteres digitados + 2 bytes. Os sinônimos ISO para **nvarchar** são **national char varying** e **national character varying**.
  
## <a name="remarks"></a>Remarks  
Quando *n* não é especificado em uma definição de dados ou instrução de declaração de variável, o tamanho padrão é 1. Quando *n* não é especificado com a função CAST, o tamanho padrão é 30.
  
Use **nchar** quando os tamanhos das entradas de dados de coluna provavelmente serão similares.
  
Use **nvarchar** quando os tamanhos das entradas de dados de coluna provavelmente variarão consideravelmente.
  
**sysname** é um tipo de dados definido pelo usuário e fornecido pelo sistema que é funcionalmente equivalente a **nvarchar(128)**, com exceção de que não permite valor nulo. **sysname** é usado para referenciar nomes de objetos de banco de dados.
  
Os objetos que usam **nchar** ou **nvarchar** recebem o agrupamento padrão do banco de dados, a menos que um agrupamento específico seja atribuído com o uso da cláusula COLLATE.
  
SET ANSI_PADDING é sempre ON para **nchar** e **nvarchar**. SET ANSI_PADDING OFF não se aplica aos tipos de dados **nchar** ou **nvarchar**.
  
Prefixe constantes de cadeia de caracteres Unicode com a letra N. Sem o prefixo N, a cadeia é convertida na página de código padrão do banco de dados. Essa página de código padrão pode não reconhecer certos caracteres.
 
> [!NOTE]  
>  Ao prefixar uma constante de cadeia de caracteres com a letra N, a conversão implícita resultará em uma cadeia de caracteres Unicode, caso a constante a ser convertida não exceda o tamanho máximo para um tipo de dados de cadeia de caracteres Unicode (4.000). Caso contrário, a conversão implícita resultará em um valor grande Unicode (max).
  
> [!WARNING]  
>  Cada coluna **varchar(max)** ou **nvarchar(max)** não nula requer 24 bytes de alocação fixa adicional, que conta para o limite de linhas de 8.060 bytes durante uma operação de classificação. Esses bytes adicionais podem criar um limite implícito para o número de colunas **varchar(max)** ou **nvarchar(max)** não nulas em uma tabela. Nenhum erro especial é fornecido quando a tabela é criada (além do aviso comum de que o tamanho máximo da linha excede o máximo permitido de 8060 bytes) ou no momento da inserção de dados. Esse grande tamanho de linha pode causar erros (como o erro 512) imprevistos pelos usuários durante algumas operações normais.  Dois exemplos de operações são uma atualização de chave de índice clusterizado ou classificações do conjunto de colunas completo.
  
## <a name="converting-character-data"></a>Convertendo dados character  
Para obter informações sobre como converter dados de caractere, consulte [char e varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md).
  
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
  
## <a name="see-also"></a>Confira também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Suporte a agrupamentos e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)
  
  
