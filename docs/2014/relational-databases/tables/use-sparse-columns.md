---
title: Usar colunas esparsas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- sparse columns, described
- null columns
- sparse columns
ms.assetid: ea7ddb87-f50b-46b6-9f5a-acab222a2ede
author: stevestein
ms.author: sstein
ms.openlocfilehash: b3068ac7a3094605bb809ac84c63766b64fda486
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85002903"
---
# <a name="use-sparse-columns"></a>Usar colunas esparsas
  Colunas esparsas são colunas comuns que têm um armazenamento otimizado para valores nulos. Elas reduzem os requisitos de espaço para valores nulos às custas de maior sobrecarga para recuperar valores não nulos. Considere o uso de colunas esparsas quando o espaço salvo for pelo menos de 20 a 40 por cento. As colunas esparsas e os conjuntos de colunas são definidos usando as instruções [CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql) ou [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) .  
  
 As colunas esparsas podem ser usadas com conjuntos de colunas e índices filtrados:  
  
-   Conjuntos de colunas  
  
     As instruções INSERT, UPDATE e DELETE podem referenciar colunas esparsas pelo nome. Entretanto, você também pode exibir e trabalhar com todas as colunas esparsas de uma tabela, combinadas em uma única coluna XML. Essa coluna é denominada conjunto de colunas. Para obter mais informações sobre conjuntos de colunas, veja [Usar conjuntos de colunas](../tables/use-column-sets.md).  
  
-   Índices filtrados  
  
     Como as colunas esparsas têm muitas linhas de valor nulo, elas são especialmente apropriadas para índices filtrados. Um índice filtrado em uma coluna esparsa pode indexar somente as linhas com valores populados. Isso cria um índice menor e mais eficiente. Para saber mais, confira [Create Filtered Indexes](../indexes/indexes.md).  
  
 As colunas esparsas e os índices filtrados habilitam aplicativos, como o [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], para armazenar e acessar com eficiência um grande número de propriedades definidas pelo usuário usando o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="properties-of-sparse-columns"></a>Propriedades das colunas esparsas  
 As colunas esparsas têm as seguintes características:  
  
-   O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usa a palavra-chave SPARSE em uma definição de coluna otimizar o armazenamento de valores naquela coluna. Portanto, quando o valor da coluna for NULL para qualquer linha na tabela, os valores não exigirão armazenamento.  
  
-   As exibições do catálogo para uma tabela que tenha colunas esparsas são as mesmas que para uma tabela típica. A exibição do catálogo sys.columns contém uma linha para cada coluna na tabela e inclui um conjunto de colunas, se houver um definido.  
  
-   Colunas esparsas são uma propriedade da camada de armazenamento, não a tabela lógica. Portanto, uma instrução SELECT...INTO não copia sobre a propriedade de coluna esparsa em uma nova tabela.  
  
-   A função COLUMNS_UPDATED retorna um valor `varbinary` para indicar todas as colunas atualizadas durante uma ação DML. Os bits retornados pela função COLUMNS_UPDATED são os seguintes:  
  
    -   Quando uma coluna esparsa é explicitamente atualizada, o bit correspondente àquela coluna esparsa é definido como 1 e o bit para o conjunto de colunas é definido como 1.  
  
    -   Quando um conjunto de colunas é explicitamente atualizado, o bit para o conjunto de colunas é definido como 1 e os bits para todas as colunas esparsas naquela tabela são definidos como 1.  
  
    -   Para operações de inserção, todos os bits são definidos como 1.  
  
     Para obter mais informações sobre conjuntos de colunas, veja [Usar conjuntos de colunas](../tables/use-column-sets.md).  
  
 Os seguintes tipos de dados não podem ser especificados como SPARSE:  
  
|||  
|-|-|  
|`geography`|`text`|  
|`geometry`|`timestamp`|  
|`image`|`user-defined data types`|  
|`ntext`||  
  
