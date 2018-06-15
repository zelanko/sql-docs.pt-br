---
title: Promover valores XML usados frequentemente com colunas computadas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- promoting properties [XML in SQL Server]
- property promotion [XML in SQL Server]
ms.assetid: f5111896-c2fd-4209-b500-f2baa45489ad
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b02df9c27dfc406bec621d68936ac85b6b949406
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33015813"
---
# <a name="promote-frequently-used-xml-values-with-computed-columns"></a>Promover valores XML frequentemente usados com colunas computadas
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Se as consultas forem feitas principalmente em um pequeno número de valores de elementos e atributos, você poderá desejar promover essas quantidades em colunas relacionais. Isso é útil quando consultas são emitidas em uma pequena parte dos dados XML enquanto toda a instância XML é recuperada. A criação de um índice XML na coluna XML não é necessária. Em vez disso, a coluna promovida pode ser indexada. As consultas devem ser escritas para usar a coluna promovida. Isto é, o otimizador de consultas não destina consultas novamente na coluna XML para a coluna promovida.  
  
 A coluna promovida pode ser uma coluna computada na mesma tabela ou ser uma coluna separada, mantida pelo usuário em uma tabela. Isso é suficiente quando valores singleton são promovidos de cada instância XML. No entanto para propriedades com vários valores, é necessário criar uma tabela separada para a propriedade, conforme descrito na seção a seguir.  
  
## <a name="computed-column-based-on-the-xml-data-type"></a>Coluna computada com base no tipo de dados xml  
 Uma coluna computada pode ser criada usando uma função definida pelo usuário que invoca métodos de tipo de dados **xml** . O tipo da coluna computada pode ser qualquer tipo SQL, inclusive XML. Isso é ilustrado no exemplo a seguir.  
  
### <a name="example-computed-column-based-on-the-xml-data-type-method"></a>Exemplo: Coluna computada com base no método do tipo de dados xml  
 Crie a função definida pelo usuário para um número ISBN de livro:  
  
```  
CREATE FUNCTION udf_get_book_ISBN (@xData xml)  
RETURNS varchar(20)  
BEGIN  
   DECLARE @ISBN   varchar(20)  
   SELECT @ISBN = @xData.value('/book[1]/@ISBN', 'varchar(20)')  
   RETURN @ISBN   
END  
```  
  
 Adicione uma coluna computada à tabela para o ISBN:  
  
```  
ALTER TABLE      T  
ADD   ISBN AS dbo.udf_get_book_ISBN(xCol)  
```  
  
 A coluna computada pode ser indexada de maneira normal.  
  
### <a name="example-queries-on-a-computed-column-based-on-xml-data-type-methods"></a>Exemplo: Consultas em uma coluna computada com base em métodos de tipo de dados xml  
 Para obter o <`book`> cujo ISBN é 0-7356-1588-2:  
  
```  
SELECT xCol  
FROM   T  
WHERE  xCol.exist('/book/@ISBN[. = "0-7356-1588-2"]') = 1  
```  
  
 A consulta na coluna XML pode ser reescrita para usar a coluna computada da seguinte maneira:  
  
```  
SELECT xCol  
FROM   T  
WHERE  ISBN = '0-7356-1588-2'  
```  
  
 É possível criar uma função definida pelo usuário para retornar o tipo de dados **xml** e uma coluna computada usando a função definida pelo usuário. No entanto não é possível criar um índice XML na coluna XML computada.  
  
## <a name="creating-property-tables"></a>Criando tabelas de propriedades  
 Você pode desejar promover algumas das propriedades com vários valores de seus dados XML em uma ou mais tabelas, criar índices nessas tabelas e destinar suas consultas novamente para usá-las. Um cenário típico é aquele em que um pequeno número propriedades cobre a maior parte da carga de trabalho das consultas. É possível fazer o seguinte:  
  
-   Crie uma ou mais tabelas para manter as propriedades com vários valores. Você pode descobrir que é conveniente armazenar uma propriedade por tabela e duplicar a chave primária da tabela base nas tabelas de propriedades para junção retroativa com a tabela base.  
  
-   Para manter a ordem relativa das propriedades, você precisa introduzir uma coluna separada para a ordem relativa.  
  
