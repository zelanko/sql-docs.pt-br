---
title: Procedimentos armazenados de argumentos e propriedades de índice espacial | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ccd9e2be26c8d514e17a4aa03af422cd648fe426
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51666595"
---
# <a name="spatial-index-stored-procedures---arguments-and-properties"></a>Índice espacial procedimentos armazenados – argumentos e propriedades
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Este tópico documenta os argumentos e as propriedades para procedimentos armazenados de índice espacial.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
 Para a sintaxe de procedimentos armazenados de índice espacial específicos, consulte os seguintes tópicos:  
  
-   [sp_help_spatial_geometry_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [sp_help_spatial_geometry_index_xml &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [sp_help_spatial_geography_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [sp_help_spatial_geography_index_xml &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="arguments"></a>Argumentos  
 [  **@tabname =**] **'***tabname***'**  
 É o nome qualificado ou não da tabela para a qual o índice espacial foi especificado.  
  
 As aspas somente serão requeridas se uma tabela qualificada for especificada. Se um nome completamente qualificado, incluindo um nome de banco de dados, for fornecido, o nome do banco de dados deverá ser o nome do banco de dados atual. *tabname* está **nvarchar**(776), sem padrão.  
  
 [  **@indexname =** ] **'***indexname***'**  
 É o nome do índice espacial especificado. *indexName* está **sysname** sem nenhum padrão.  
  
 [  **@verboseoutput =** ] **'***verboseoutput***'**  
 É o intervalo dos nomes de propriedade e valores a ser retornado.  
  
 0 = propriedades principais  
  
 \>0 = todas as propriedades  
  
 *verboseoutput* está **tinyint** sem nenhum padrão.  
  
 [  **@query_sample =** ] **'***query_sample***'**  
 É um exemplo de consulta representativo que pode ser usado para testar a utilidade do índice. Pode ser um objeto representativo ou uma janela de consulta. *query_sample* está **geometria** sem nenhum padrão.  
  
 [  **@xml_output =** ] **'***xml_output***'**  
 É um parâmetro de saída que retorna o conjunto de resultados em um fragmento XML. *xml_output* está **xml** sem nenhum padrão.  
  
## <a name="properties"></a>Propriedades  
 Definir **@verboseoutput** = 0 para retornar as propriedades principais, conforme mostrado na tabela a seguir. **@verboseoutput** > 0 para retornar todas as propriedades do índice espacial.  
  
 **Base_Table_Rows**  
 O número de linhas da tabela base. O valor é **bigint**.  
  
 **Colunas Bounding_Box_xmin**  
 Mínimo de X delimitadora do índice espacial para propriedades da caixa **geometria** tipo. Esse valor da propriedade é NULL para **geografia**tipo. O valor é **float**.  
  
 **Bounding_Box_ymin**  
 Propriedades da caixa de índice espacial para delimitadora mínima de Y **geometria** tipo. Esse valor da propriedade é NULL para **geografia** tipo. O valor é **float**.  
  
 **Bounding_Box_xmax**  
 Propriedades da caixa de índice espacial para delimitadora máxima de X **geometria** tipo. Esse valor da propriedade é NULL para **geografia** tipo. O valor é **float**.  
  
 **Bounding_Box_ymax**  
 Propriedades da caixa de índice espacial para delimitadora máxima de Y **geometria** tipo. Esse valor da propriedade é NULL para **geografia** tipo. O valor é **float**.  
  
 **Grid_Size_Level_1**  
 Densidade de grade nível 1 do índice espacial:  
  
 16 para LOW  
  
 64 para MEDIUM  
  
 256 para HIGH  
  
 O valor é **int**.  
  
 **Grid_Size_Level_2**  
 Densidade de grade de nível 2 do índice espacial:  
  
 16 para LOW  
  
 64 para MEDIUM  
  
 256 para HIGH  
  
 O valor é **int**.  
  
 **Grid_Size_Level_3**  
 Densidade de grade nível 3 do índice espacial:  
  
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
 Indica se o exemplo de consulta representativo está fora da caixa delimitadora do **geometria** índice e, em uma célula raiz (célula nível 0). Este é 0 (não em célula de nível 0) ou 1. Se estiver na célula nível 0, o índice investigado não será um índice apropriado para o exemplo de consulta. Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_ObjectCells_In_Level0_In_Index**  
 Número de instâncias de célula de objetos indexados que são incluídas no mosaico no nível 0 (célula raiz, fora da caixa delimitadora para **geometria**). Esta é uma propriedade principal. O valor é **bigint**.  
  
 Para **geometria** índices, isso ocorrerá se a caixa delimitadora do índice é menor do que o domínio de dados. Um grande número de objetos no nível 0 pode exigir filtros secundários caso a janela de consulta esteja parcialmente fora a delimitação caixa e diminuirão o desempenho do índice (por exemplo, **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample** é 1). Se a janela de consulta estiver dentro da caixa delimitadora, um número elevado de objetos no nível 0 pode melhorar o desempenho do índice.  
  
 As instâncias NULL e vazias são contadas no nível 0, mas não influenciam o desempenho. O nível 0 terá o mesmo número de células e de instâncias NULL e vazias na tabela base. Para **geografia** índices, o nível 0 terá o número de células como NULL e a célula de instâncias vazias + 1, porque o exemplo de consulta é contado como 1.  
  
 **Total_Number_Of_ObjectCells_In_Level1_In_Index**  
 Número de instâncias de célula de objetos indexados que são incluídas no mosaico com precisão de nível 1. Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_ObjectCells_In_Level2_In_Index**  
 Número de instâncias de célula de objetos indexados que são incluídas no mosaico com precisão de nível 2. Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_ObjectCells_In_Level3_In_Index**  
 Número de instâncias de célula de objetos indexados que são incluídas no mosaico com precisão de nível 3. Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_ObjectCells_In_Level4_In_Index**  
 O número de instâncias de célula de objetos indexados que são incluídas em mosaicos com previsão de nível 4. Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level1_In_Index**  
 Número de células que são completamente abrangidas por um objeto no mosaico de nível 1 e, portanto, são parte do objeto. (Cell_attributevalue é 2.) Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level2_In_Index**  
 Número de células que são completamente abrangidas por um objeto no mosaico de nível 2 e, portanto, são parte do objeto. (O valor de Cell_attribute é 2.) Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level3_In_Index**  
 Número de células que são completamente abrangidas por um objeto no mosaico de nível 3 e, portanto, são parte do objeto. (O valor de Cell_attribute é 2.) Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level4_In_Index**  
 O número de células que são completamente abrangidas por um objeto em um mosaico de nível 4 e, portanto, fazem parte do objeto. (O valor de Cell_attribute é 2.) Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level1_In_Index**  
 Número de células que são intersectadas por um objeto no mosaico de nível 1. (O valor de Cell_attribute é 1.) Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level2_In_Index**  
 Número de células que são intersectadas por um objeto no mosaico de nível 2. (O valor de Cell_attribute é 1.) Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level3_In_Index**  
 Número de células que são intersectadas por um objeto no mosaico de nível 3. (O valor de Cell_attribute é 1.) Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level4_In_Index**  
 Número de células que são intersectadas por um objeto no mosaico de nível 4. (O valor de Cell_attribute é 1.) Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_For_QuerySample**  
 Indica se o exemplo de consulta está na célula raiz 0 fora da caixa delimitadora, mas tocando-a. Esta é uma propriedade principal. O valor é **bigint**.  
  
> [!NOTE]  
>  Esta informações é útil apenas ao determinar se há objetos que a caixa delimitadora pode ter ignorado.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_In_Index**  
 Número de objetos em nível 0 que ticam a caixa delimitadora. (O valor de Cell_attribute é 0.)  O valor é **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level1_In_Index**  
 Número de células de objeto que tocam um limite de células de grade no mosaico de nível 1. (O valor de Cell_attribute é 0.) Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level2_In_Index**  
 Número de células de objeto que tocam um limite de células de grade no mosaico nível 2. (O valor de Cell_attribute é 0.) Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level3_In_Index**  
 Número de células de objeto que tocam um limite de células de grade no mosaico nível 3. (O valor de Cell_attribute é 0.) Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level4_In_Index**  
 Número de células de objeto que tocam um limite de célula de grade no mosaico nível 4. (O valor de Cell_attribute é 0.) Esta é uma propriedade principal. O valor é **bigint**.  
  
 **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 Porcentagem da área total (total de células folha) da grade que contém células folha cobertas por um objeto.  
  
 Por exemplo, um objeto é incluído em um mosaico em 10 células em 4 níveis de grade diferentes que cobrem uma área equivalente a 100 células folha. Suponha que há 3 células interiores que são cobertas completamente pelo objeto. A área coberta pelas 3 células interiores é equivalente a 42 células folha. Assim, a porcentagem de área coberta é 42 por cento. Esse é um bom exemplo de quão bem os objetos estão fragmentados no índice.  
  
 O valor é **float**.  
  
 **Intersecting_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 Mesmo que **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**, exceto que essas são células parcialmente cobertas. O valor é **float**.  
  
 **Border_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 Mesmo que **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage** , exceto que as células de borda. O valor é **float**.  
  
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
  
 O número retornado só é aplicável para **STintersects**.  
  
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
 Se linhas P estiverem selecionadas pelo filtro primário e s é o número de linhas de saída, este returnsO/P como uma porcentagem. Quanto mais alta for a eficiência do filtro primário, menores serão os positivos falsos que o filtro secundário terá que processar. Esta é uma propriedade principal. O valor é **float.**  
  
## <a name="permissions"></a>Permissões  
 Usuário deve ser um membro do **pública** função. Requer permissão READ ACCESS no servidor e no objeto. Isto se aplica a procedimentos armazenados de índice espacial.  
  
## <a name="remarks"></a>Comentários  
 As propriedades que contêm valores NULL não são incluídas no conjunto de retorno.  
  
## <a name="examples"></a>Exemplos  
 Para obter exemplos, consulte os tópicos a seguir:  
  
-   [sp_help_spatial_geometry_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [sp_help_spatial_geometry_index_xml &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [sp_help_spatial_geography_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [sp_help_spatial_geography_index_xml &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="requirements"></a>Requisitos  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de índice espacial &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Fundamentos de XQuery](../../xquery/xquery-basics.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