## <a name="estimated-space-savings-by-data-type"></a>Aumento de espaço estimado por tipo de dados  
 As colunas esparsas exigem mais espaço de armazenamento para valores não nulos do que o espaço exigido para dados idênticos não marcados como SPARSE. As tabelas a seguir mostram o uso de espaço para cada tipo de dados. A coluna **Percentual de NULL** indica o percentual de dados que deve ser NULL para um aumento de espaço de 40 por cento.  
  
 **Tipos de dados de comprimento fixo**  
  
|Tipo de dados|Bytes não esparsos|Bytes esparsos|Percentual de NULL|  
|---------------|---------------------|------------------|---------------------|  
|`bit`|0,125|5|98%|  
|`tinyint`|1|5|86%|  
|`smallint`|2|6|76%|  
|`int`|4|8|64%|  
|`bigint`|8|12|52%|  
|`real`|4|8|64%|  
|`float`|8|12|52%|  
|`smallmoney`|4|8|64%|  
|`money`|8|12|52%|  
|`smalldatetime`|4|8|64%|  
|`datetime`|8|12|52%|  
|`uniqueidentifier`|16|20|43%|  
|`date`|3|7|69%|  
  
 **Tipos de dados de comprimento dependente de precisão**  
  
|Tipo de dados|Bytes não esparsos|Bytes esparsos|Percentual de NULL|  
|---------------|---------------------|------------------|---------------------|  
|`datetime2(0)`|6|10|57%|  
|`datetime2(7)`|8|12|52%|  
|`time(0)`|3|7|69%|  
|`time(7)`|5|9|60%|  
|`datetimetoffset(0)`|8|12|52%|  
|`datetimetoffset (7)`|10|14|49%|  
|`decimal/numeric(1,s)`|5|9|60%|  
|`decimal/numeric(38,s)`|17|21|42%|  
|`vardecimal(p,s)`|Use o tipo `decimal` como uma estimativa conservadora.|||  
  
 **Tipos de dados de comprimento dependente de dados**  
  
|Tipo de dados|Bytes não esparsos|Bytes esparsos|Percentual de NULL|  
|---------------|---------------------|------------------|---------------------|  
|`sql_variant`|Varia de acordo com o tipo de dados subjacente|||  
|`varchar` ou `char`|2*|4*|60%|  
|`nvarchar` ou `nchar`|2*|4*+|60%|  
|`varbinary` ou `binary`|2*|4*|60%|  
|`xml`|2*|4*|60%|  
|`hierarchyid`|2*|4*|60%|  
  
 * O comprimento é igual à média dos dados que estão contidos no tipo, mais 2 ou 4 bytes.  
  
## <a name="in-memory-overhead-required-for-updates-to-sparse-columns"></a>Sobrecarga na memória necessária para atualizações em colunas esparsas  
 Quando for criar tabelas com colunas esparsas, tenha em mente que uma sobrecarga adicional de 2 bytes é necessária para cada coluna esparsa não nula na tabela quando uma linha está sendo atualizada. Em resultado dessa necessidade de memória adicional, as atualizações podem falhar inesperadamente com o erro 576 quando o tamanho total da linha, incluindo essa sobrecarga de memória, excede 8019, e nenhuma coluna pode ser retirada da linha.  
  
 Considere o exemplo de uma tabela que tem 600 colunas esparsas do tipo bigint. Se houver 571 colunas não nulas, o tamanho total em disco será 571 * 12 = 6852 bytes. Depois de incluir a sobrecarga de linha adicional e o cabeçalho da coluna esparsa, isso aumenta para cerca de 6895 bytes. A página ainda tem cerca de 1124 bytes disponíveis em disco. Isso pode dar a impressão de que as colunas adicionais podem ser atualizadas com sucesso. No entanto, durante a atualização, há uma sobrecarga adicional na memória que é 2\*(o número de colunas esparsas não nulas). Neste exemplo, incluir a sobrecarga adicional – 2 \* 571 = 1142 bytes – aumenta o tamanho da linha no disco em torno de 8037 bytes. Esse tamanho excede o tamanho máximo permitido de 8019 bytes. Como todas as colunas têm tipos de dados de comprimento fixo, elas não podem ser retiradas da linha. Portanto, a atualização falha com o erro 576.  
  
