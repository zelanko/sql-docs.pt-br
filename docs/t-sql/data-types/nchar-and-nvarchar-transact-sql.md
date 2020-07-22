---
title: nchar e nvarchar (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2019
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 63673258e2fa368544c6cc43158025770861a8f9
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555601"
---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar e nvarchar (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Tipos de dados de caractere que sejam de tamanho fixo, **nchar** ou de tamanho variável, **nvarchar**. A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], quando uma ordenação habilitada por [Caractere Suplementar (SC)](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters) é usada, esses tipos de dados armazenam o intervalo completo de dados de caractere [Unicode](../../relational-databases/collations/collation-and-unicode-support.md#Unicode_Defn) e usam a codificação de caracteres [UTF-16 ](https://www.wikipedia.org/wiki/UTF-16). Se uma ordenação não SC for especificada, então esses tipos de dados armazenarão somente o subconjunto de dados de caractere compatíveis com a codificação de caracteres [UCS-2](https://www.wikipedia.org/wiki/Universal_Coded_Character_Set#Encoding_forms).

## <a name="arguments"></a>Argumentos
**nchar** [ ( n ) ]  
Dados de cadeia de caracteres de tamanho fixo. *n* define o tamanho da cadeia de caracteres em pares-byte e deve ser um valor entre 1 a 4.000. O tamanho do armazenamento é duas vezes *n* bytes. Para a codificação [UCS-2](https://www.wikipedia.org/wiki/UTF-16#U+0000_to_U+D7FF_and_U+E000_to_U+FFFF), o tamanho de armazenamento é duas vezes *n* bytes e a quantidade de caracteres que pode ser armazenada também é *n*. Para a codificação UTF-16, o tamanho de armazenamento ainda é duas vezes *n* bytes, mas a quantidade de caracteres que pode ser armazenada pode ser menor que *n* porque os Caracteres Suplementares usam dois pares-byte (também chamados de [par alternativo](https://www.wikipedia.org/wiki/UTF-16#U+010000_to_U+10FFFF)). Os sinônimos ISO para **nchar** são **char nacional** e **caractere nacional**.
  
**nvarchar** [ ( n | **max** ) ]  
Dados de cadeia de caracteres de tamanho variável. *n* define o tamanho da cadeia de caracteres em pares-byte e pode ser um valor entre 1 a 4.000. **max** indica que o tamanho de armazenamento máximo é de 2^30-1 caracteres (2 GB). O tamanho do armazenamento é duas vezes *n* bytes + 2 bytes. Para a codificação [UCS-2](https://www.wikipedia.org/wiki/UTF-16#U+0000_to_U+D7FF_and_U+E000_to_U+FFFF), o tamanho de armazenamento é duas vezes *n* bytes + 2 bytes e a quantidade de caracteres que pode ser armazenada também é *n*. Para a codificação UTF-16, o tamanho de armazenamento ainda é duas vezes *n* bytes + 2 bytes, mas a quantidade de caracteres que pode ser armazenada pode ser menor que *n* porque os Caracteres Suplementares usam dois pares-byte (também chamados de [par alternativo](https://www.wikipedia.org/wiki/UTF-16#U+010000_to_U+10FFFF)). Os sinônimos ISO para **nvarchar** são **national char varying** e **national character varying**.
  
## <a name="remarks"></a>Comentários  
Um equívoco comum é considerar que em [NCHAR(*n*) e NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), *n* define o número de caracteres. Mas em [NCHAR(*n*) e NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), o *n* define o comprimento da cadeia de caracteres em **pares-byte** (0 a 4.000). *n* nunca define números de caracteres que podem ser armazenados. Isso é semelhante à definição de [CHAR(*n*) e VARCHAR(*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md).   
O equívoco ocorre porque, ao usar caracteres definidos no intervalo Unicode 0 – 65.535, um caractere pode ser armazenado por cada par-byte. No entanto, em intervalos Unicode mais altos (65.536 – 1.114.111), um caractere pode usar dois pares-byte. Por exemplo, em uma coluna definida como NCHAR(10), o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] pode armazenar 10 caracteres que usam um par-byte (intervalo Unicode 0 – 65.535), mas menos de 10 caracteres ao usar dois pares-byte (o intervalo Unicode 65.536 – 1.114.111). Para obter mais informações sobre o armazenamento e os intervalos de caracteres Unicode, confira [Diferenças de armazenamento entre UTF-8 e UTF-16](../../relational-databases/collations/collation-and-unicode-support.md#storage_differences).     

Quando *n* não é especificado em uma definição de dados ou instrução de declaração de variável, o tamanho padrão é 1. Quando *n* não é especificado com a função CAST, o tamanho padrão é 30.

Se você usar **nchar** ou **nvarchar**, recomendamos que:
- Use **nchar** quando os tamanhos das entradas de dados de coluna forem consistentes.  
- Use **nvarchar** quando os tamanhos das entradas de dados de coluna variarem consideravelmente.  
- Use **nvarchar(max)** quando os tamanhos das entradas de dados de coluna variarem consideravelmente e o tamanho da cadeia de caracteres puder exceder 4.000 pares-bytes.  
  
**sysname** é um tipo de dados definido pelo usuário e fornecido pelo sistema que é funcionalmente equivalente a **nvarchar(128)** , com exceção de que não permite valor nulo. **sysname** é usado para referenciar nomes de objetos de banco de dados.
  
Os objetos que usam **nchar** ou **nvarchar** recebem a ordenação padrão do banco de dados, a menos que uma ordenação específica seja atribuída com o uso da cláusula COLLATE.
  
SET ANSI_PADDING é sempre ON para **nchar** e **nvarchar**. SET ANSI_PADDING OFF não se aplica aos tipos de dados **nchar** ou **nvarchar**.
  
Prefixe uma constante de cadeia de caracteres Unicode com a letra N para sinalizar a entrada UCS-2 ou UTF-16, dependendo de se uma ordenação SC for ou não usada. Sem o prefixo N, a cadeia de caracteres é convertida para a página de código padrão do banco de dados, que talvez não reconheça determinados caracteres. A partir do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], quando uma ordenação habilitada por UTF-8 é usada, a página de código padrão é capaz de armazenar um conjunto de caracteres UNICODE UTF-8. 
 
> [!NOTE]  
> Ao prefixar uma constante de cadeia de caracteres com a letra N, a conversão implícita resultará em uma cadeia de caracteres UCS-2 ou UTF-16, caso a constante a ser convertida não exceda o tamanho máximo para o tipo de dados de cadeia de caracteres nvarchar (4.000). Caso contrário, a conversão implícita resultará em um nvarchar de valor grande (max).
  
> [!WARNING]  
> Cada coluna **varchar(max)** ou **nvarchar(max)** não nula requer 24 bytes de alocação fixa adicional, que conta para o limite de linhas de 8.060 bytes durante uma operação de classificação. Esses bytes adicionais podem criar um limite implícito para o número de colunas **varchar(max)** ou **nvarchar(max)** não nulas em uma tabela. Nenhum erro especial é fornecido quando a tabela é criada (além do aviso comum de que o tamanho máximo da linha excede o máximo permitido de 8.060 bytes) ou no momento da inserção de dados. Esse grande tamanho de linha pode causar erros (como o erro 512) imprevistos pelos usuários durante algumas operações normais.  Dois exemplos de operações são uma atualização de chave de índice clusterizado ou classificações do conjunto de colunas completo.
  
## <a name="converting-character-data"></a>Convertendo dados character  
Para obter informações sobre como converter dados de caractere, consulte [char e varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md).
  
## <a name="see-also"></a>Confira também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)    
[Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)     
[Conjuntos de caracteres multibyte e de byte único](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)  
  
