---
title: Criar índices XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- indexes [XML in SQL Server]
- XML indexes [SQL Server], creating
ms.assetid: 6ecac598-355d-4408-baf7-1b2e8d4cf7c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7da89810a92c14f5b59ebcd546c4fb4cfa256f02
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527509"
---
# <a name="create-xml-indexes"></a>Criar índices XML
  Este tópico descreve como criar índices XML primários e secundários.  
  
## <a name="creating-a-primary-xml-index"></a>Criando um índice XML primário  
 Para criar um índice XML primário, use a instrução DDL [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)]. Nem todas as opções disponíveis para índices não XML têm suporte em índices XML.  
  
 Observe o seguinte ao criar um índice XML:  
  
-   Para criar um índice XML, a tabela que contém a coluna XML que está sendo indexada, chamada de tabela base, deve ter um índice clusterizado na chave primária. Isso garante que se a tabela base estiver particionada, o índice XML primário poderá ser particionado usando o mesmo esquema e função de particionamento.  
  
-   Se existir um índice XML, a chave primária clusterizada da tabela não poderá ser modificada. É necessário descartar todos os índices XML da tabela para modificar a chave primária.  
  
-   Um índice XML primário pode ser criado em uma única coluna de tipo `xml`. Não é possível criar nenhum outro tipo de índice com a coluna de tipo XML como uma coluna de chave. No entanto, é possível incluir a coluna de tipo `xml` L em um índice não XML. Cada coluna de tipo `xml` em uma tabela pode ter seu próprio índice XML primário. Porém, apenas um índice XML primário por coluna de tipo `xml` é permitido.  
  
-   Índices XML existem no mesmo namespace que índices não XML. Portanto, não é possível ter um índice XML e um índice não XML na mesma tabela com o mesmo nome.  
  
-   As opções IGNORE_DUP_KEY e ONLINE sempre estão definidas como OFF para índices XML. Essas opções podem ser especificadas com um valor de OFF.  
  
-   As informações de particionamento ou de grupo de arquivos da tabela do usuário são aplicadas ao índice XML. Usuários não podem especificá-las separadamente em um índice XML.  
  
-   A opção de índice DROP_EXISTING pode descartar um índice XML primário e criar um novo índice XML primário ou descartar um índice XML secundário e criar um novo índice XML secundário. No entanto, essa opção não pode descartar um índice XML secundário para criar um índice XML primário novo ou vice-versa.  
  
-   Nomes de índice XML primário têm as mesmas restrições que nomes de exibição.  
  
 Você não pode criar um índice XML em um `xml` tipo de coluna em uma exibição em um **tabela** com valor de variável com `xml` colunas de tipo ou `xml` variáveis do tipo.  
  
-   Para alterar uma coluna de tipo `xml` de XML sem-tipo para XML com tipo ou vice-versa, usando a opção ALTER TABLE ALTER COLUMN, nenhum índice XML deve existir na coluna. Se existir um índice, ele deve ser descartado antes da tentativa de alterar o tipo de coluna.  
  
-   A opção ARITHABORT deve ser definida como ON quando um índice XML é criado. Para consultar, inserir, excluir ou atualizar valores na coluna XML usando métodos de tipo de dados XML, a mesma opção deve ser definida na conexão. Caso contrário, haverá falha nos métodos de tipo de dados XML.  
  
    > [!NOTE]  
    >  Informações sobre um índice XML podem ser localizadas em exibições do catálogo. No entanto, não há suporte para **sp_helpindex** . Os exemplos fornecidos mais adiante neste tópico mostram como consultar as exibições do catálogo para localizar informações sobre índices XML.  
  
 Ao criar ou recriar um índice XML primário em uma coluna de tipo de dados XML que contém valores de tipos de Esquema XML **xs:date** ou **xs:dateTime** (ou quaisquer subtipos desses tipos) que têm um ano menor que 1, haverá falha na criação do índice no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] permitiu esses valores; portanto, este problema pode ocorrer durante a criação de índices em um banco de dados gerado no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações, consulte [Comparar XML digitado com XML não digitado](../xml/compare-typed-xml-to-untyped-xml.md).  
  
### <a name="example-creating-a-primary-xml-index"></a>Exemplo: Criando um índice XML primário  
 A tabela T (pk INT PRIMARY KEY, xCol XML) com uma coluna XML sem-tipo é usada na maioria dos exemplos. Esses podem ser estendidos para XML com tipo de uma maneira direta. Para simplificar, as consultas são descritas para instâncias de dados XML, conforme mostrado a seguir:  
  
```  
<book genre="security" publicationdate="2002" ISBN="0-7356-1588-2">  
   <title>Writing Secure Code</title>  
   <author>  
      <first-name>Michael</first-name>  
      <last-name>Howard</last-name>  
   </author>  
   <author>  
      <first-name>David</first-name>  
      <last-name>LeBlanc</last-name>  
   </author>  
   <price>39.99</price>  
</book>  
```  
  
 A instrução a seguir cria um índice XML, chamado idx_xCol, na coluna XML xCol da tabela T:  
  
