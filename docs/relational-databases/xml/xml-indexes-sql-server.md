---
title: "Índices XML (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing indexes
- deleting indexes
- secondary indexes [XML in SQL Server]
- xml data type [SQL Server], indexes
- dropping indexes
- PATH index
- DROP_EXISTING clause
- XML [SQL Server], indexes
- primary indexes [XML in SQL Server]
- indexes [SQL Server], XML
- XML indexes [SQL Server], secondary
- BLOBs, XML indexes
- disabling indexes
- XML indexes [SQL Server], modifying
- XML indexes [SQL Server]
- XML indexes [SQL Server], primary
- modifying indexes
- XML indexes [SQL Server], dropping
- VALUE index
- XML indexes [SQL Server], xml data type
- PROPERTY index
- XML indexes [SQL Server], creating
ms.assetid: f5c9209d-b3f3-4543-b30b-01365a5e7333
caps.latest.revision: "59"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 89cddd8c4eabe6b8c1888df909da934350dfae09
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="xml-indexes-sql-server"></a>Índices XML (SQL Server)
  Índices XML podem ser criados em colunas de tipo de dados **xml** . Eles indexam todas as marcas, valores e caminhos através das instâncias XML na coluna e se beneficiam do desempenho das consultas. Seu aplicativo pode se beneficiar de um índice XML nas seguintes situações:  
  
-   Consultas em colunas XML são comuns em sua carga de trabalho. O custo da manutenção de índices XML durante a modificação de dados deve ser considerado.  
  
-   Seus valores XML são relativamente grandes e as partes recuperadas são relativamente pequenas. A construção de índices evita a análise de todos os dados em tempo de execução e beneficia pesquisas de índice para processamento eficiente de consultas.  
  
 Índices XML se encaixam nas seguintes categorias:  
  
-   Índice XML primário  
  
-   Índice XML secundário  
  
 O primeiro índice na coluna de tipo **xml** deve ser o índice XML primário. Usando o índice de XML primário, os seguintes tipos de índices secundários têm suporte: PATH, VALUE e PROPERTY. Dependendo do tipo de consulta, esses índices secundários podem ajudar a melhorar o desempenho de consultas.  
  
