---
title: Argumentos e propriedades de procedimentos armazenados de índice espacial | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- spatial indexes [SQL Server], stored procedures
ms.assetid: ee26082b-c0ed-40ff-b5ad-f5f6b00f0475
author: stevestein
ms.author: sstein
ms.openlocfilehash: 82b906be4568b15a18c55247532bf35b6cd939a7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "69028901"
---
# <a name="spatial-index-stored-procedures---arguments-and-properties"></a>Procedimentos armazenados de índice espacial – argumentos e propriedades
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Este tópico documenta os argumentos e as propriedades para procedimentos armazenados de índice espacial.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
 Para a sintaxe de procedimentos armazenados de índice espacial específicos, consulte os seguintes tópicos:  
  
-   [&#41;&#40;Transact-SQL de sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [&#41;&#40;Transact-SQL de sp_help_spatial_geometry_index_xml](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [&#41;&#40;Transact-SQL de sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [&#41;&#40;Transact-SQL de sp_help_spatial_geography_index_xml](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="arguments"></a>Argumentos  
`[ @tabname = ] 'tabname'`É o nome qualificado ou não qualificado da tabela para a qual o índice espacial foi especificado.  
  
 As aspas somente serão requeridas se uma tabela qualificada for especificada. Se um nome completamente qualificado, incluindo um nome de banco de dados, for fornecido, o nome do banco de dados deverá ser o nome do banco de dados atual. *tabname* é **nvarchar**(776), sem padrão.  
  
`[ @indexname = ] 'indexname'`É o nome do índice espacial especificado. *IndexName* é **sysname** sem padrão.  
  
`[ @verboseoutput = ] 'verboseoutput'`É o intervalo de nomes de propriedade e valores a serem retornados.  
  
 0 = propriedades principais  
  
 \>0 = todas as propriedades  
  
 *verboseoutput* é **tinyint** sem padrão.  
  
`[ @query_sample = ] 'query_sample'`É um exemplo de consulta representativo que pode ser usado para testar a utilidade do índice. Pode ser um objeto representativo ou uma janela de consulta. *query_sample* é **Geometry** sem padrão.  
  
`[ @xml_output = ] 'xml_output'`É um parâmetro de saída que retorna o conjunto de resultados em um fragmento XML. *xml_output* é **XML** sem padrão.  
  
## <a name="properties"></a>Propriedades  
 Defina ** \@verboseoutput** = 0 para retornar propriedades de núcleo, conforme mostrado na tabela abaixo; VerboseOutput > 0 para retornar todas as propriedades do índice espacial. ** \@**  
  
 **Base_Table_Rows**  
 O número de linhas da tabela base. O valor é **bigint**.  
  
 **Bounding_Box_xmin**  
 X-Propriedades da caixa delimitadora mínima do índice espacial para o tipo **Geometry** . Esse valor de propriedade é nulo para o tipo de **geografia**. O valor é **float**.  
  
 **Bounding_Box_ymin**  
 Propriedades da caixa delimitadora Y mínima do índice espacial para o tipo **Geometry** . Esse valor de propriedade é nulo para o tipo de **geografia** . O valor é **float**.  
  
 **Bounding_Box_xmax**  
 X – Propriedades da caixa delimitadora máxima do índice espacial para o tipo **Geometry** . Esse valor de propriedade é nulo para o tipo de **geografia** . O valor é **float**.  
  
 **Bounding_Box_ymax**  
 Y – propriedades da caixa delimitadora máxima do índice espacial para o tipo **Geometry** . Esse valor de propriedade é nulo para o tipo de **geografia** . O valor é **float**.  
  
 **Grid_Size_Level_1**  
 Densidade da grade de nível 1 do índice espacial:  
  
 16 para LOW  
  
 64 para MEDIUM  
  
 256 para HIGH  
  
 O valor é **int**.  
  
 **Grid_Size_Level_2**  
 Densidade da grade de nível 2 do índice espacial:  
  
 16 para LOW  
  
 64 para MEDIUM  
  
 256 para HIGH  
  
 O valor é **int**.  
  
 **Grid_Size_Level_3**  
 Densidade de grade de nível 3 do índice espacial:  
  
 16 para LOW  
  
 64 para MEDIUM  
  
 256 para HIGH  
  
 O valor é **int**.  
  
 **Grid_Size_Level_4**  
 Densidade da grade Nível 4 do índice espacial:  
  
 16 para LOW  
  
 64 para MEDIUM  
  
 256 para HIGH  
  
 O valor é **int**.  
  
 **Cells_Per_Object**  
 Número de células por objeto (propriedade de índice). O valor é **int**.  
  
 **Total_Primary_Index_Rows**  
 O número de linhas no índice. O valor é **bigint**.  
  
 **Total_Primary_Index_Pages**  
 O número de páginas no índice. O valor é **bigint**.  
  
 **Average_Number_Of_Index_Rows_Per_Base_Row**  
 O número de linhas do índice/linhas da tabela base. O valor é **bigint**.  
  
 **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample**  
 Indica se o exemplo de consulta representativo está fora da caixa delimitadora do índice de **geometria** e na célula raiz (nível 0 célula). Este é 0 (não em célula de nível 0) ou 1. Se estiver na célula nível 0, o índice investigado não será um índice apropriado para o exemplo de consulta. Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_ObjectCells_In_Level0_In_Index**  
 Número de instâncias de célula de objetos indexados que são mosaico no nível 0 (célula raiz, fora da caixa delimitadora para **geometria**). Esta é uma propriedade principal. O valor é **bigint**.  
  
 Para índices de **geometria** , isso ocorrerá se a caixa delimitadora do índice for menor do que o domínio de dados. Um grande número de objetos no nível 0 pode exigir filtros secundários se a janela de consulta cair parcialmente fora da caixa delimitadora e diminuir o desempenho do índice (por exemplo, **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample** é 1). Se a janela de consulta estiver dentro da caixa delimitadora, um número elevado de objetos no nível 0 pode melhorar o desempenho do índice.  
  
 As instâncias NULL e vazias são contadas no nível 0, mas não influenciam o desempenho. O nível 0 terá o mesmo número de células e de instâncias NULL e vazias na tabela base. Para índices de **geografia** , o nível 0 terá tantas células quanto nulas e instâncias vazias + 1 célula, porque o exemplo de consulta é contado como 1.  
  
 **Total_Number_Of_ObjectCells_In_Level1_In_Index**  
 Número de instâncias de célula de objetos indexados que são mosaico com precisão de nível 1. Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_ObjectCells_In_Level2_In_Index**  
 Número de instâncias de célula de objetos indexados que são mosaico com precisão de nível 2. Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_ObjectCells_In_Level3_In_Index**  
 Número de instâncias de célula de objetos indexados que são mosaico com precisão de nível 3. Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_ObjectCells_In_Level4_In_Index**  
 O número de instâncias de célula de objetos indexados que são incluídas em mosaicos com previsão de nível 4. Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level1_In_Index**  
 Número de células que são completamente cobertas por um objeto no mosaico nível 1 e, portanto, são interiores para o objeto. (Cell_attributevalue é 2.) Essa é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level2_In_Index**  
 Número de células que são completamente cobertas por um objeto no nível de mosaico 2 e, portanto, são interiores para o objeto. (O valor de Cell_attribute é 2.) Essa é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level3_In_Index**  
 Número de células que são completamente cobertas por um objeto no mosaico nível 3 e, portanto, são interiores para o objeto. (O valor de Cell_attribute é 2.) Essa é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level4_In_Index**  
 O número de células que são completamente abrangidas por um objeto em um mosaico de nível 4 e, portanto, fazem parte do objeto. (O valor de Cell_attribute é 2.) Essa é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level1_In_Index**  
 Número de células que são interseccionadas por um objeto no nível de mosaico 1. (Cell_attribute valor é 1.) Essa é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level2_In_Index**  
 Número de células que são interseccionadas por um objeto no nível de mosaico 2. (Cell_attribute valor é 1.) Essa é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level3_In_Index**  
 Número de células que são interseccionadas por um objeto no nível 3 do mosaico. (Cell_attribute valor é 1.) Essa é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level4_In_Index**  
 Número de células que são intersectadas por um objeto no mosaico de nível 4. (Cell_attribute valor é 1.) Essa é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_For_QuerySample**  
 Indica se o exemplo de consulta está na célula raiz 0 fora da caixa delimitadora, mas tocando-a. Esta é uma propriedade principal. O valor é **bigint**.  
  
> [!NOTE]  
>  Esta informações é útil apenas ao determinar se há objetos que a caixa delimitadora pode ter ignorado.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_In_Index**  
 Número de objetos em nível 0 que ticam a caixa delimitadora. (Cell_attribute valor é 0.)  O valor é **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level1_In_Index**  
 Número de células de objeto que tocam um limite de células de grade no nível de mosaico 1. (Cell_attribute valor é 0.) Essa é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level2_In_Index**  
 Número de células de objeto que tocam um limite de células de grade no nível de mosaico 2. (Cell_attribute valor é 0.) Essa é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level3_In_Index**  
 Número de células de objeto que tocam o limite de uma célula de grade no nível 3 do mosaico. (Cell_attribute valor é 0.) Essa é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level4_In_Index**  
 Número de células de objeto que tocam um limite de célula de grade no mosaico nível 4. (Cell_attribute valor é 0.) Essa é uma propriedade principal. O valor é **bigint**.  
  
 **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 Porcentagem da área total (total de células folha) da grade que contém células folha cobertas por um objeto.  
  
 Por exemplo, um objeto é incluído em um mosaico em 10 células em 4 níveis de grade diferentes que cobrem uma área equivalente a 100 células folha. Suponha que há 3 células interiores que são cobertas completamente pelo objeto. A área coberta pelas 3 células interiores é equivalente a 42 células folha. Assim, a porcentagem de área coberta é 42 por cento. Esse é um bom exemplo de quão bem os objetos estão fragmentados no índice.  
  
 O valor é **float**.  
  
 **Intersecting_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 O mesmo que **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**, exceto que essas são células parcialmente cobertas. O valor é **float**.  
  
 **Border_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 O mesmo que **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage** , exceto que eles são células de borda. O valor é **float**.  
  
 **Average_Cells_Per_Object_Normalized_To_Leaf_Grid**  
 Células comuns por objeto normalizado na grade da folha. Isso nos dá uma indicação do tamanho espacial do objeto ou de quão grande os objetos são. O valor é **float**.  
  
 **Average_Objects_PerLeaf_GridCell**  
 Dispersão do índice. Número médio de objetos por célula folha. O valor é **float**.  
  
 **Number_Of_SRIDs_Found**  
 O número de SRIDs exclusivo no índice e na coluna. O valor é **int**.  
  
 Como uma coluna pode conter mais de um SRID e os objetos de SRIDs diferentes nunca cruzam, o número de SRIDs indicam a seletividade do índice.  
  
 **Width_Of_Cell_In_Level1**  
 Propriedade de largura da célula na grade de indexação. A unidade de medida é fornecida pelo índice e depende no SRID dos dados indexados. O valor é **float**.  
  
 **Width_Of_Cell_In_Level2**  
 Propriedade de largura da célula na grade de indexação. A unidade de medida é fornecida pelo índice e depende no SRID dos dados indexados. O valor é **float**.  
  
 **Width_Of_Cell_In_Level3**  
 Propriedade de largura da célula na grade de indexação. A unidade de medida é fornecida pelo índice e depende no SRID dos dados indexados. O valor é **float**.  
  
 **Width_Of_Cell_In_Level4**  
 Propriedade de largura da célula na grade de indexação. A unidade de medida é fornecida pelo índice e depende do SRID dos dados indexados. O valor é **float**.  
  
 **Height_Of_Cell_In_Level1**  
 Propriedade de altura da célula na grade de indexação. A unidade de medida é fornecida pelo índice e depende no SRID dos dados indexados. O valor é **float**.  
  
 **Height_Of_Cell_In_Level2**  
 Propriedade de altura da célula na grade de indexação. A unidade de medida é fornecida pelo índice e depende no SRID dos dados indexados. O valor é **float**.  
  
 **Height_Of_Cell_In_Level3**  
 Propriedade de altura da célula na grade de indexação. A unidade de medida é fornecida pelo índice e depende no SRID dos dados indexados. O valor é **float**.  
  
 **Height_Of_Cell_In_Level4**  
 Propriedade de altura da célula na grade de indexação. A unidade de medida é fornecida pelo índice e depende no SRID dos dados indexados. O valor é **float**.  
  
 **Area_Of_Cell_In_Level1**  
 Propriedade de área da célula na grade de indexação. A unidade de medida é fornecida pelo índice e depende no SRID dos dados indexados. O valor é **float**.  
  
 **Area_Of_Cell_In_Level2**  
 Propriedade de área da célula na grade de indexação. A unidade de medida é fornecida pelo índice e depende no SRID dos dados indexados. O valor é **float**.  
  
 **Area_Of_Cell_In_Level3**  
 Propriedade de área da célula na grade de indexação. A unidade de medida é fornecida pelo índice e depende no SRID dos dados indexados. O valor é **float**.  
  
 **Area_Of_Cell_In_Level4**  
 Propriedade de área da célula na grade de indexação. A unidade de medida é fornecida pelo índice e depende no SRID dos dados indexados. O valor é **float**.  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level1**  
 A porcentagem de cobertura da caixa delimitadora por uma célula de nível 1. O valor é **float**.  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level2**  
 A porcentagem de cobertura da caixa delimitadora por uma célula de nível 2. O valor é **float**.  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level3**  
 A porcentagem de cobertura da caixa delimitadora por uma célula de nível 3. O valor é **float**.  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level4**  
 A porcentagem de cobertura da caixa delimitadora por uma célula de nível 4. O valor é **float**.  
  
 **Number_Of_Rows_Selected_By_Primary_Filter**  
 O número de linhas selecionadas pelo filtro primário. Esta é uma propriedade principal. O valor é **bigint.**  
  
 **Number_Of_Rows_Selected_By_Internal_Filter**  
 O número de linhas selecionadas pelo filtro interno. O filtro secundário não é chamado para essas linhas. Esta é uma propriedade principal. O valor é **bigint.**  
  
 O número retornado só é aplicável a **interseções**.  
  
 **Number_Of_Times_Secondary_Filter_Is_Called**  
 O número de vezes que o filtro secundário é chamado. Esta é uma propriedade principal. O valor é **bigint.**  
  
 **Percentage_Of_Rows_NotSelected_By_Primary_Filter**  
 Se houver linhas N na tabela base e P forem selecionados pelo filtro primário, (N-P)/N será retornado como porcentagem. Esta é uma propriedade principal. O valor é **float.**  
  
 **Percentage_Of_Primary_Filter_Rows_Selected_By_internal_Filter**  
 Se linhas P estiverem selecionadas pelo filtro primário e linhas S estiverem selecionadas pelo filtro interno, S/P será retornado como porcentagem. Quando mais alta for a porcentagem, melhor será o índice ao evitar o filtro secundário com desempenho mais caro. Esta é uma propriedade principal. O valor é **float.**  
  
 **Number_Of_Rows_Output**  
 O número de saída de linhas produzido pela consulta. Esta é uma propriedade principal. O valor é **bigint.**  
  
 **Internal_Filter_Efficiency**  
 Se O for o número de saída de linhas, S/O será retornado como uma porcentagem. Esta é uma propriedade principal. O valor é **float.**  
  
 **Primary_Filter_Efficiency**  
 Se P linhas forem selecionadas pelo filtro primário e o for o número de saídas de linhas, isso retornará/P como uma porcentagem. Quanto mais alta for a eficiência do filtro primário, menores serão os positivos falsos que o filtro secundário terá que processar. Esta é uma propriedade principal. O valor é **float.**  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ser um membro da função **pública** . Requer permissão READ ACCESS no servidor e no objeto. Isto se aplica a procedimentos armazenados de índice espacial.  
  
## <a name="remarks"></a>Comentários  
 As propriedades que contêm valores NULL não são incluídas no conjunto de retorno.  
  
## <a name="examples"></a>Exemplos  
 Para obter exemplos, consulte os tópicos a seguir:  
  
-   [&#41;&#40;Transact-SQL de sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [&#41;&#40;Transact-SQL de sp_help_spatial_geometry_index_xml](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [&#41;&#40;Transact-SQL de sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [&#41;&#40;Transact-SQL de sp_help_spatial_geography_index_xml](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="requirements"></a>Requisitos  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de índice espacial &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [&#41;&#40;Transact-SQL de sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [Visão geral dos índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Noções básicas do XQuery](../../xquery/xquery-basics.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