```  
CREATE PRIMARY XML INDEX idx_xCol on T (xCol)  
```  
  
## <a name="creating-a-secondary-xml-index"></a>Criando um índice XML secundário  
 Use a instrução DDL [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] para criar índices XML secundários e especificar o tipo do índice XML secundário desejado.  
  
 Observe o seguinte ao criar índices XML secundários:  
  
-   São permitidas todas as opções de indexação que se aplicam a um índice não clusterizado, exceto IGNORE_DUP_KEY e ONLINE, em índices XML secundários. As duas opções sempre devem ser definidas como OFF para índices XML secundários.  
  
-   Os índices secundários são particionados exatamente como o índice XML primário.  
  
-   DROP_EXISTING pode descartar um índice secundário e criar outro índice secundário na tabela de usuário.  
  
 É possível consultar a exibição de catálogo **sys.xml_indexes** para recuperar informações do índice XML. Observe que a coluna **secondary_type_desc** na exibição de catálogo **sys.xml_indexes** fornece o tipo de índice secundário:  
  
```  
SELECT  *   
FROM    sys.xml_indexes;  
```  
  
 Os valores retornados na coluna **secondary_type_desc** podem ser NULL, PATH, VALUE ou PROPERTY. Para o índice XML primário, o valor retornado é NULL.  
  
### <a name="example-creating-secondary-xml-indexes"></a>Exemplo: Criando índices XML secundários  
 O exemplo a seguir ilustra como são criados índices XML secundários. O exemplo também mostra informações sobre os índices XML criados.  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML);  
GO  
-- Create primary index.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol);  
GO  
-- Create secondary indexes (PATH, VALUE, PROPERTY).  
CREATE XML INDEX PIdx_T_XmlCol_PATH ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR PATH;  
GO  
CREATE XML INDEX PIdx_T_XmlCol_VALUE ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR VALUE;  
GO  
CREATE XML INDEX PIdx_T_XmlCol_PROPERTY ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR PROPERTY;  
GO  
```  
  
 É possível consultar o `sys.xml_indexes` para recuperar informações de índices XML. A coluna `secondary_type_desc` fornece o tipo de índice secundário.  
  
```  
SELECT  *   
FROM    sys.xml_indexes;  
```  
  
 Também é possível consultar a exibição do catálogo para obter informações de índice.  
  
```  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T');  
```  
  
 É possível adicionar dados de exemplo e revisar as informações do índice XML.  
  
```  
INSERT INTO T VALUES (1,  
'<doc id="123">  
<sections>  
<section num="2">  
<heading>Background</heading>  
</section>  
<section num="3">  
<heading>Sort</heading>  
</section>  
<section num="4">  
<heading>Search</heading>  
</section>  
</sections>  
</doc>');  
GO  
-- Check XML index information.  
SELECT *  
FROM   sys.dm_db_index_physical_stats (db_id(), object_id('T'), NULL, NULL, 'DETAILED');  
GO  
-- Space usage of primary XML index  
DECLARE @index_id int;  
SELECT  @index_id = i.index_id  
FROM    sys.xml_indexes i   
WHERE   i.name = 'PIdx_T_XmlCol' and object_name(i.object_id) = 'T';  
  
SELECT *  
FROM sys.dm_db_index_physical_stats (db_id(), object_id('T') , @index_id, DEFAULT, 'DETAILED');  
go  
--- Space usage of secondary XML index (for example PATH secondary index)  PIdx_T_XmlCol_PATH  
DECLARE @index_id int;  
SELECT  @index_id = i.index_id   
FROM    sys.xml_indexes i   
WHERE  i.name = 'PIdx_T_XmlCol_PATH' and object_name(i.object_id) = 'T';  
  
SELECT *  
FROM sys.dm_db_index_physical_stats (db_id(), object_id('T') , @index_id, DEFAULT, 'DETAILED');  
go  
  
-- Space usage of all secondary XML indexes for a particular table  
SELECT i.name, object_name(i.object_id), stats.*   
FROM   sys.dm_db_index_physical_stats (db_id(), object_id('T'), NULL, DEFAULT, 'DETAILED') stats  
JOIN sys.xml_indexes i ON (stats.object_id = i.object_id and stats.index_id = i.index_id)  
WHERE secondary_type is not null;  
-- Drop secondary indexes.  
DROP INDEX PIdx_T_XmlCol_PATH ON T;  
GO  
DROP INDEX PIdx_T_XmlCol_VALUE ON T;  
GO  
DROP INDEX PIdx_T_XmlCol_PROPERTY ON T;  
GO  
-- Drop primary index.  
DROP INDEX PIdx_T_XmlCol ON T;  
-- Drop table T.  
DROP TABLE T;  
Go  
```  
  
## <a name="see-also"></a>Consulte também  
 [Índices XML &#40;SQL Server&#41;](xml-indexes-sql-server.md)   
 [Dados XML &#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