## <a name="restrictions-for-using-sparse-columns"></a>Restrições para o uso de colunas esparsas  
 As colunas esparsas podem ser de qualquer tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e podem se comportar como qualquer outra coluna com as seguintes restrições:  
  
-   Uma coluna esparsa deve permitir valor nulo e não deve ter as propriedades ROWGUIDCOL ou IDENTITY. Uma coluna esparsa não pode ser nenhum destes tipos de dados: `text`, `ntext`, `image`, `timestamp`, tipo de dados definido pelo usuário, `geometry` ou `geography`; ou ter o atributo FILESTREAM.  
  
-   Uma coluna esparsa não pode ter um valor padrão.  
  
-   Uma coluna esparsa não pode estar associada a uma regra.  
  
-   Embora uma coluna computada possa conter uma coluna esparsa, uma coluna computada não pode ser marcada como SPARSE.  
  
-   Uma coluna esparsa não pode fazer parte de um índice clusterizado ou de um índice de chave primária exclusivo. Entretanto, as colunas computadas persistentes e não persistentes definidas em colunas esparsas podem fazer parte de uma chave clusterizada.  
  
-   Uma coluna esparsa não pode ser usada como uma chave de partição de um índice clusterizado ou heap. Porém, uma coluna esparsa pode ser usada como a chave de partição de um índice não clusterizado.  
  
-   Uma coluna esparsa não pode fazer parte de um tipo de tabela definido pelo usuário, usado em variáveis de tabela e em parâmetros com valor de tabela.  
  
-   Colunas esparsas são incompatíveis com a compactação de dados. Portanto, colunas esparsas não podem ser adicionadas a tabelas compactadas, e nenhuma tabela que contenha colunas esparsas pode ser compactada.  
  
-   A alteração de uma coluna de esparsa para não esparsa ou de não esparsa para esparsa exige a alteração do formato de armazenamento da coluna. O Mecanismo de Banco de Dados do SQL Server usa o procedimento a seguir para executar essa alteração:  
  
    1.  Adiciona uma nova coluna à tabela no novo tamanho e formato de armazenamento.  
  
    2.  Para cada linha na tabela, atualiza e copia o valor armazenado na coluna antiga na coluna nova.  
  
    3.  Remove a coluna antiga do esquema da tabela.  
  
    4.  Reconstrói a tabela (se não houver nenhum índice clusterizado) ou reconstrói o índice clusterizado para recuperar o espaço usado pela coluna antiga.  
  
    > [!NOTE]  
    >  A etapa 2 pode falhar quando o tamanho dos dados na linha exceder o tamanho máximo de linha permitido. Esse tamanho inclui o tamanho dos dados armazenados na coluna antiga e os dados atualizados armazenados na coluna nova. Esse limite é de 8060 bytes para tabelas que não contêm nenhuma coluna esparsa ou 8018 bytes para tabelas que contêm colunas esparsas. Esse erro poderá ocorrer até mesmo se todas as colunas elegíveis forem empurradas para fora da linha.  
  
-   Quando você alterar uma coluna não esparsa para uma coluna esparsa, a coluna esparsa consumirá mais espaço para valores não nulos. Quando uma linha está próxima do limite de tamanho máximo de linha, pode haver falha na operação.  
  
## <a name="sql-server-technologies-that-support-sparse-columns"></a>Tecnologias do SQL Server que oferecem suporte a colunas esparsas  
 Esta seção descreve como as colunas esparsas têm suporte nas seguintes tecnologias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   Replicação transacional  
  
     A replicação transacional oferece suporte a colunas esparsas, mas não oferece suporte a conjuntos de colunas que podem ser usados com colunas esparsas. Para obter mais informações sobre conjuntos de colunas, veja [Usar conjuntos de colunas](../tables/use-column-sets.md).  
  
     A replicação do atributo SPARSE é determinada por uma opção de esquema especificada usando [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) ou usando a caixa de diálogo **Propriedades do Artigo** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. As versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dão suporte a colunas esparsas. Se for necessário replicar dados para uma versão anterior, especifique que o atributo SPARSE não deve ser replicado.  
  
     Para tabelas publicadas, não é possível adicionar novas colunas esparsas a uma tabela nem alterar a propriedade esparsa de uma coluna existente. Se tal operação for exigida, descarte e recrie a publicação.  
  
