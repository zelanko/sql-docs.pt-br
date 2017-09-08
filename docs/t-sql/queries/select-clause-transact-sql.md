---
title: "Cláusula SELECT (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT Clause
- SELECT_Clause_TSQL
- DISTINCT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- parentheses [SQL Server]
- identity columns [SQL Server], SELECT clause
- SELECT clause
- $IDENTITY keyword
- user-defined types [SQL Server], invoking methods and properties
- SELECT statement [SQL Server], processing orders
- clauses [SQL Server], SELECT
- $ROWGUID keyword
- queries [SQL Server], results
ms.assetid: 2616d800-4853-4cf1-af77-d32d68d8c2ef
caps.latest.revision: 54
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e8b6972868c221ec0368b689164eff740ae6f1a7
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="select-clause-transact-sql"></a>Cláusula SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Especifica as colunas a serem retornadas pela consulta.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SELECT [ ALL | DISTINCT ]  
[ TOP ( expression ) [ PERCENT ] [ WITH TIES ] ]   
<select_list>   
<select_list> ::=   
    {   
      *   
      | { table_name | view_name | table_alias }.*   
      | {  
          [ { table_name | view_name | table_alias }. ]  
               { column_name | $IDENTITY | $ROWGUID }   
          | udt_column_name [ { . | :: } { { property_name | field_name }   
            | method_name ( argument [ ,...n] ) } ]  
          | expression  
          [ [ AS ] column_alias ]   
         }  
      | column_alias = expression   
    } [ ,...n ]   
```  
  
## <a name="arguments"></a>Argumentos  
 **ALL**  
 Especifica que linhas duplicadas podem aparecer no conjunto de resultados. ALL é o padrão.  
  
 DISTINCT  
 Especifica que só linhas exclusivas podem aparecer no conjunto de resultados. Valores nulos são considerados iguais para os propósitos da palavra-chave DISTINCT.  
  
 Parte superior (*expressão* ) [%] [WITH TIES]  
 Indica que apenas um primeiro conjunto ou porcentagem de linhas especificado será retornado de um conjunto de resultados de consulta. *expression* pode ser um número ou uma porcentagem das linhas.  
  
 Para compatibilidade com versões anteriores, usando a parte superior *expressão* sem parênteses em SELECT instruções tem suporte, mas não é recomendável. Para obter mais informações, consulte [TOP &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
\<select_list > as colunas a serem selecionadas para o conjunto de resultados. A lista de seleções é uma série de lista de expressões separadas por vírgulas. O número máximo de expressões que pode ser especificado na lista de seleção é 4096.  
  
 \*  
 Especifica que todas as colunas de todas as tabelas e exibições na cláusula FROM devem ser retornadas. As colunas são retornadas por tabela ou exibição, conforme especificado na cláusula FROM, e na ordem em que existem na tabela ou exibição.  
  
 *table_name* | *view_name* | *tabela*_*alias*. *  
 Limita o escopo do \* para a tabela ou exibição especificada.  
  
 *nome da coluna*  
 É o nome de uma coluna a ser retornada. Qualificar *column_name* para impedir uma referência ambígua, como ocorre quando duas tabelas na cláusula FROM têm colunas com nomes duplicados. Por exemplo, as tabelas SalesOrderHeader e SalesOrderDetail no [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] banco de dados tanto têm uma coluna denominada ModifiedDate. Se as duas tabelas estão unidas em uma consulta, a data modificada das entradas de SalesOrderDetail pode ser especificada na lista de seleção como SalesOrderDetail.ModifiedDate.  
  
 *expressão*  
 É uma constante, função, qualquer combinação de nomes de coluna, constantes e funções conectadas por um operador ou operadores, ou uma subconsulta.  
  
 $IDENTITY  
 Retorna a coluna de identidade. Para obter mais informações, consulte [identidade &#40; Propriedade &#41; &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql-identity-property.md), [ALTER TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-table-transact-sql.md), e [criar tabela &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).  
  
 Se mais de uma tabela na cláusula FROM tiver uma coluna com a propriedade IDENTITY, $IDENTITY deverá ser qualificada com o nome específico da tabela, como T1.$IDENTITY.  
  
 $ROWGUID  
 Retorna a coluna do GUID da linha.  
  
 Se houver mais de uma tabela na cláusula FROM com a propriedade ROWGUIDCOL, $ROWGUID deverá ser qualificado com o nome específico da tabela, como T1.$ROWGUID.  
  
 *udt_column_name*  
 É o nome de uma coluna de tipo CLR (common language runtime) definida pelo usuário a ser retornada.  
  
> [!NOTE]  
>  O [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] retorna valores de tipo definidos pelo usuário em representação binária. Para retornar valores de tipo definido pelo usuário na cadeia de caracteres ou formato XML, use [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) ou [converter](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
 { . | :: }  
 Especifica um método, uma propriedade ou um campo de um tipo de dados CLR definido pelo usuário. Use. para um método de instância (não estático), propriedade ou campo. Use :: para um método estático, propriedade ou campo. Para invocar um método, uma propriedade ou um campo de um tipo de dados CLR definido pelo usuário, você deve ter a permissão EXECUTE no tipo.  
  
 *Property_Name*  
 É uma propriedade pública de *udt_column_name*.  
  
 *nome_do_campo*  
 É um membro de dados público *udt_column_name*.  
  
 *nome_do_método*  
 É um método público de *udt_column_name* que usa um ou mais argumentos. *nome_do_método* não pode ser um método modificador.  
  
 O exemplo a seguir seleciona os valores para a coluna `Location`, definida como tipo `point`, da tabela `Cities`, invocando um método de tipo denominado `Distance`:  
  
```  
CREATE TABLE dbo.Cities (  
     Name varchar(20),  
     State varchar(20),  
     Location point );  
