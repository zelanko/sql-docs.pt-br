---
title: CompoundCurve | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: ae357f9b-e3e2-4cdf-af02-012acda2e466
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 48d1ca9458b4993ad509cc2bbedd8d23b127918c
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688677"
---
# <a name="compoundcurve"></a>CompoundCurve
  Uma `CompoundCurve` é uma coleção de zero ou mais `CircularString` contínua ou `LineString` instâncias de tipos geometry ou geography.  
  
> [!IMPORTANT]  
>  Para obter uma descrição detalhada e exemplos dos novos recursos espaciais nesta versão, incluindo o subtipo `CompoundCurve`, baixe o white paper, [novos recursos espaciais no SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407).  
  
 Uma instância de `CompoundCurve` vazia pode ser instanciada, mas para que uma `CompoundCurve` seja válida, ela deve atender aos seguintes critérios:  
  
1.  Ele deve conter pelo menos uma `CircularString` ou `LineString` instância.  
  
2.  A sequência de instâncias de `CircularString` ou `LineString` deve ser contínua.  
  
 Se um `CompoundCurve` contiver uma sequência de várias instâncias de `CircularString` e `LineString`, o ponto de extremidade final para cada instância, exceto para a última instância, deverá ser o ponto de extremidade inicial para a próxima instância na sequência. Isso significa que, se o ponto final de uma instância anterior na sequência for (4 3 7 2), o ponto de partida para a próxima instância na sequência deverá ser (4 3 7 2). Observe que os valores Z (elevação) e M (medida) para o ponto também devem ser iguais. Se houver uma diferença nos dois pontos, um `System.FormatException` será lançado. Os pontos em um `CircularString` não precisam ter um valor Z ou M. Se nenhum valor Z ou M for fornecido para o ponto final da instância anterior, o ponto inicial da próxima instância não poderá incluir valores Z ou M. Se o ponto final da sequência anterior for (4 3), o ponto de partida para a próxima sequência deverá ser (4 3); Ele não pode ser (4 3 7 2). Todos os pontos em uma instância de `CompoundCurve` não devem ter um valor Z ou o mesmo valor Z.  
  
## <a name="compoundcurve-instances"></a>Instâncias de CompoundCurve  
 A ilustração a seguir mostra os tipos de `CompoundCurve` válidos.  
  
 ![](../../database-engine/media/f278742e-b861-4555-8b51-3d972b7602bf.png "f278742e-b861-4555-8b51-3d972b7602bf")  
  
### <a name="accepted-instances"></a>Instâncias aceitas  
 `CompoundCurve` instância será aceita se for uma instância vazia ou atender aos critérios a seguir.  
  
1.  Todas as instâncias contidas pela instância `CompoundCurve` são aceitas instâncias de segmento de arco circular. Para obter mais informações sobre instâncias de segmento de arco circular aceitas, consulte [LineString](linestring.md) e [circularstring](circularstring.md).  
  
2.  Todos os segmentos de arco circular na instância de `CompoundCurve` estão conectados. O primeiro ponto para cada segmento de arco circular com sucesso é o mesmo que o último ponto no segmento de arco circular anterior.  
  
    > [!NOTE]  
    >  Isso inclui as coordenadas Z e M. Portanto, todas as quatro coordenadas X, Y, Z e M devem ser as mesmas.  
  
3.  Nenhuma das instâncias contidas são instâncias vazias.  
  
 O exemplo a seguir mostra as instâncias de `CompoundCurve` aceitas.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE EMPTY';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (-1 0, 2 0))';  
```  
  
 O exemplo a seguir mostra `CompoundCurve` instâncias que não são aceitas. Essas instâncias geram `System.FormatException`.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE(CIRCULARSTRING EMPTY)';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (1 0, 2 0))';  
```  
  
### <a name="valid-instances"></a>Instâncias válidas  
 Uma instância de `CompoundCurve` será válida se atender aos critérios a seguir.  
  
1.  A instância de `CompoundCurve` é aceita.  
  