-   Replicação de mesclagem  
  
     A replicação de mesclagem não oferece suporte a colunas esparsas ou conjuntos de colunas.  
  
-   Change tracking  
  
     O controle de alterações oferece suporte a colunas esparsas e conjuntos de colunas. Quando um conjunto de colunas é atualizado em uma tabela, o controle de alterações trata isso como uma atualização em toda a linha. Nenhum controle de alteração detalhado é fornecido para obter o conjunto exato de colunas esparsas atualizadas pela operação de atualização de conjunto de colunas. Se as colunas esparsas forem atualizadas explicitamente por uma instrução DML, o controle de alterações funcionará de forma comum e poderá identificar o conjunto exato das colunas alteradas.  
  
-   captura de dados de alterações  
  
     O Change Data Capture oferece suporte a colunas esparsas, mas não a conjuntos de colunas.  
  
-   A propriedade esparsa de uma coluna não é preservada quando a tabela é copiada.  
  
## <a name="examples"></a>Exemplos  
 Neste exemplo, uma tabela de documento contém um conjunto comum que tem as colunas `DocID` e `Title`. O grupo de Produção quer uma coluna `ProductionSpecification` e `ProductionLocation` para todos os documentos da produção. O grupo Marketing quer uma coluna `MarketingSurveyGroup` para os documentos de marketing. O código neste exemplo cria uma tabela que usa colunas esparsas, insere duas linhas na tabela e, depois, seleciona dados da tabela.  
  
> [!NOTE]  
>  Essa tabela tem somente cinco colunas para facilitar a exibição e a leitura. A declaração de colunas esparsas para aceitarem valores nulos será opcional se a opção ANSI_NULL_DFLT_ON estiver definida.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TABLE DocumentStore  
    (DocID int PRIMARY KEY,  
     Title varchar(200) NOT NULL,  
     ProductionSpecification varchar(20) SPARSE NULL,  
     ProductionLocation smallint SPARSE NULL,  
     MarketingSurveyGroup varchar(20) SPARSE NULL ) ;  
GO  
  
INSERT DocumentStore(DocID, Title, ProductionSpecification, ProductionLocation)  
VALUES (1, 'Tire Spec 1', 'AXZZ217', 27);  
GO  
  
INSERT DocumentStore(DocID, Title, MarketingSurveyGroup)  
VALUES (2, 'Survey 2142', 'Men 25 - 35');  
GO  
```  
  
 A seleção de todas as colunas da tabela retorna um conjunto de resultados comum.  
  
```  
SELECT * FROM DocumentStore ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID  Title        ProductionSpecification  ProductionLocation  MarketingSurveyGroup`  
  
 `1      Tire Spec 1  AXZZ217                  27                  NULL`  
  
 `2      Survey 2142  NULL                     NULL                Men 25-35`  
  
 Como o departamento de Produção não está interessado nos dados de marketing, eles querem usar uma lista de colunas que retorne somente colunas de interesse, como mostrado na consulta a seguir.  
  
```  
SELECT DocID, Title, ProductionSpecification, ProductionLocation   
FROM DocumentStore   
WHERE ProductionSpecification IS NOT NULL ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID  Title        ProductionSpecification  ProductionLocation`  
  
 `1      Tire Spec 1  AXZZ217                  27`  
  
## <a name="see-also"></a>Consulte Também  
 [Usar conjuntos de colunas](../tables/use-column-sets.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [sys.columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-columns-transact-sql)  
  
  