-   Crie gatilhos na coluna XML para manter as tabelas de propriedades. Dentro dos gatilhos, proceda de uma das seguintes maneiras:  
  
    -   Use métodos de tipo de dados **xml** , como **nodes()** e **value()**, para inserir e excluir linhas das tabelas de propriedades.  
  
    -   Crie funções com valor de tabela de streaming no CLR (Common Language Runtime) para inserir e excluir linhas das tabelas de propriedades.  
  
    -   Escreva consultas para acesso do SQL às tabelas de propriedades e para acesso do XML à coluna XML na tabela base, com junções entre as tabelas usando suas chaves primárias.  
  
### <a name="example-create-a-property-table"></a>Exemplo: Crie uma tabela de propriedades  
 Para ilustração, assuma que você quer promover o nome dos autores. Os livros têm um ou mais autores, de forma que nome é uma propriedade com vários valores. Cada nome é armazenado em uma linha separada de uma tabela de propriedades. A chave primária da tabela base é duplicada na tabela de propriedades para junção retroativa.  
  
```  
create table tblPropAuthor (propPK int, propAuthor varchar(max))  
```  
  
### <a name="example-create-a-user-defined-function-to-generate-a-rowset-from-an-xml-instance"></a>Exemplo: Crie uma função definida pelo usuário para gerar um conjunto de linhas de uma instância XML  
 A função com valor de tabela a seguir, udf_XML2Table, aceita um valor de chave primária e uma instância XML. Ela recupera o nome de todos os autores dos elementos de <`book`> e retorna um conjunto de linhas de chave primária, primeiros pares de nomes.  
  
```  
create function udf_XML2Table (@pk int, @xCol xml)  
returns @ret_Table table (propPK int, propAuthor varchar(max))  
with schemabinding  
as  
begin  
      insert into @ret_Table   
      select @pk, nref.value('.', 'varchar(max)')  
      from   @xCol.nodes('/book/author/first-name') R(nref)  
      return  
end  
```  
  
### <a name="example-create-triggers-to-populate-a-property-table"></a>Exemplo: Crie gatilhos para popular uma tabela de propriedades  
 O gatilho de inserção insere linhas na tabela de propriedades:  
  
```  
create trigger trg_docs_INS on T for insert  
as  
      declare @wantedXML xml  
      declare @FK int  
      select @wantedXML = xCol from inserted  
      select @FK = PK from inserted  
  
   insert into tblPropAuthor  
   select * from dbo.udf_XML2Table(@FK, @wantedXML)  
```  
  
 O gatilho de exclusão exclui as linhas da tabela de propriedades com base no valor da chave primária das linhas excluídas:  
  
```  
create trigger trg_docs_DEL on T for delete  
as  
   declare @FK int  
   select @FK = PK from deleted  
   delete tblPropAuthor where propPK = @FK  
```  
  
 O gatilho de atualização exclui as linhas existentes da tabela de propriedades correspondentes à instância XML atualizada e insere novas linhas na tabela de propriedades:  
  
```  
create trigger trg_docs_UPD  
on T  
for update  
as  
if update(xCol) or update(pk)  
begin  
      declare @FK int  
      declare @wantedXML xml  
      select @FK = PK from deleted  
      delete tblPropAuthor where propPK = @FK  
  
   select @wantedXML = xCol from inserted  
   select @FK = pk from inserted  
  
   insert into tblPropAuthor   
      select * from dbo.udf_XML2Table(@FK, @wantedXML)  
end  
```  
  
### <a name="example-find-xml-instances-whose-authors-have-the-same-first-name"></a>Exemplo: Localize instâncias XML cujos autores têm o mesmo nome  
 A consulta pode ser formada na coluna XML. Como alternativa, é possível pesquisar o nome "David" na tabela de propriedades e executar uma junção retroativa com a tabela base para retornar a instância XML. Por exemplo:  
  
```  
SELECT xCol   
FROM     T JOIN tblPropAuthor ON T.pk = tblPropAuthor.propPK  
WHERE    tblPropAuthor.propAuthor = 'David'  
```  
  
### <a name="example-solution-using-the-clr-streaming-table-valued-function"></a>Exemplo: Solução usando a função com valor de tabela de streaming de CLR  
 Esta solução é composta das seguintes etapas:  
  
1.  Definir uma classe CLR, SqlReaderBase, que implementa ISqlReader e gera um streaming, saída com valor de tabela, aplicando uma expressão de caminho em uma instância XML.  
  
