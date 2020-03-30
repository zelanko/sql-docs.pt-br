---
title: uniqueidentifier (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- uniqueidentifier
- uniqueidentifier_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- uniqueidentifier data type
- globally unique identifiers [SQL Server]
- GUIDs [SQL Server]
ms.assetid: b026035b-f3d2-4d70-989d-3884b4ca0233
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5471791b3f75130bc2fb262a05683aa953f7f3a8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68000443"
---
# <a name="uniqueidentifier-transact-sql"></a>uniqueidentifier (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

É um GUID de 16 bytes.
  
## <a name="remarks"></a>Comentários  
Uma coluna ou variável local de tipo de dados **uniqueidentifier** podem ser inicializadas com um valor das seguintes maneiras:
-   Usando as funções [NEWID](../../t-sql/functions/newid-transact-sql.md) ou [NEWSEQUENTIALID](../../t-sql/functions/newsequentialid-transact-sql.md).    
-   Ao converter de uma constante de cadeia de caracteres no formato *xxxxxxxx*-*xxxx*-*xxxx*-*xxxx*-*xxxxxxxxxxxx*, em que cada *x* é um dígito hexadecimal no intervalo 0–9 ou a–f. Por exemplo, 6F9619FF-8B86-D011-B42D-00C04FC964FF é um valor **uniqueidentifier** válido.  
  
Operadores de comparação podem ser usados com valores de **uniqueidentifier**. Entretanto, a ordenação não é implementada comparando os padrões de bit dos dois valores. As únicas operações que podem ser executadas com um valor **uniqueidentifier** são comparações (=, <>, \<, >, \<=, >=) e verificações para NULL (IS NULL e IS NOT NULL). Nenhum outro operador aritmético pode ser usado. Todas as restrições de coluna e propriedades, exceto IDENTITY, podem ser usadas no tipo de dados **uniqueidentifier**.
  
A replicação de mesclagem e a replicação transacional com assinaturas de atualização usam colunas **uniqueidentifier** para garantir que as linhas sejam identificadas com exclusividade em várias cópias da tabela.
  
## <a name="converting-uniqueidentifier-data"></a>Convertendo dados uniqueidentifier  
O tipo **uniqueidentifier** é considerado um tipo de caractere para fins de conversão de uma expressão de caractere e, portanto, está sujeito às regras de truncamento para conversão em um tipo de caractere. Ou seja, quando expressões de caractere são convertidas em um tipo de dados de caractere de um tamanho diferente, os valores muito longos para o novo tipo de dados são truncados. Consulte a seção Exemplos.
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições

Essas ferramentas e recursos não são compatíveis com o tipo de dados `uniqueidentifier`:
- PolyBase
- [ferramenta de carregamento de dwloader](https://msdn.microsoft.com/sql/analytics-platform-system/dwloader) para Parallel Data Warehouse

## <a name="examples"></a>Exemplos  
O exemplo a seguir converte um valor `uniqueidentifier` em um tipo de dados `char`.
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
O exemplo a seguir demonstra o truncamento de dados quando o valor é muito longo para o tipo de dados da conversão. Como o tipo **uniqueidentifier** é limitado a 36 caracteres, os caracteres que excedem esse comprimento ficam truncados.
  
```sql
DECLARE @ID nvarchar(max) = N'0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong';  
SELECT @ID, CONVERT(uniqueidentifier, @ID) AS TruncatedValue;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
String                                       TruncatedValue  
-------------------------------------------- ------------------------------------  
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Confira também
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[NEWID &#40;Transact-SQL&#41;](../../t-sql/functions/newid-transact-sql.md)  
[NEWSEQUENTIALID &#40;Transact-SQL&#41;](../../t-sql/functions/newsequentialid-transact-sql.md)    
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)
  
  