2.  Todas as instâncias de segmento de arco circular contidas na instância de `CompoundCurve` são instâncias válidas.  
  
 O exemplo a seguir mostra instâncias de `CompoundCurve` válidas.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE EMPTY';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (-1 0, 2 0))';  
DECLARE @g3 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 1 1, 1 1), (1 1, 3 5, 5 4))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
  
```  
  
 `@g3` é válido porque a instância de `CircularString` é válida. Para obter mais informações sobre a validade da instância de `CircularString`, consulte [circularstring](circularstring.md).  
  
 O exemplo a seguir mostra `CompoundCurve` instâncias que não são válidas.  
  
```  
DECLARE @g1 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 1 1, 1 1), (1 1, 3 5, 5 4, 3 5))';  
DECLARE @g2 geometry = 'COMPOUNDCURVE((1 1, 1 1))';  
DECLARE @g3 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 2 3, 1 1))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g1` não é válido porque a segunda instância não é uma instância de LineString válida. `@g2` não é válido porque a instância de `LineString` não é válida. `@g3` não é válido porque a instância de `CircularString` não é válida. Para obter mais informações sobre instâncias válidas de `CircularString` e `LineString`, consulte [circularstring](circularstring.md) e [LineString](linestring.md).  
  
## <a name="examples"></a>Disso  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-compooundcurve"></a>um. Instanciando uma instância de geometry com um Compoundcurve vazio  
 O exemplo a seguir mostra como criar uma instância de `CompoundCurve` vazia:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE EMPTY');  
```  
  
### <a name="b-declaring-and-instantiating-a-geometry-instance-using-a-compoundcurve-in-the-same-statement"></a>b. Declarando e instanciando uma instância de geometry usando um CompoundCurve na mesma instrução  
 O exemplo a seguir mostra como declarar e inicializar uma instância de `geometry` com uma `CompoundCurve`in mesma instrução:  
  
```sql  
DECLARE @g geometry = 'COMPOUNDCURVE ((2 2, 0 0),CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';  
```  
  
### <a name="c-instantiating-a-geography-instance-with-a-compoundcurve"></a>&. Instanciando uma instância de geography com um CompoundCurve  
 O exemplo a seguir mostra como declarar e inicializar uma instância de `geography` com um `CompoundCurve`:  
  
```sql  
DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
```  
  
### <a name="d-storing-a-square-in-a-compoundcurve-instance"></a>D. Armazenando um quadrado em uma instância de CompoundCurve  
 O exemplo a seguir usa duas maneiras diferentes de usar uma instância de `CompoundCurve` para armazenar um quadrado.  
  
```sql  
DECLARE @g1 geometry, @g2 geometry;  
SET @g1 = geometry::Parse('COMPOUNDCURVE((1 1, 1 3), (1 3, 3 3),(3 3, 3 1), (3 1, 1 1))');  
SET @g2 = geometry::Parse('COMPOUNDCURVE((1 1, 1 3, 3 3, 3 1, 1 1))');  
SELECT @g1.STLength(), @g2.STLength();  
```  
  
 Os comprimentos para `@g1` e `@g2` são os mesmos. Observe que, no exemplo, uma instância de `CompoundCurve` pode armazenar uma ou mais instâncias de `LineString`.  
  
### <a name="e-instantiating-a-geometry-instance-using-a-compoundcurve-with-multiple-circularstrings"></a>Oriental. Instanciar uma instância de geometry usando um CompoundCurve com vários CircularStrings  
 O exemplo a seguir mostra como usar duas instâncias diferentes de `CircularString` para inicializar um `CompoundCurve`.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), CIRCULARSTRING(4 2, 2 4, 0 2))');  