2.  Crie um assembly e uma função definida pelo usuário de Transact-SQL para iniciar a classe CLR.  
  
3.  Defina os gatilhos de inserção, atualização e exclusão usando a função definida pelo usuário para manter uma tabela de propriedades.  
  
 Para fazer isso, primeiro crie a função CLR de streaming. O tipo de dados **xml** é exposto como um SqlXml de classe gerenciada no ADO.NET e dá suporte ao método **CreateReader()** que retorna um XmlReader.  
  
> [!NOTE]  
>  O código de exemplo nesta seção usa XPathDocument e XPathNavigator. Isso força você a carregar todos os documentos XML na memória. Se estiver usando código semelhante em seu aplicativo para processar vários documentos XML grandes, esse código não será escalável. Em vez disso, mantenha as alocações de memória pequenas e use interfaces de streaming sempre que possível. Para obter mais informações sobre o desempenho, veja [Arquitetura da integração CLR](http://msdn.microsoft.com/library/05e4b872-3d21-46de-b4d5-739b5f2a0cf9).  
  
```  
public class c_streaming_xml_tvf {  
   public static ISqlReader streaming_xml_tvf   
(SqlXml xmlDoc, string pathExpression) {  
      return (new TestSqlReaderBase (xmlDoc, pathExpression));  
   }  
}  
  
// Class that implements ISqlReader  
public class TestSqlReaderBase : ISqlReader {  
XPathNodeIterator m_iterator;           
   public SqlChars FirstName;  
// Metadata for current resultset  
private SqlMetaData[] m_rgSqlMetaData;        
  
   public TestSqlReaderBase (SqlXml xmlDoc, string pathExpression) {     
      // Variables for XPath navigation  
      XPathDocument xDoc;  
      XPathNavigator xNav;  
      XPathExpression xPath;  
  
      // Set sql metadata  
      m_rgSqlMetaData = new SqlMetaData[1];  
      m_rgSqlMetaData[0] = new SqlMetaData ("FirstName",    
SqlDbType.NVarChar,50);     
  
      //Set up the Navigator  
      if (!xmlDoc.IsNull)  
          xDoc = new XPathDocument (xmlDoc.CreateReader());  
      else  
          xDoc = new XPathDocument ();  
      xNav = xDoc.CreateNavigator();  
      xPath = xNav.Compile (pathExpression);  
      m_iterator = xNav.Select(xPath);  
   }  
   public bool Read() {  
      bool moreRows = true;  
      if (moreRows = m_iterator.MoveNext())  
         FirstName = new SqlChars (m_iterator.Current.Value);  
      return moreRows;  
   }  
}  
```  
  
 Em seguida, crie um assembly e uma função definida pelo usuário [!INCLUDE[tsql](../../includes/tsql-md.md)] , SQL_streaming_xml_tvf (não mostrada), que corresponda à função CLR, streaming_xml_tvf. A função definida pelo usuário é usada para definir a função com valor de tabela, CLR_udf_XML2Table, para geração do conjunto de linhas:  
  
```  
create function CLR_udf_XML2Table (@pk int, @xCol xml)  
returns @ret_Table table (FK int, FirstName varchar(max))  
with schemabinding  
as  
begin  
      insert into @ret_Table   
   select @pk, FirstName   
   FROM   SQL_streaming_xml_tvf (@xCol, '/book/author/first-name')  
      return  
end  
```  
  
 Finalmente, defina gatilhos conforme mostrado no exemplo "Crie gatilhos para popular uma tabela de propriedades", mas substitua a função udf_XML2Table pela CLR_udf_XML2Table. O gatilho de inserção é mostrado no exemplo a seguir:  
  
```  
create trigger CLR_trg_docs_INS on T for insert  
as  
   declare @wantedXML xml  
   declare @FK int  
   select @wantedXML = xCol from inserted  
   select @FK = PK from inserted  
  
   insert into tblPropAuthor  
      select *  
   from    dbo.CLR_udf_XML2Table(@FK, @wantedXML)  
```  
  
 O gatilho de inserção é idêntico à versão de não CLR. No entanto o gatilho de atualização apenas substitui a função udf_XML2Table() pela CLR_udf_XML2Table().  
  
## <a name="see-also"></a>Consulte Também  
 [Usar XML em colunas computadas](../../relational-databases/xml/use-xml-in-computed-columns.md)  
  
  
