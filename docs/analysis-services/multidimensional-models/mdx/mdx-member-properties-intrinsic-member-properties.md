---
title: Propriedades intrínsecas do membro (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e54aa6bb53e6ce9f34e6647927f29b7aadb97180
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740241"
---
# <a name="mdx-member-properties---intrinsic-member-properties"></a>Propriedades de membro MDX – propriedades intrínsecas do membro
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] expõe propriedades intrínsecas em membros de dimensão que você pode incluir em uma consulta para retornar dados ou metadados adicionais para uso em um aplicativo personalizado ou para ajudar na investigação ou na construção do modelo. Se você estiver usando as ferramentas de cliente do SQL Server, poderá exibir propriedades intrínsecas no SQL Server Management Studio (SSMS).  
  
 As propriedades intrínsecas incluem **ID**, **KEY**, **KEYx**e **NAME**, que são propriedades expostas por cada membro, em qualquer nível. Você também pode retornar informações de posição, como **LEVEL_NUMBER** ou **PARENT_UNIQUE_NAME**, entre outros.  
  
 Dependendo de como você cria a consulta e no aplicativo cliente que você está usando para executar consultas, as propriedades do membro podem ou não ser visíveis no conjunto de resultados. Se você estiver usando o SQL Server Management Studio para testar ou executar consultas, poderá clicar duas vezes em um membro no conjunto de resultados para abrir a caixa de diálogo Propriedades do Membro, mostrando os valores para cada propriedade intrínseca do membro.  
  
 Para obter uma introdução sobre como usar e exibir propriedades do membro de dimensão, consulte [Exibindo propriedades do membro do SSAS dentro de uma janela de consulta MDX no SSMS](http://go.microsoft.com/fwlink/?LinkId=317362).  
  
> [!NOTE]
>  Como um provedor compatível com a seção OLAP da especificação OLE DB com data de março de 1999 (2.6), o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] dá suporte a propriedades intrínsecas do membro listadas neste tópico.  
> 
>  Provedores diferentes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] podem dar suporte a outras propriedades intrínsecas do membro. Para obter mais informações sobre as propriedades intrínsecas do membro que têm suporte por outros provedores, consulte a documentação fornecida com esses provedores.  
  
## <a name="types-of-member-properties"></a>Tipos de propriedades do membro  
 As propriedades intrínsecas do membro com suporte pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] são de dois tipos:  
  
 Propriedades do membro sensíveis ao contexto  
 Essas propriedades do membro devem ser usadas no contexto de uma hierarquia ou nível específico, e fornecem valores para cada membro da dimensão ou nível especificado.  
  
 Observe como o exemplo a seguir inclui o caminho da propriedade **KEY** : `MEMBER [Measures].[Parent Member Key] AS [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("KEY")`.  
  
 Propriedades do membro não sensíveis ao contexto  
 Essas propriedades do membro não podem ser usadas no contexto de uma dimensão ou nível específico, e retornar valores para todos os membros em um eixo.  
  
 As propriedades que não são sensíveis a contexto são autônomas e não incluem informações de caminho. Observe como não há nenhuma dimensão ou nível especificado para **PARENT_UNIQUE_NAME** no exemplo a seguir: `DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS`  
  
 Independentemente da propriedade intrínseca do membro ser sensível ou não ao contexto, as regras de uso a seguir são aplicáveis:  
  
-   Você pode especificar somente as propriedades intrínsecas do membro relacionadas a membros de dimensão projetados no eixo.  
  
-   Você pode combinar solicitações de propriedades do membro sensíveis ao contexto na mesma consulta com propriedades intrínsecas do membro não sensíveis ao contexto.  
  
-   Você usa a palavra-chave **PROPERTIES** para consultar as propriedades.  
  
 As seções a seguir descrevem as duas propriedades intrínsecas do membro sensíveis e não sensíveis ao contexto disponíveis no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], e como usar a palavra-chave **PROPERTIES** com cada tipo de propriedade.  
  
## <a name="context-sensitive-member-properties"></a>Propriedades do membro sensíveis ao contexto  
 Todos os membros de dimensão e membros de nível têm suporte a uma lista de propriedades intrínsecas do membro são sensíveis ao contexto. A tabela a seguir lista essas propriedades sensíveis ao contexto.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**ID**|A ID mantida internamente para o membro.|  
