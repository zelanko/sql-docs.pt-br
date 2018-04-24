---
title: OPENXML (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ColPattern [XML in SQL Server]
- OPENXML statement, about OPENXML statement
- writing XML, OPENXML statement
- OPENXML statement, querying XML
- attribute-centric mapping
- SELECT statement [SQL Server], OPENXML keyword
- column patterns [XML in SQL Server]
- row patterns [XML in SQL Server]
- rowpattern [XML in SQL Server]
- queries [XML in SQL Server], OPENXML statement
- XML [SQL Server], OPENXML statement
- element-centric mapping [SQL Server]
ms.assetid: 060126fc-ed0f-478f-830a-08e418d410dc
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1fc81deadbf518851599699c83f6f5dbf39a39c9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="openxml-sql-server"></a>OPENXML (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  OPENXML, uma palavra-chave do [!INCLUDE[tsql](../../includes/tsql-md.md)] , fornece um conjunto de linhas em documentos XML na memória que é semelhante a uma tabela ou exibição. OPENXML permite acesso a dados XML ainda que ele seja um conjunto de linhas relacional. Ele faz isso fornecendo uma exibição do conjunto de linhas da representação interna de um documento XML. Os registros no conjunto de linhas podem ser armazenados em tabelas do banco de dados.  
  
 OPENXML pode ser usado em instruções SELECT e SELECT INTO sempre que provedores de conjunto de linhas, uma exibição ou OPENROWSET podem ser exibidos como a origem. Para obter informações sobre a sintaxe do OPENXML, veja [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md).  
  
 Para gravar consultas em relação a um documento XML usando OPENXML, você deve primeiro chamar **sp_xml_preparedocument**. Isso analisa o documento XML e retorna um identificador ao documento analisado pronto para consumo. O documento analisado é uma representação da árvore DOM (Document Object Model) de vários nós no documento XML. O identificador do documento é passado para OPENXML. Em seguida, o OPENXML fornece uma exibição do conjunto de linhas do documento, baseado nos parâmetros passados para ele.  
  
> [!NOTE]  
>  O**sp_xml_preparedocument** usa uma versão atualizada pelo SQL do analisador MSXML, Msxmlsql.dll. Essa versão do analisador MSXML foi criada para oferecer suporte ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e permanecer para compatível com o MSXML versão 2.6.  
  
 A representação interna de um documento XML deve ser removida da memória chamando o procedimento armazenado do sistema **sp_xml_removedocument** para liberar a memória.  
  
 A ilustração a seguir mostra o processo.  
  
 ![Analisando XML com OPENXML](../../relational-databases/xml/media/xmlsp.gif "Analisando XML com OPENXML")  
  
 Observe que para entender o OPENXML, é necessário estar familiarizado com consultas XPath e ter um entendimento de XML. Para obter mais informações sobre suporte ao XPath no SQL Server, consulte [Usando consultas XPath no SQLXML 4.0](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md).  
  
> [!NOTE]  
>  O OpenXML permite que os padrões de linha e coluna do XPath sejam parametrizados como variáveis. Essa parametrização pode resultar em injeções de expressões XPath, se o programador expuser a parametrização a usuários externos (por exemplo, se os parâmetros forem fornecidos por meio de um procedimento armazenado chamado externamente). Para evitar esses problemas potenciais de segurança, é recomendável que os parâmetros de XPath nunca sejam expostos a chamadores externos.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra o uso do `OPENXML` em uma instrução `INSERT` e em uma instrução `SELECT` . O documento XML de exemplo contém elementos `<Customers>` e `<Orders>` .  
  
 Primeiro, o procedimento armazenado `sp_xml_preparedocument` analisa o documento XML. O documento analisado é uma representação em árvore dos nós (elementos, atributos, texto e comentários) no documento XML. `OPENXML` se refere, em seguida, a esse documento XML analisado e fornece uma exibição de conjunto de linhas de todo ou partes desse documento XML. Uma instrução `INSERT` que usa `OPENXML` pode inserir dados desse tipo de conjunto de linhas em uma tabela de banco de dados. Várias chamadas do `OPENXML` podem ser usadas para fornecer uma exibição do conjunto de linhas de várias partes do documento XML e processá-las, por exemplo, inserindo-as em diferentes tabelas. Esse processo também é referido como XML de fragmentação em tabelas.  
  
 No exemplo a seguir, um documento XML é fragmentado de uma maneira que os elementos `<Customers>` são armazenados na tabela `Customers` e elementos `<Orders>` são armazenados na tabela `Orders` usando duas instruções `INSERT` . O exemplo também mostra uma instrução `SELECT` com `OPENXML` que recupera `CustomerID` e `OrderDate` do documento XML. A última etapa do processo é chamar `sp_xml_removedocument`. Isso é feito para liberar a memória alocada para conter a representação em árvore XML que foi criada durante a fase de análise.  
  
```  
-- Create tables for later population using OPENXML.  
CREATE TABLE Customers (CustomerID varchar(20) primary key,  
                ContactName varchar(20),   
                CompanyName varchar(20));  
GO  
CREATE TABLE Orders( CustomerID varchar(20), OrderDate datetime;)  
GO  
DECLARE @docHandle int;  
DECLARE @xmlDocument nvarchar(max); -- or xml type  
SET @xmlDocument = N'<ROOT>  
<Customers CustomerID="XYZAA" ContactName="Joe" CompanyName="Company1">  
<Orders CustomerID="XYZAA" OrderDate="2000-08-25T00:00:00"/>  
<Orders CustomerID="XYZAA" OrderDate="2000-10-03T00:00:00"/>  
</Customers>  
<Customers CustomerID="XYZBB" ContactName="Steve"  
CompanyName="Company2">No Orders yet!  
</Customers>  
</ROOT>';  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument;  
-- Use OPENXML to provide rowset consisting of customer data.  
INSERT Customers   
SELECT *   
FROM OPENXML(@docHandle, N'/ROOT/Customers')   
  WITH Customers;  
-- Use OPENXML to provide rowset consisting of order data.  
INSERT Orders   
SELECT *   
FROM OPENXML(@docHandle, N'//Orders')   
  WITH Orders;  
-- Using OPENXML in a SELECT statement.  
SELECT * FROM OPENXML(@docHandle, N'/ROOT/Customers/Orders') WITH (CustomerID nchar(5) '../@CustomerID', OrderDate datetime);  
-- Remove the internal representation of the XML document.  
EXEC sp_xml_removedocument @docHandle;   
```  
  
 A ilustração a seguir mostra a árvore XML analisada do documento XML anterior que foi criado usando sp_xml_preparedocument.  
  
 ![Árvore XML analisada](../../relational-databases/xml/media/xmlparsedtree.gif "Árvore XML analisada")  
  
## <a name="openxml-parameters"></a>Parâmetros de OPENXML  
 Os parâmetros para OPENXML incluem:  
  
-   Um identificador de documento XML (*idoc*)  
  
-   Uma expressão XPath para identificar os nós a serem mapeados para linhas (*rowpattern*)  
  
-   Uma descrição do conjunto de linhas a ser gerado  
  
-   Mapeamento entre as colunas do conjunto de linhas e os nós XML  
  
### <a name="xml-document-handle-idoc"></a>Identificador do documento XML (idoc)  
 O identificador do documento é retornado pelo procedimento armazenado **sp_xml_preparedocument** .  
  
### <a name="xpath-expression-to-identify-the-nodes-to-be-processed-rowpattern"></a>Expressão XPath para identificar os nós a serem processados (rowpattern)  
 A expressão XPath especificada como *rowpattern* identifica um conjunto de nós no documento XML. Cada nó identificado por *rowpattern* corresponde a uma única linha no conjunto de linhas gerado por OPENXML.  
  
 Os nós identificados pela expressão XPath podem ser qualquer nó XML no documento XML. Se *rowpattern* identificar um conjunto de elementos no documento XML, haverá uma linha no conjunto de linhas para cada nó de elemento identificado. Por exemplo, se *rowpattern* terminar em um atributo, será criada uma linha para cada nó de atributo selecionado por *rowpattern*.  
  
### <a name="description-of-the-rowset-to-be-generated"></a>Descrição do conjunto de linhas a ser gerado  
 Um esquema de conjunto de linhas usado por OPENXML para gerar o conjunto de linhas resultante. É possível usar as seguintes opções ao especificar um esquema de conjunto de linhas.  
  
#### <a name="using-the-edge-table-format"></a>Usando o formato de tabela de borda  
 Você deve usar o formato de tabela de borda para especificar um esquema de conjunto de linhas. Não use a cláusula WITH.  
  
 Quando isso é feito, o OPENXML retorna um conjunto de linhas no formato de tabela de borda. Isso é referido como uma tabela de borda, porque cada borda na árvore do documento XML analisado é mapeada para uma linha no conjunto de linhas.  
  
 Tabelas de borda representam a estrutura do documento XML refinado dentro de uma única tabela. Essa estrutura inclui o nomes dos atributos e elementos, a hierarquia do documento, os namespaces e as instruções de processamento. O formato de tabela de borda permite obter informações adicionais que não são expostas pelas metapropriedades. Para mais informações sobre as metapropriedades, consulte [Specify Metaproperties in OPENXML](../../relational-databases/xml/specify-metaproperties-in-openxml.md).  
  
 As informações adicionais fornecidas por uma tabela de borda permitem armazenar e consultar o tipo de dados de um elemento e de um atributo e o tipo de nó, e também armazenar e consultar informações sobre a estrutura do documento XML. Com essas informações adicionais, também pode ser possível construir seu próprio sistema de gerenciamento de documentos XML.  
  
 Usando uma tabela de borda, é possível gravar procedimentos armazenados que usam documentos XML como entrada BLOB (bloco de objetos binários grandes), produzir a tabela de borda e, em seguida, extrair e analisar o documento em um nível mais detalhado. Esse nível detalhado pode incluir a localização da hierarquia do documento, os nomes dos atributos e elementos, os namespaces e as instruções de processamento.  
  
 A tabela de borda também pode funcionar como um formato de armazenamento para documentos XML quando o mapeamento para outros formatos relacionais não for lógico e um campo ntext não estiver fornecendo informações estruturais suficientes.  
  
 Em situações em que é possível usar um analisador XML para examinar um documento XML, é possível usar uma tabela de borda em vez de obter as mesmas informações.  
  
 A tabela a seguir descreve a estrutura da tabela de borda.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id**|**bigint**|É a ID exclusiva do nó do documento.<br /><br /> O elemento raiz tem um valor de ID igual a 0. Os valores negativos da ID são reservados.|  
|**parentid**|**bigint**|Identifica o pai do nó. O pai identificado por esse ID necessariamente não é o elemento pai. No entanto isso depende do Tipo do Nó cujo o pai é identificado por esse ID. Por exemplo, se o nó for um nó de texto, seu pai poderá ser um nó de atributo.<br /><br /> Se o nó estiver no nível superior no documento XML, seu **ParentID** será NULL.|  
|**tipo de nó**|**int**|Identifica o tipo de nó e é um inteiro que corresponde à numeração do tipo de nó DOM (Document Object Model) do XML.<br /><br /> Os seguintes são os valores que podem aparecer nessa coluna para indicar o tipo do nó:<br /><br /> **1** = Nó de elemento<br /><br /> **2** = Nó de atributo<br /><br /> **3** = Nó de texto<br /><br /> **4** = Nó de seção CDATA<br /><br /> **5** = Nó de referência de entidade<br /><br /> **6** = Nó de entidade<br /><br /> **7** = Nó de instrução de processamento<br /><br /> **8** = Nó de comentário<br /><br /> **9** = Nó de documento<br /><br /> **10** = Nó de tipo de documento<br /><br /> **11** = Nó de fragmento de documento<br /><br /> **12** = Nó de notação<br /><br /> Para obter mais informações, consulte o tópico "Propriedade nodeType" no SDK do MSXML (Microsoft XML.|  
|**localname**|**nvarchar(max)**|Fornece o nome local do elemento ou do atributo. Será NULL se o objeto DOM não tiver um nome.|  
|**prefixo**|**nvarchar(max)**|É o prefixo do namespace do nome do nó.|  
|**namespaceuri**|**nvarchar(max)**|É o URI do namespace do nó. Se o valor for NULL, nenhum namespace estará presente.|  
|**datatype**|**nvarchar(max)**|É o tipo de dados real da linha de atributo ou de elemento e é normalmente NULL. O tipo de dados é deduzido do DTD embutido ou do esquema embutido.|  
|**prev**|**bigint**|É a ID de XML do elemento irmão anterior. Será NULL se não houver nenhum irmão anterior direto.|  
|**text**|**ntext**|Contém o valor do atributo ou o conteúdo do elemento em formulário de texto. Ou será NULL, se a entrada da tabela de borda não precisar de um valor.|  
  
#### <a name="using-the-with-clause-to-specify-an-existing-table"></a>Usando a cláusula WITH para especificar uma tabela existente  
 Você pode usar a cláusula WITH para especificar o nome de uma tabela existente. Para isso, basta especificar o nome de uma tabela existente cujo esquema possa ser usado por OPENXML para gerar o conjunto de linhas.  
  
#### <a name="using-the-with-clause-to-specify-a-schema"></a>Usando a cláusula WITH para especificar um esquema  
 É possível usar a cláusula WITH para especificar um esquema completo. Para especificar o esquema do conjunto de linhas, você especifica os nomes das colunas, seus tipos de dados e seus mapeamentos para o documento XML.  
  
 Você pode especificar o padrão da coluna usando o parâmetro ColPattern na SchemaDeclaration. O padrão da coluna especificado é usado para mapear uma coluna do conjunto de linhas para o nó XML que é identificado pelo padrão da linha e também é usado para determinar o tipo de mapeamento.  
  
 Se ColPattern não for especificado para uma coluna, a coluna do conjunto de linhas será mapeada para o nó XML com o mesmo nome, com base no mapeamento especificado pelo parâmetro *flags* . No entanto se ColPattern for especificado como parte da especificação do esquema na cláusula WITH, ele sobrescreverá o mapeamento especificado no parâmetro *flags* .  
  
### <a name="mapping-between-the-rowset-columns-and-the-xml-nodes"></a>Mapeamento entre as colunas do conjunto de linhas e os nós XML  
 Na instrução OPENXML, você pode opcionalmente especificar o tipo de mapeamento, como centrado em atributo ou centrado em elemento, entre as colunas do conjunto de linhas e os nós XML identificados pelo *rowpattern*. Essas informações são usadas na transformação entre os nós XML nós e as colunas do conjunto de linhas.  
  
 É possível especificar o mapeamento de qualquer um dos modos e também especificar os dois:  
  
-   Usando o parâmetro *flags*   
  
     O mapeamento especificado pelo parâmetro *flags* pressupõe correspondência de nomes na qual os nós XML são mapeados para as colunas do conjunto de linhas correspondentes com o mesmo nome.  
  
-   Usando o parâmetro *ColPattern*   
  
     *ColPattern*, uma expressão XPath , é especificada como parte de *SchemaDeclaration* na cláusula WITH. O mapeamento especificado em *ColPattern* substitui o mapeamento especificado pelo parâmetro *flags* .  
  
     *ColPattern* pode ser usado para especificar o tipo de mapeamento, como centrado em atributo ou centrado em elemento, que sobrescreve ou aprimora o mapeamento indicado por *flags*.  
  
     *ColPattern* é especificado nas seguintes circunstâncias:  
  
    -   O nome da coluna no conjunto de linhas é diferente do nome do atributo ou elemento para o qual ele é mapeado. Nesse caso, *ColPattern* é usado para identificar o elemento XML e o nome do atributo para o qual a coluna do conjunto de linhas é mapeado.  
  
    -   Você quer mapear um atributo de metapropriedade para a coluna. Nesse caso, *ColPattern* é usado para identificar a metapropriedade para a qual a coluna do conjunto de linhas é mapeada. Para mais informações sobre como usar as metapropriedades, consulte [Especificar metapropriedades em OPENXML](../../relational-databases/xml/specify-metaproperties-in-openxml.md).  
  
 Os parâmetros *flags* e *ColPattern* são opcionais. Se nenhum mapeamento for especificado, será pressuposto o mapeamento centrado em atributo. O mapeamento centrado em atributo é o valor padrão do parâmetro *flags* .  
  
#### <a name="attribute-centric-mapping"></a>mapeamento centrado em atributo  
 A definição do parâmetro *flags* no OPENXML como 1 (XML_ATTRIBUTES) especifica mapeamento **centrado em atributo** . Se *flags* contiver XML_ ATTRIBUTES, o conjunto de linhas exposto fornecerá ou consumirá linhas nas quais cada elemento XML é representado como uma linha. Os atributos XML são mapeados para os atributos definidos na SchemaDeclaration ou que são fornecidos pelo Tablename da cláusula WITH com base na correspondência de nomes. A correspondência de nomes significa que os atributos XML de um nome específico são armazenados em uma coluna no conjunto de linhas com o mesmo nome.  
  
 Se o nome da coluna for diferente do nome de atributo para o qual ele é mapeado, *ColPattern* deverá ser especificado.  
  
 Se o atributo XML tiver um qualificador de namespace, o nome da coluna no conjunto de linhas também precisará ter o qualificador.  
  
#### <a name="element-centric-mapping"></a>Mapeamento centrado em elemento  
 A definição do parâmetro *flags* no OPENXML como 2 (XML_ELEMENTS) especifica mapeamento **centrado em elemento** . É semelhante ao mapeamento **centrado em atributo** , com exceção das seguintes diferenças:  
  
-   A correspondência de nomes do exemplo de mapeamento, uma mapeamento de coluna para um elemento XML com o mesmo nome seleciona os subelementos não complexos, a menos que o padrão em nível de coluna seja especificado. No processo de recuperação, se o subelemento for complexo porque contém subelementos adicionais, a coluna será definida como NULL. Valores de atributos dos subelementos são ignorados então.  
  
-   Para vários subelementos com o mesmo nome, o primeiro nó é retornado.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_xml_preparedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)   
 [sp_xml_removedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)   
 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)   
 [Dados XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