SELECT @g.STLength();  
```  
  
 Isso produz a seguinte saída: 12,566370... que é o equivalente a 4&#x03c0; (4 * PI). A instância de `CompoundCurve` no exemplo armazena um círculo com um raio de 2. Os dois exemplos de código anteriores não tinham que usar um `CompoundCurve`. No primeiro exemplo, um `LineString` instância teria sido mais simples, e uma instância de `CircularString` teria sido mais simples para o segundo exemplo. No entanto, o exemplo a seguir mostra onde um `CompoundCurve` fornece uma alternativa melhor.  
  
### <a name="f-using-a-compoundcurve-to-store-a-semicircle"></a>fixo. Usando um CompoundCurve para armazenar um semicírculo  
 O exemplo a seguir usa uma instância de `CompoundCurve` para armazenar um semicírculo.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))');  
SELECT @g.STLength();  
```  
  
### <a name="g-storing-multiple-circularstring-and-linestring-instances-in-a-compoundcurve"></a>m. Armazenando várias instâncias Circularstring e LineString em um CompoundCurve  
 O exemplo a seguir mostra como várias instâncias de `CircularString` e `LineString` podem ser armazenadas usando uma `CompoundCurve`.  
  
```sql  
DECLARE @g geometry  
SET @g = geometry::Parse('COMPOUNDCURVE((3 5, 3 3), CIRCULARSTRING(3 3, 5 1, 7 3), (7 3, 7 5), CIRCULARSTRING(7 5, 5 7, 3 5))');  
SELECT @g.STLength();  
```  
  
### <a name="h-storing-instances-with-z-and-m-values"></a>H. Armazenando instâncias com valores Z e M  
 O exemplo a seguir mostra como usar uma instância de `CompoundCurve` para armazenar uma sequência de `CircularString` e `LineString` instâncias com valores Z e M.  
  
```sql  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(7 5 4 2, 5 7 4 2, 3 5 4 2), (3 5 4 2, 8 7 4 2))');  
```  
  
### <a name="i-illustrating-why-circularstring-instances-must-be-explicitly-declared"></a>Encontrei. Ilustrando por que instâncias Circularstring devem ser declaradas explicitamente  
 O exemplo a seguir mostra por que `CircularString` instâncias devem ser declaradas explicitamente. O programador está tentando armazenar um círculo em uma instância de `CompoundCurve`.  
  
```sql  
DECLARE @g1 geometry;    
DECLARE @g2 geometry;  
SET @g1 = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 2 4, 0 2))');  
SELECT 'Circle One', @g1.STLength() AS Perimeter;  -- gives an inaccurate amount  
SET @g2 = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), CIRCULARSTRING(4 2, 2 4, 0 2))');  
SELECT 'Circle Two', @g2.STLength() AS Perimeter;  -- now we get an accurate amount  
```  
  
 A saída é a seguinte:  
  
```  
Circle One11.940039...  
Circle Two12.566370...  
```  
  
 O perímetro para o círculo dois é de&#x03c0; aproximadamente 4 (4 * PI), que é o valor real para o perímetro. No entanto, o perímetro do círculo um é significativamente impreciso. A instância de `CompoundCurve` do círculo um armazena um segmento de arco circular (ABC) e dois segmentos de linha (CD, DA). A instância de `CompoundCurve` precisa armazenar dois segmentos de arco circular (ABC, CDA) para definir um círculo. Uma instância de `LineString` define o segundo conjunto de pontos (4 2, 2 4, 0 2) na instância de `CompoundCurve` de um círculo. Você precisa declarar explicitamente uma instância de `CircularString` dentro de um `CompoundCurve`.  
  
## <a name="see-also"></a>Consulte também  
 [Tipo&#41; de &#40;dados geometry de preisvalid](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)    
 @No__t_3 de [tipo &#40;&#41; de dados geometry de tamanho](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)  
 [Tipo&#41; de &#40;dados geometry de costartpoint](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)    
 @No__t_3 de [tipo &#40;&#41; de dados geometry de ponto de extremidade](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)  
 @No__t_1 de [LineString](linestring.md)  
 @No__t_1 [circularstring](circularstring.md)  
 [Visão geral dos tipos de dados espaciais](spatial-data-types-overview.md)    
 [Empresas](point.md)  
  
  