GO  
DECLARE @p point (32, 23), @distance float;  
GO  
SELECT Location.Distance (@p)  
FROM Cities;  
```  
  
 *alias de column_*  
 Um nome alternativo para substituir o nome da coluna no conjunto de resultados da consulta. Por exemplo, um alias como Quantidade ou Quantidade até a Data ou Qtd pode ser especificado para uma coluna denominada quantidade.  
  
 Aliases também são usados para especificar nomes para os resultados de expressões, por exemplo:  
  
 `USE AdventureWorks2012`;  
  
 `GO`  
  
 `SELECT AVG(UnitPrice) AS [Average Price]`  
  
 `FROM Sales.SalesOrderDetail;`  
  
 *column_alias* pode ser usado em uma cláusula ORDER BY. Porém, não pode ser usado em uma cláusula WHERE, GROUP BY nem HAVING. Se a expressão de consulta faz parte de uma instrução DECLARE CURSOR, *column_alias* não pode ser usado na cláusula FOR UPDATE.  
  
## <a name="remarks"></a>Comentários  
 O comprimento dos dados retornados para **texto** ou **ntext** colunas incluídas na lista de seleção é definido para o menor valor dos seguintes: o tamanho real do **texto** coluna, a configuração de sessão TEXTSIZE padrão ou o limite de aplicativo codificado. Para alterar o comprimento do texto retornado para a sessão, use a instrução SET. Por padrão, o limite no comprimento de dados de texto retornados com uma instrução SELECT é 4.000 bytes.  
  
 O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] gerará a exceção 511 e reverterá a instrução atualmente em execução, se algum dos seguintes comportamentos ocorrer:  
  
-   A instrução SELECT produz uma linha de resultados ou uma tabela de trabalho intermediária que excede 8.060 bytes.  
  
-   A instrução DELETE, INSERT ou UPDATE tenta uma ação em uma linha que excede 8.060 bytes.  
  
 Ocorrerá um erro se nenhum nome de coluna for especificado para uma coluna criada por uma instrução SELECT INTO ou CREATE VIEW.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos SELECT &#40; Transact-SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)   
 [Expressões &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  

