---
title: Usar XML em colunas computadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- computed columns, XML
- XML [SQL Server], computed columns
ms.assetid: 1313b889-69b4-4018-9868-0496dd83bf44
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b9af73a4ad0a0dbc1c71d6f2cd0a9e39aa035ab4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020189"
---
# <a name="use-xml-in-computed-columns"></a>Usar XML em colunas computadas
  Instâncias XML ser exibidas como uma origem de uma coluna computada ou como um tipo de coluna computada. Os exemplos neste tópico mostram como usar XML com colunas computadas.  
  
## <a name="creating-computed-columns-from-xml-columns"></a>Criando colunas computadas de colunas XML  
 Na instrução `CREATE TABLE` a seguir, uma coluna de tipo `xml` (`col2`) é computada a partir de `col1`:  
  
```  
CREATE TABLE T(col1 varchar(max), col2 AS CAST(col1 AS xml) )    
```  
  
 O tipo de dados `xml` também pode ser exibido como uma origem ao criar uma coluna computada, conforme mostrado na seguinte instrução `CREATE TABLE` :  
  
```  
CREATE TABLE T (col1 xml, col2 as cast(col1 as varchar(1000) ))   
```  
  
 É possível criar uma coluna computada extraindo um valor de uma coluna de tipo `xml` , conforme mostrado no exemplo a seguir. Como os métodos do tipo de dados `xml` não podem ser usados diretamente ao criar colunas computadas, o exemplo primeiro define uma função (`my_udf`) que retorna um valor de uma instância XML. A função encapsula o método `value()` do tipo `xml` . Em seguida, o nome da função é especificado na instrução `CREATE TABLE` da coluna computada.  
  
```  
CREATE FUNCTION my_udf(@var xml) returns int  
AS BEGIN   
RETURN @var.value('(/ProductDescription/@ProductModelID)[1]' , 'int')  
END  
GO  
-- Use the function in CREATE TABLE.  
CREATE TABLE T (col1 xml, col2 as dbo.my_udf(col1) )  
GO  
-- Try adding a row.   
INSERT INTO T values('<ProductDescription ProductModelID="1" />')  
GO  
-- Verify results.  
SELECT col2, col1  
FROM T  
  
```  
  
 Como no exemplo anterior, o exemplo a seguir define uma função para retornar uma instância de tipo `xml` para uma coluna computada. Dentro da função, o método `query()` do tipo de dados `xml` recupera um valor de um parâmetro de tipo `xml` .  
  
```  
CREATE FUNCTION my_udf(@var xml)   
  RETURNS xml AS   
BEGIN   
   RETURN @var.query('ProductDescription/Features')  
END  
```  
  
 Na instrução `CREATE TABLE` a seguir, `Col2` é uma coluna computada que usa os dados XML (elemento`<Features>` ) que são retornados pela função:  
  
```  
CREATE TABLE T (Col1 xml, Col2 as dbo.my_udf(Col1) )  
-- Insert a row in table T.  
INSERT INTO T VALUES('  
<ProductDescription ProductModelID="1" >  
  <Features>  
    <Feature1>description</Feature1>  
    <Feature2>description</Feature2>  
  </Features>  
</ProductDescription>')  
-- Verify the results.  
SELECT *  
FROM T  
```  
  
### <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Promover valores XML frequentemente usados com colunas computadas](promote-frequently-used-xml-values-with-computed-columns.md)|Descreve como usar promoção de propriedades com colunas computadas e tabelas de propriedades.|  
  
  