|**Key**|O valor da chave de membro no tipo de dados original. MEMBER_KEY é para compatibilidade com versões anteriores.  MEMBER_KEY tem o mesmo valor que KEY0 para chaves não compostas e a propriedade MEMBER_KEY é nula para chaves compostas.|  
|**KEYx**|A chave para o membro, onde x é o valor ordinal com base em zero da chave. KEY0 está disponível para chaves compostas e não compostas, mas primariamente usado para chaves compostas.<br /><br /> Para chaves compostas, KEY0, KEY1, KEY2 e assim por diante, formam coletivamente a chave composta. Você pode usar cada uma independentemente em uma consulta para retornar essa parte da chave composta. Por exemplo, especificar KEY0 retorna a primeira parte da chave composta, especificar KEY1 retorna a parte seguinte da chave composta e assim por diante.<br /><br /> Se a chave for não composta, KEY0 será equivalente a **Key**.<br /><br /> Observe que **KEYx** pode ser usado no contexto assim como sem contexto. Por esse motivo, ela é exibida em ambas as listas.<br /><br /> Para obter um exemplo de como usar essa propriedade de membro, consulte [uma notícia simples do MDX: Key0, Key1, Key2](http://go.microsoft.com/fwlink/?LinkId=317364).|  
|**Nome**|O nome do membro.|  
  
### <a name="properties-syntax-for-context-sensitive-properties"></a>Sintaxe PROPERTIES para propriedades sensíveis ao contexto  
 Você usa essas propriedades do membro no contexto de uma dimensão ou nível específico, e fornece valores para cada membro da dimensão ou nível especificado.  
  
 Para propriedades de dimensão do membro, você precede o nome da propriedade com o nome da dimensão à qual a propriedade se aplica. O exemplo a seguir mostra a sintaxe apropriada:  
  
 `DIMENSION PROPERTIES Dimension.Property_name`  
  
 Para uma propriedade de membro de nível, você pode preceder o nome da propriedade somente com o nome do nível ou, para especificação adicional, o nome da dimensão e do nível. O exemplo a seguir mostra a sintaxe apropriada:  
  
 `DIMENSION PROPERTIES [Dimension.]Level.Property_name`  
  
 Para ilustrar, você gostaria de retornar todos os nomes de cada membro referenciado na dimensão `[Sales]` . Para retornar esses nomes, você usaria a seguinte instrução em uma consulta MDX (Multidimensional Expressions):  
  
 `DIMENSION PROPERTIES [Sales].Name`  
  
## <a name="non-context-sensitive-member-properties"></a>Propriedades do membro não sensíveis ao contexto  
 Todos os membros dão suporte a uma lista de propriedades intrínsecas do membro que são as mesmas, independentemente do contexto. Essas propriedades fornecem informações adicionais que podem ser usadas por aplicativos para aprimorar a experiência do usuário.  
  
 A tabela a seguir lista as propriedades intrínsecas não sensíveis ao contexto com suporte pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Colunas no conjunto de linhas de esquema MEMBERS suportam as propriedades intrínsecas do membro listadas na seguinte tabela. Para obter mais informações sobre o conjunto de linhas do esquema **MEMBERS** , consulte [Conjunto de linhas MDSCHEMA_MEMBERS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-members-rowset).  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**CATALOG_NAME**|O nome do cubo ao qual este membro pertence.|  
|**CHILDREN_CARDINALITY**|O número de filhos de um membro. Isso pode ser uma estimativa, portanto, você não deve confiar nisso como sendo a contagem exata. Os provedores devem retornar a melhor estimativa possível.|  
|**CUSTOM_ROLLUP**|A expressão de membro personalizado.|  
|**CUSTOM_ROLLUP_PROPERTIES**|As propriedades de membro personalizado.|  
|**DESCRIPTION**|Uma descrição legível do membro.|  
|**DIMENSION_UNIQUE_NAME**|O nome exclusivo da dimensão à qual este membro pertence. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|**HIERARCHY_UNIQUE_NAME**|O nome exclusivo da hierarquia. Se o membro pertencer a mais de uma hierarquia, haverá uma fila para cada hierarquia à qual o membro pertence. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|**IS_DATAMEMBER**|Um booliano que indica se o membro é ou não um membro de dados.|  
|**IS_PLACEHOLDERMEMBER**|Um booliano que indica se o membro é ou não um espaço reservado.|  
|**KEYx**|A chave para o membro, onde x é o valor ordinal com base em zero da chave. KEY0 está disponível para chaves compostas e não compostas.<br /><br /> Se a chave for não composta, KEY0 será equivalente a **Key**.<br /><br /> Para chaves compostas, KEY0, KEY1, KEY2 e assim por diante, formam coletivamente a chave composta. Você pode fazer referência a cada uma independentemente em uma consulta para retornar essa parte da chave composta. Por exemplo, especificar KEY0 retorna a primeira parte da chave composta, especificar KEY1 retorna a parte seguinte da chave composta e assim por diante.<br /><br /> Observe que **KEYx** pode ser usado no contexto assim como sem contexto. Por esse motivo, ela é exibida em ambas as listas.<br /><br /> Para obter um exemplo de como usar essa propriedade de membro, consulte [uma notícia simples do MDX: Key0, Key1, Key2](http://go.microsoft.com/fwlink/?LinkId=317364).|  
|**LCID** *x*|A conversão da legenda do membro no valor hexadecimal da identificação de localidade, em que *x* é o valor decimal da identificação de localidade (por exemplo, LCID1009 como Inglês – Canadá). Isso somente estará disponível se a conversão tiver a coluna da legenda associada à fonte de dados.|  
|**LEVEL_NUMBER**|A distância do membro para a raiz da hierarquia. O nível raiz é zero.|  
|**LEVEL_UNIQUE_NAME**|O nome exclusivo do nível ao qual o membro pertence. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|**MEMBER_CAPTION**|Um rótulo ou legenda associado ao membro. A legenda serve basicamente para fins de exibição. Se uma legenda não existir, a consulta retornará **MEMBER_NAME**.|  
|**MEMBER_KEY**|O valor da chave de membro no tipo de dados original. MEMBER_KEY é para compatibilidade com versões anteriores.  MEMBER_KEY tem o mesmo valor que KEY0 para chaves não compostas e a propriedade MEMBER_KEY é nula para chaves compostas.|  
|**MEMBER_NAME**|O nome do membro.|  
|**MEMBER_TYPE**|O tipo do membro. Essa propriedade pode ter um dos seguintes valores:<br /><br /> **MDMEMBER_TYPE_REGULAR**<br /><br /> **MDMEMBER_TYPE_ALL**<br /><br /> **MDMEMBER_TYPE_FORMULA**<br /><br /> **MDMEMBER_TYPE_MEASURE**<br /><br /> **MDMEMBER_TYPE_UNKNOWN**<br /><br /> <br /><br /> Observação: MDMEMBER_TYPE_FORMULA tem prioridade sobre MDMEMBER_TYPE_MEASURE. Portanto, se houver um membro de fórmula (calculado) na dimensão Medidas, a propriedade **MEMBER_TYPE** para o membro calculado será MDMEMBER_TYPE_FORMULA.|  
|**MEMBER_UNIQUE_NAME**|O nome exclusivo do membro. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|**MEMBER_VALUE**|O valor do membro no tipo original.|  
|**PARENT_COUNT**|O número de pais deste membro.|  
|**PARENT_LEVEL**|A distância do pai do membro para o nível raiz da hierarquia. O nível raiz é zero.|  
|**PARENT_UNIQUE_NAME**|O nome exclusivo do pai do membro. **NULL** é retornado para qualquer membro no nível raiz. Para provedores que geram nomes exclusivos por qualificação, cada componente desse nome é delimitado.|  
|**SKIPPED_LEVELS**|O número de níveis ignorados do membro.|  
|**UNARY_OPERATOR**|O operador unário do membro.|  
|**UNIQUE_NAME**|O nome totalmente qualificado do membro, neste formato: [dimensão].[nível].[key6.]|  
  
### <a name="properties-syntax-for-non-context-sensitive-properties"></a>Sintaxe PROPERTIES para propriedades não sensíveis ao contexto  
 Use a sintaxe a seguir para especificar uma propriedade intrínseca, não sensível ao contexto do membro usando a palavra-chave **PROPERTIES** :  
  
 `DIMENSION PROPERTIES Property`  
  
 Note que esta sintaxe não permite qualificar a propriedade por uma dimensão ou nível. A propriedade não pode ser qualificada porque uma propriedade intrínseca do membro não sensível ao contexto se aplica a todos os membros de um eixo.  
  
 Por exemplo, uma instrução MDX que especifica a propriedade intrínseca do membro **DESCRIPTION** teria a seguinte sintaxe:  
  
 `DIMENSION PROPERTIES DESCRIPTION`  
  
 Esta instrução retorna a descrição de cada membro na dimensão do eixo. Se você tentasse qualificar a propriedade com uma dimensão ou um nível, como em *Dimensão*`.DESCRIPTION` ou *Nível*`.DESCRIPTION`, não seria possível validar a instrução.  
  
### <a name="example"></a>Exemplo  
 Os exemplos a seguir mostram as consultas MDX que retornam propriedades intrínsecas.  
  
 **Exemplo 1: Use as propriedades intrínsecas sensíveis ao contexto na consulta**  
  
 O exemplo a seguir retorna a ID pai, a chave e o nome de cada categoria de produto. Observe como as propriedades são expostas como medidas. Isso permite que você exiba as propriedades em um conjunto de células quando você executa a consulta, em vez da caixa de diálogo Propriedades do Membro no SSMS. Você pode executar uma consulta como essa para recuperar os metadados do membro de um cubo que já foi implantado.  
  
```  
WITH  
MEMBER [Measures].[Parent Member ID] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("ID")  
MEMBER [Measures].[Parent Member Key] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("KEY")  
MEMBER [Measures].[Parent Member Name] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("Name")  
SELECT  
 {[Measures].[Parent Member ID], [Measures].[Parent Member Key], [Measures].[Parent Member Name] } on COLUMNS,   
 [Product].[Product Categories].AllMembers on ROWS  
FROM [Adventure Works]  
```  
  
 **Exemplo 2: Propriedades de intrínsecas sensíveis ao contexto não**  
  
 O exemplo a seguir é uma lista completa de propriedades intrínsecas não sensíveis ao contexto. Depois de executar a consulta no SSMS, clique em membros individuais para exibir propriedades na caixa de diálogo Propriedades do Membro.  
  
```  
SELECT [Measures].[Sales Amount Quota] on COLUMNS,  
[Employee].[Employees].members  
DIMENSION PROPERTIES  
 CATALOG_NAME ,   
 CHILDREN_CARDINALITY ,  
 CUSTOM_ROLLUP ,   
 CUSTOM_ROLLUP_PROPERTIES ,   
 DESCRIPTION ,   
 DIMENSION_UNIQUE_NAME ,   
 HIERARCHY_UNIQUE_NAME ,  
 IS_DATAMEMBER ,   
 IS_PLACEHOLDERMEMBER ,   
 KEY0 ,  
 LCID ,  
 LEVEL_NUMBER ,  
 LEVEL_UNIQUE_NAME ,  
 MEMBER_CAPTION ,   
 MEMBER_KEY ,   
 MEMBER_NAME ,   
 MEMBER_TYPE ,  
 MEMBER_UNIQUE_NAME ,   
 MEMBER_VALUE ,   
 PARENT_COUNT ,   
 PARENT_LEVEL ,   
 PARENT_UNIQUE_NAME ,  
 SKIPPED_LEVELS ,   
 UNARY_OPERATOR ,   
 UNIQUE_NAME    
 ON ROWS  
FROM [Adventure Works]  
WHERE [Employee].[Employee Department].[Department].&[Sales]  
```  
  
 **Exemplo 3: Retornar propriedades do membro como dados em um conjunto de resultados**  
  
 O exemplo a seguir retorna a legenda convertida para o membro de categoria de produto na dimensão Produto no cubo Adventure Works para localidades especificadas.  
  
```  
WITH   
MEMBER Measures.CategoryCaption AS Product.Category.CurrentMember.MEMBER_CAPTION  
MEMBER Measures.SpanishCategoryCaption AS Product.Category.CurrentMember.Properties("LCID3082")  
MEMBER Measures.FrenchCategoryCaption AS Product.Category.CurrentMember.Properties("LCID1036")  
SELECT   
{ Measures.CategoryCaption, Measures.SpanishCategoryCaption, Measures.FrenchCategoryCaption } ON 0  
,[Product].[Category].MEMBERS ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [PeriodsToDate &#40;MDX&#41;](../../../mdx/periodstodate-mdx.md)   
 [Children &#40;MDX&#41;](../../../mdx/children-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../../../mdx/hierarchize-mdx.md)   
 [Count &#40;Set&#41; &#40;MDX&#41;](../../../mdx/count-set-mdx.md)   
 [Filter &#40;MDX&#41;](../../../mdx/filter-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../../../mdx/drilldownlevel-mdx.md)   
 [Properties &#40;MDX&#41;](../../../mdx/properties-mdx.md)   
 [PrevMember &#40;MDX&#41;](../../../mdx/prevmember-mdx.md)   
 [Usando propriedades do membro &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [Referência da Função MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