> [!NOTE]  
>  Não é possível criar ou modificar um índice XML a menos que as opções do banco de dados estejam definidas corretamente para trabalhar com o tipo de dados **xml** . Para obter mais informações, veja [Usar a pesquisa de texto completo com colunas XML](../../relational-databases/xml/use-full-text-search-with-xml-columns.md).  
  
 Instâncias XML são armazenadas em colunas de tipo **xml** como BLOBs (objetos binários grandes). Essas instâncias XML podem ser grandes e a representação binária armazenada de instâncias de tipo de dados **xml** pode ser de até 2 GB. Sem um índice, esses objetos binários grandes são fragmentados em tempo de execução para avaliar uma consulta. Essa fragmentação pode ser demorada. Por exemplo, considere a consulta abaixo:  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.query('  
  /PD:ProductDescription/PD:Summary  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist ('/PD:ProductDescription/@ProductModelID[.="19"]') = 1  
```  
  
 Para selecionar as instâncias XML que atendem à condição na cláusula `WHERE` , o BLOB (objeto binário grande) XML em cada linha da tabela `Production.ProductModel` é fragmentado em tempo de execução. Em seguida, a expressão `(/PD:ProductDescription/@ProductModelID[.="19"]`) no método `exist()` é avaliada. Essa fragmentação em tempo de execução pode ser dispendiosa dependendo do tamanho e do número de instâncias armazenadas na coluna.  
  
 Se a consulta de BLOBs XML for comum no ambiente do seu aplicativo, a indexação de colunas de tipo **xml** ajudará. No entanto há um custo associado à manutenção do índice durante a modificação de dados.  
  
## <a name="primary-xml-index"></a>Índice XML primário  
 O índice XML primário indexa todos os valores, marcas e caminhos dentro das instâncias XML em uma coluna XML. Para criar um índice XML, a tabela que contém a coluna XML deve ter um índice clusterizado na chave primária da tabela. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa essa chave primária para correlacionar linhas no índice XML primário com linhas na tabela que contém a coluna XML.  
  
 Um índice XML primário é uma representação fragmentada e persistente dos BLOBs XML na coluna de tipo de dados **xml** . Para cada BLOB (objeto binário grande) XML na coluna, o índice cria várias linhas de dados. O número de linhas no índice é aproximadamente igual ao número de nós no objeto binário grande XML. Quando uma consulta recupera a instância XML completa, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece a instância da coluna XML. As consultas dentro de instâncias XML usam o índice XML primário e podem retornar valores escalares ou subárvores XML usando o próprio índice.  
  
 Cada linha armazena as seguintes informações de nó:  
  
-   Nome da marca, como um nome de atributo ou elemento.  
  
-   Valor do nó.  
  
-   Tipo de nó, como um nó de elemento, nó de atributo ou nó de texto.  
  
-   Informações de ordem do documento representada por um identificador de nó interno.  
  
-   Caminho de cada nó para a raiz da árvore XML. Essa coluna é pesquisada para expressões de caminho na consulta.  
  
-   Chave primária da tabela base. A chave primária da tabela base é duplicada no índice XML primário para uma junção retroativa com a tabela base, e o número máximo de colunas na chave primária da tabela base é limitado a 15.  
  
 Essas informações de nó são usadas para avaliar e construir resultados XML para uma consulta especificada. Para fins de otimização, as informações de nome da marca e de tipo de nó são codificadas como valores inteiros e a coluna Path usa a mesma codificação. Além disso, caminhos são armazenados em ordem inversa para permitir correspondência de caminhos quando apenas o sufixo do caminho é conhecido. Por exemplo:  
  
-   `//ContactRecord/PhoneNumber` em que apenas as duas últimas etapas são conhecidas  
  
 OU  
  
-   `/Book/*/Title` em que o caractere curinga (`*`) é especificado no meio da expressão.  
  
 O processador de consultas usa índice XML primário para consultas que envolvem [Métodos de tipo de dados xml](../../t-sql/xml/xml-data-type-methods.md) e retorna valores escalares ou as subárvores XML do próprio índice primário. (Esse índice armazena todas as informações necessárias para reconstruir a instância XML.)  
  
 Por exemplo, a consulta a seguir retorna informações resumidas armazenadas na coluna de tipo `CatalogDescription`**xml** na tabela `ProductModel`. A consulta retorna informações de <`Summary`> apenas para modelos de produto cuja descrição de catálogo também armazena a descrição de <`Features`>.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")SELECT CatalogDescription.query('  /PD:ProductDescription/PD:Summary') as ResultFROM Production.ProductModelWHERE CatalogDescription.exist ('/PD:ProductDescription/PD:Features') = 1  
```  
  
 Com relação ao índice XML primário, em vez de fragmentar cada instância de objeto binário grande XML na tabela base, as linhas no índice que correspondem a cada objeto binário grande XML são pesquisadas sequencialmente para a expressão especificada no método `exist()`. Se o caminho for encontrado na coluna Path no índice, o elemento <`Summary`> juntamente com suas subárvores será recuperado do índice XML primário e convertido em um objeto binário grande XML como o resultado do método `query()`.  
  
 Observe que o índice XML primário não é usado ao recuperar uma instância XML completa. Por exemplo, a consulta a seguir recupera da tabela toda a instância XML que descreve as instruções de fabricação para um modelo de produto específico.  
  
```  
USE AdventureWorks2012;SELECT InstructionsFROM Production.ProductModel WHERE ProductModelID=7;  
```  
  
## <a name="secondary-xml-indexes"></a>Índices XML secundários  
 Para melhorar o desempenho da pesquisa, você pode criar índices XML secundários. Um índice XML primário deve existir para que seja possível criar índices secundários. Estes são os tipos:  
  
-   Índice XML secundário PATH  
  
-   Índice XML secundário VALUE  
  
-   Índice XML secundário PROPERTY  
  
 A seguir estão algumas diretrizes para criação de um ou mais índices secundários:  
  
-   Se sua carga de trabalho usar expressões de caminho significativamente em colunas XML, o índice XML secundário PATH provavelmente acelerará sua carga de trabalho. O caso mais comum é o uso do método **exist()** em colunas XML na cláusula WHERE do Transact-SQL.  
  
-   Se sua carga de trabalho recuperar vários valores de instâncias XML individuais usando expressões de caminho, caminhos de clustering dentro de cada instância XML no índice PROPERTY poderão ser úteis. Isso normalmente ocorre em um cenário de recipiente de propriedades quando as propriedades de um objeto são buscadas e seu valor de chave primária é conhecido.  
  
-   Se sua carga de trabalho envolver consulta de valores dentro de instâncias XML sem conhecer os nomes de elementos ou de atributos que contêm esses valores, você poderá desejar criar o índice VALUE. Normalmente isso ocorre com pesquisas de eixos descendentes, como //author[last-name="Howard"], em que elementos \<author> podem ocorrer em qualquer nível da hierarquia. Isso também ocorre em consultas com caracteres curinga, como /book [@* = "novel"], em que a consulta procura por elementos \<book> que têm algum atributo com o valor “novel”.  
  
### <a name="path-secondary-xml-index"></a>Índice XML secundário PATH  
 Se suas consultas normalmente especificarem expressões de caminho em colunas de tipo **xml** , um índice secundário PATH poderá acelerar a pesquisa. Conforme descrito anteriormente neste tópico, o índice primário é útil quando você tem consultas que especificam o método **exist()** na cláusula WHERE. Se você adicionar um índice secundário PATH, poderá também melhorar o desempenho da pesquisa nessas consultas.  
  
 Embora um índice XML primário evite precisar fragmentar objetos binários grandes XML em tempo de execução, ele pode fornecer o melhor desempenho para consultas baseadas em expressões de caminho. Como todas as linhas no índice XML primário correspondentes a um objeto binário grande são pesquisadas sequencialmente para grandes instâncias XML, a pesquisa sequencial pode ser lenta. Nesse caso, ter um índice secundário construído nos valores de caminho e valores de nós no índice primário pode acelerar significativamente a pesquisa do índice. No índice secundário PATH, o valores de caminhos e de nós são colunas de chave que permitem buscas mais eficientes ao pesquisar caminhos. O otimizador de consulta pode usar o índice PATH para expressões como as mostradas no seguinte:  
  
-   `/root/Location` que especifica apenas um caminho  
  
 OU  
  
-   `/root/Location/@LocationID[.="10"]` em que o caminho e o valor do nó são especificados.  
  
 A consulta seguinte mostra onde o índice PATH é útil:  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.query('  
  /PD:ProductDescription/PD:Summary  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist ('/PD:ProductDescription/@ProductModelID[.="19"]') = 1  
```  
  
 Na consulta, a expressão de caminho `/PD:ProductDescription/@ProductModelID` e o valor `"19"` no método `exist()` correspondem aos campos de chave do índice PATH. Isso permite busca direta no índice PATH e fornece desempenho melhor de pesquisa do que a pesquisa sequencial de valores de caminho no índice primário.  
  
### <a name="value-secondary-xml-index"></a>Índice XML secundário VALUE  
 Se as consultas forem baseadas em valor, por exemplo, `/Root/ProductDescription/@*[. = "Mountain Bike"]` ou `//ProductDescription[@Name = "Mountain Bike"]`e o caminho não for especificado completamente ou se incluir um caractere curinga, você poderá obter resultados mais rápidos construindo um índice XML secundário construído sobre valores de nós no índice XML primário.  
  
 As colunas de chave do índice VALUE são (valor de nó e caminho) do índice XML primário. Se sua carga de trabalho envolver consulta de valores de instâncias XML sem conhecer os nomes de elementos ou de atributos que contêm os valores, um índice VALUE poderá ser útil. Por exemplo, a expressão a seguir se beneficiará da existência de um índice VALUE:  
  
-   `//author[LastName="someName"]` onde você sabe o valor do elemento <`LastName`>, mas o pai de <`author`> pode ocorrer em qualquer lugar.  
  
-   `/book[@* = "someValue"]` onde a consulta procura o elemento <`book`> que tem algum atributo contendo o valor `"someValue"`.  
  
 A consulta a seguir retorna `ContactID` da tabela `Contact` . A cláusula `WHERE` especifica um filtro que procura valores no tipo de coluna `AdditionalContactInfo`**xml** . As IDs de contato serão retornadas apenas se o objeto binário grande XML das informações de contato adicionais correspondentes incluírem um número de telefone específico. Como o elemento <`telephoneNumber`> pode aparecer em qualquer lugar no XML, a expressão de caminho especifica o eixo descendente ou independente.  
  
```  
WITH XMLNAMESPACES (  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS CI,  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.exist('//ACT:telephoneNumber/ACT:number[.="111-111-1111"]') = 1  
```  
  
 Nessa situação, o valor da pesquisa de <`number`> é conhecido, mas ele pode aparecer em qualquer lugar na instância XML como um filho do elemento <`telephoneNumber`>. Esse tipo de consulta pode se beneficiar de um índice de pesquisa baseado em um valor específico.  
  
### <a name="property-secondary-index"></a>Índice XML secundário PROPERTY  
 Consultas que recuperam um ou mais valores de instâncias XML individuais podem se beneficiar de um índice PROPERTY. Esse cenário ocorre ao recuperar propriedades de objetos usando o método **value()** do tipo **xml** e quando o valor da chave primária do objeto é conhecido.  
  
 O índice PROPERTY é construído nas colunas (PK, Caminho e valor do nó) do índice XML primário, em que PK é a chave primária da tabela base.  
  
 Por exemplo, para obter o modelo do produto `19`, a consulta a seguir recupera o `ProductModelID` e os valores do atributo `ProductModelName` usando o método `value()` . Em vez de usar o índice XML primário ou os outros índices XML secundários, o índice PROPERTY pode fornecer execução mais rápida.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.value('(/PD:ProductDescription/@ProductModelID)[1]', 'int') as ModelID,  
       CatalogDescription.value('(/PD:ProductDescription/@ProductModelName)[1]', 'varchar(30)') as ModelName          
FROM Production.ProductModel     
WHERE ProductModelID = 19  
```  
  
 Exceto pelas diferenças descritas posteriormente neste tópico, a criação de um índice XML em uma coluna de tipo**xml** é semelhante à criação de um índice em uma coluna de tipo não**xml** . As instruções DDL do [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir podem ser usadas para criar e gerenciar índices XML:  
  
-   [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
-   [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
-   [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
## <a name="getting-information-about-xml-indexes"></a>Obtendo informações sobre índices XML  
 As entradas de índice XML são exibidas na exibição do catálogo, sys.indexes, com o índice "tipo" 3. A coluna de nome contém o nome do índice XML.  
  
 Também são registrados índices de XML na exibição do catálogo, sys.xml_indexes. Essa exibição contém todas as colunas de sys.indexes e algumas específicas que são úteis para índices XML. O valor NULL na coluna secondary_type indica um índice XML primário, os valores 'P', 'R' e 'V' representam os índices XML secundários PATH, PROPERTY e VALUE, respectivamente.  
  
 O uso espacial de índices XML pode ser localizado na função com valor de tabela [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md). Ela fornece informações, como o número de páginas ocupadas no disco, tamanho médio das linhas em bytes e o número de registros para todos os tipos de índices. Isso também inclui índices XML. Essas informações estão disponíveis para cada partição do banco de dados. Índices XML usam o mesmo esquema e função de particionamento da tabela base.  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [Dados XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
