---
title: Usar conjuntos de colunas | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2015
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- sparse columns, column sets
- column sets
ms.assetid: a4f9de95-dc8f-4ad8-b957-137e32bfa500
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f8cd068e23315edcef7df3a677a52530a767c685
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47714454"
---
# <a name="use-column-sets"></a>Usar conjuntos de colunas
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  As tabelas que usam colunas esparsas podem designar um conjunto de colunas para retornar todas as colunas esparsas na tabela. Um conjunto de colunas é uma representação em XML sem-tipo que combina todas as colunas esparsas de uma tabela em uma saída estruturada. Um conjunto de colunas é como uma coluna calculada em que o conjunto de colunas não é fisicamente armazenado na tabela. Um conjunto de colunas difere de uma coluna calculada em que o conjunto de colunas é diretamente atualizável.  
  
 Considere o uso de conjuntos de colunas quando o número de colunas em uma tabela for grande e trabalhar nelas individualmente for difícil. Os aplicativos devem observar alguma melhoria no desempenho quando selecionam e inserem dados usando conjuntos de colunas em tabelas com muitas colunas. Entretanto, o desempenho de conjuntos de colunas pode ser reduzido quando muitos índices são definidos nas colunas das tabelas. Isso porque a quantidade de memória necessária para um plano de execução aumenta.  
  
 Para definir um conjunto de colunas, use as palavras-chave *<column_set_name>* FOR ALL_SPARSE_COLUMNS nas instruções [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) ou [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="guidelines-for-using-column-sets"></a>Diretrizes para usar conjuntos de colunas  
 Ao usar conjuntos de colunas, considere as seguintes diretrizes:  
  
-   Colunas esparsas e um conjunto de colunas podem ser adicionados como parte da mesma instrução.  
  
-   Um conjunto de colunas não poderá ser adicionado a uma tabela se ela já contiver colunas esparsas.  
  
-   O conjunto de colunas não pode ser alterado. Para alterar um conjunto de colunas, as colunas esparsas e o próprio conjunto de colunas devem ser excluídos e recriados.  
  
-   Um conjunto de colunas pode ser adicionado a uma tabela que não inclui colunas esparsas. Se, posteriormente, forem adicionadas colunas esparsas à tabela, elas serão exibidas no conjunto de colunas.  
  
-   Somente um conjunto de colunas é permitido por tabela.  
  
-   Um conjunto de colunas é opcional e não é exigido para usar colunas esparsas.  
  
-   Restrições ou valores padrão não podem ser definidos em um conjunto de colunas.  
  
-   Colunas computadas não podem conter colunas de conjunto de colunas.  
  
-   Consultas distribuídas não têm suporte em tabelas que contêm conjuntos de colunas.  
  
-   Replicação não oferece suporte a conjuntos de colunas.  
  
-   Change data capture não oferece suporte a conjuntos de colunas.  
  
-   Um conjunto de colunas não pode fazer parte de nenhum tipo de índice. Incluindo índices XML, índices de texto completo e exibições indexadas. Um conjunto de colunas não pode ser adicionado como uma coluna incluída em qualquer índice.  
  
-   Um conjunto de colunas não pode ser usado na expressão de filtro de um índice filtrado ou estatísticas filtradas.  
  
-   Quando uma exibição inclui um conjunto de colunas, ele é exibido na exibição como uma coluna XML.  
  
-   Um conjunto de colunas não pode ser incluído em uma definição de exibição indexada.  
  
-   Exibições particionadas que incluem tabelas com conjuntos de colunas são atualizáveis quando a exibição particionada especifica as colunas esparsas por nome. Uma exibição particionada não é atualizável quando referencia o conjunto de colunas.  
  
-   Notificações de consulta referentes a conjuntos de colunas não são permitidas.  
  
-   Dados XML têm um limite de tamanho de 2 GB. Se os dados combinados de todas as colunas esparsas não nulas em uma linha excederem esse limite, a operação de consulta ou DML produzirá um erro.  
  
-   Para obter informações sobre os dados retornados pela função COLUMNS_UPDATED, veja [Usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="guidelines-for-selecting-data-from-a-column-set"></a>Diretrizes para selecionar dados de um conjunto de colunas  
 Considere as seguintes diretrizes para selecionar dados de um conjunto de colunas:  
  
-   Conceitualmente, um conjunto de colunas é um tipo coluna XML computada, atualizável, que agrega um conjunto de colunas relacionais subjacentes em uma representação XML única. O conjunto de colunas só oferece suporte à propriedade ALL_SPARSE_COLUMNS. Essa propriedade é usada para agregar todos os valores não nulos de todas as colunas esparsas para uma linha específica.  
  
-   No editor de tabela do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] os conjuntos de colunas são exibidos como um campo XML editável. Defina os conjuntos de colunas no formato:  
  
    ```  
    <column_name_1>value1</column_name_1><column_name_2>value2</column_name_2>...  
    ```  
  
     Exemplos de conjuntos de colunas:  
  
    -   `<sparseProp1>10</sparseProp1><sparseProp3>20</sparseProp3>`  
  
    -   `<DocTitle>Bicycle Parts List</DocTitle><Region>West</Region>`  
  
-   Colunas esparsas que contêm valores nulos são omitidas da representação XML do conjunto de colunas.  
  
> [!WARNING]  
>  A adição de um conjunto de colunas altera o comportamento de consultas SELECT *. A consulta retornará o conjunto de colunas como uma coluna XML e não retornará as colunas esparsas individuais. Designers de esquema e desenvolvedores de software devem ter cuidado para não violar aplicativos existentes.  
  
## <a name="inserting-or-modifying-data-in-a-column-set"></a>Inserindo ou modificando dados em um conjunto de colunas  
 A manipulação de dados de uma coluna esparsa pode ser executada usando o nome de colunas individuais ou referenciando o nome do conjunto de colunas e especificando seus valores usando o formato XML do conjunto de colunas. As colunas esparsas podem ser exibidas em qualquer ordem na coluna XML.  
  
 Quando os valores de colunas esparsas são inseridos ou atualizados usando o conjunto de colunas XML, os valores inseridos nas colunas esparsas subjacentes são implicitamente convertidos do tipo de dados **xml** . No caso de colunas numéricas, um valor em branco no XML para a coluna numérica é convertido em uma cadeia de caracteres vazia. Isso faz com que um zero seja inserido na coluna numérica, como mostrado no exemplo a seguir.  
  
```  
CREATE TABLE t (i int SPARSE, cs xml column_set FOR ALL_SPARSE_COLUMNS);  
GO  
INSERT t(cs) VALUES ('<i/>');  
GO  
SELECT i FROM t;  
GO  
```  
  
 Nesse exemplo, nenhum valor foi especificado para a coluna `i`, mas o valor `0` foi inserido.  
  
## <a name="using-the-sqlvariant-data-type"></a>Usando o tipo de dados sql_variant  
 O tipo de dados **sql_variant** pode armazenar vários tipos de dados diferentes, como **int**, **char**e **data**. Os conjuntos de colunas geram informações de tipo de dados como escala, precisão e informações de localidade que são associadas a um valor **sql_variant** como atributo na coluna XML gerada. Se você tentar fornecer esses atributos em uma instrução XML personalizada como uma entrada para uma operação de inserção ou atualização em um conjunto de colunas, alguns desses atributos serão exigidos e a outros será atribuído um valor padrão. A tabela a seguir lista os tipos de dados e os valores padrão que o servidor gera quando o valor não é fornecido.  
  
|Tipo de dados|localeID*|sqlCompareOptions|sqlCollationVersion|SqlSortId|Comprimento máximo|Precisão|Escala|  
|---------------|----------------|-----------------------|-------------------------|---------------|--------------------|---------------|-----------|  
|**char**, **varchar**, **binary**|-1|'Padrão'|0|0|8000|Não aplicável**|Não aplicável|  
|**nvarchar**|-1|'Padrão'|0|0|4000|Não aplicável|Não aplicável|  
|**decimal**, **float**, **real**|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|18|0|  
|**integer**, **bigint**, **tinyint**, **smallint**|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|  
|**datetime2**|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|7|  
|**datetime offset**|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|7|  
|**datetime**, **date**, **smalldatetime**|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|  
|**money**, **smallmoney**|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|  
|**time**|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|Não aplicável|7|  
  
 \*  localeID -1 significa a localidade padrão. A localidade Inglês é 1033.  
  
 ** Não aplicável = nenhum valor é produzido para esses atributos durante uma operação de seleção no conjunto de colunas. Gera um erro quando um valor é especificado para esse atributo pelo chamador na representação XML fornecida por um conjunto de colunas, em uma operação de inserção ou atualização.  
  
## <a name="security"></a>Segurança  
 O modelo de segurança para um conjunto de colunas funciona de modo semelhante ao modelo de segurança que existe entre tabela e colunas. Os conjuntos de colunas podem ser visualizados como uma minitabela e uma operação de seleção é como uma operação SELECT * nessa minitabela. Mas a relação entre o conjunto de colunas e as colunas esparsas é uma relação de agrupamento, em vez de estritamente um contêiner. O modelo de segurança verifica a segurança na coluna do conjunto de colunas e respeita as operações DENY nas colunas esparsas subjacentes. Características adicionais do modelo de segurança:  
  
-   Permissões de segurança podem ser concedidas e revogadas da coluna do conjunto de colunas, semelhante a qualquer outra coluna na tabela.  
  
-   Um GRANT ou REVOKE de permissões SELECT, INSERT, UPDATE, DELETE e REFERENCES em uma coluna de conjunto de colunas não se propaga às colunas membros subjacentes daquele conjunto. Só se aplica ao uso da coluna do conjunto de colunas. Permissão DENY em um conjunto de colunas se propaga às colunas esparsas subjacentes da tabela.  
  
-   A execução das instruções SELECT, INSERT, UPDATE e DELETE na coluna do conjunto de colunas exige que o usuário tenha permissões correspondentes na coluna do conjunto de colunas e, também, a permissão correspondente em todas as colunas esparsas da tabela. Como o conjunto de colunas representa todas as colunas esparsas na tabela, é necessário ter permissão para todas as colunas esparsas, incluindo as colunas esparsas que podem não estar sendo alteradas.  
  
-   A execução de uma instrução REVOKE em uma coluna esparsa ou conjunto de colunas faz com que a segurança assuma como padrão seu objeto pai.  
  
## <a name="examples"></a>Exemplos  
 Nos exemplos a seguir, uma tabela de documento contém o conjunto comum de colunas `DocID` e `Title`. O grupo de Produção quer uma coluna `ProductionSpecification` e `ProductionLocation` para todos os documentos da produção. O grupo Marketing quer uma coluna `MarketingSurveyGroup` para os documentos de marketing.  
  
### <a name="a-creating-a-table-that-has-a-column-set"></a>A. Criando uma tabela que possui um conjunto de colunas  
 O exemplo a seguir cria a tabela que usa colunas esparsas e inclui o conjunto de colunas `SpecialPurposeColumns`. O exemplo insere duas linhas na tabela e, depois, seleciona dados da tabela.  
  
> [!NOTE]  
>  Essa tabela tem somente cinco colunas para facilitar a exibição e a leitura.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TABLE DocumentStoreWithColumnSet  
    (DocID int PRIMARY KEY,  
     Title varchar(200) NOT NULL,  
     ProductionSpecification varchar(20) SPARSE NULL,  
     ProductionLocation smallint SPARSE NULL,  
     MarketingSurveyGroup varchar(20) SPARSE NULL,  
     MarketingProgramID int SPARSE NULL,  
     SpecialPurposeColumns XML COLUMN_SET FOR ALL_SPARSE_COLUMNS);  
GO  
```  
  
### <a name="b-inserting-data-to-a-table-by-using-the-names-of-the-sparse-columns"></a>B. Inserindo dados em uma tabela usando os nomes das colunas esparsas  
 Os exemplos a seguir inserem duas linhas na tabela criada no exemplo A. Os exemplos usam os nomes das colunas esparsas e não referenciam o conjunto de colunas.  
  
```  
INSERT DocumentStoreWithColumnSet (DocID, Title, ProductionSpecification, ProductionLocation)  
VALUES (1, 'Tire Spec 1', 'AXZZ217', 27);  
GO  
  
INSERT DocumentStoreWithColumnSet (DocID, Title, MarketingSurveyGroup)  
VALUES (2, 'Survey 2142', 'Men 25 - 35');  
GO  
```  
  
### <a name="c-inserting-data-to-a-table-by-using-the-name-of-the-column-set"></a>C. Inserindo dados em uma tabela usando o nome do conjunto de colunas  
 O exemplo a seguir insere uma terceira linha na tabela criada no exemplo A. Dessa vez, os nomes das colunas esparsas não são usados. Em vez disso, o nome do conjunto de colunas é usado e a inserção fornece os valores para duas das colunas esparsas no formato XML.  
  
```  
INSERT DocumentStoreWithColumnSet (DocID, Title, SpecialPurposeColumns)  
VALUES (3, 'Tire Spec 2', '<ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>');  
GO  
```  
  
### <a name="d-observing-the-results-of-a-column-set-when-select--is-used"></a>D. Observando os resultados de um conjunto de colunas quando SELECT * é usado  
 O exemplo a seguir seleciona todas as colunas da tabela que contém um conjunto de colunas. Retorna uma coluna XML com os valores combinados das colunas esparsas. Não retorna as colunas esparsas individualmente.  
  
```  
SELECT DocID, Title, SpecialPurposeColumns FROM DocumentStoreWithColumnSet ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        SpecialPurposeColumns`  
  
 `1      Tire Spec 1  <ProductionSpecification>AXZZ217</ProductionSpecification><ProductionLocation>27</ProductionLocation>`  
  
 `2      Survey 2142  <MarketingSurveyGroup>Men 25 - 35</MarketingSurveyGroup>`  
  
 `3      Tire Spec 2  <ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>`  
  
### <a name="e-observing-the-results-of-selecting-the-column-set-by-name"></a>E. Observando os resultados da seleção do conjunto de colunas por nome  
 Como o departamento de Produção não está interessado nos dados de marketing, este exemplo adiciona uma cláusula `WHERE` para restringir a saída. O exemplo usa o nome do conjunto de colunas.  
  
```  
SELECT DocID, Title, SpecialPurposeColumns  
FROM DocumentStoreWithColumnSet  
WHERE ProductionSpecification IS NOT NULL ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        SpecialPurposeColumns`  
  
 `1     Tire Spec 1  <ProductionSpecification>AXZZ217</ProductionSpecification><ProductionLocation>27</ProductionLocation>`  
  
 `3     Tire Spec 2  <ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>`  
  
### <a name="f-observing-the-results-of-selecting-sparse-columns-by-name"></a>F. Observando os resultados da seleção de colunas esparsas por nome  
 Quando uma tabela contém um conjunto de colunas, você ainda pode consultar a tabela usando nomes de colunas individuais, como mostrado no exemplo a seguir.  
  
```  
SELECT DocID, Title, ProductionSpecification, ProductionLocation   
FROM DocumentStoreWithColumnSet  
WHERE ProductionSpecification IS NOT NULL ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        ProductionSpecification ProductionLocation`  
  
 `1     Tire Spec 1  AXZZ217                 27`  
  
 `3     Tire Spec 2  AXW9R411                38`  
  
### <a name="g-updating-a-table-by-using-a-column-set"></a>G. Atualizando uma tabela usando um conjunto de colunas  
 O exemplo a seguir atualiza o terceiro registro com os novos valores para as colunas esparsas usadas por aquela linha.  
  
```  
UPDATE DocumentStoreWithColumnSet  
SET SpecialPurposeColumns = '<ProductionSpecification>ZZ285W</ProductionSpecification><ProductionLocation>38</ProductionLocation>'  
WHERE DocID = 3 ;  
GO  
```  
  
> [!IMPORTANT]  
>  Uma instrução UPDATE que usa um conjunto de colunas atualiza todas as colunas esparsas na tabela. As colunas esparsas que não são referenciadas são atualizadas como NULL.  
  
 O exemplo a seguir atualiza o terceiro registro, mas só especifica o valor de uma das duas colunas populadas. A segunda coluna `ProductionLocation` não é incluída na instrução `UPDATE` e é atualizada como NULL.  
  
```  
UPDATE DocumentStoreWithColumnSet  
SET SpecialPurposeColumns = '<ProductionSpecification>ZZ285W</ProductionSpecification>'  
WHERE DocID = 3 ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md)  
  
  
