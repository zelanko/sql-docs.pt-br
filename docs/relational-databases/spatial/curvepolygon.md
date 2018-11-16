---
title: CurvePolygon | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e000a1d8-a049-4542-bfeb-943fd6ab3969
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 10532564d2310ad3b8eaf28c2693bafb423d81a2
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51658833"
---
# <a name="curvepolygon"></a>CurvePolygon
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **CurvePolygon** é uma superfície topologicamente fechada definida por um anel delimitador exterior e zero ou mais anéis interiores  
  
> [!IMPORTANT]  
>  Para obter uma descrição detalhada e exemplos dos recursos espaciais introduzidos no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], incluindo o subtipo **CurvePolygon** , baixe o white paper sobre [Novos recursos espaciais no SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407).  
  
 Os critérios a seguir definem os atributos de uma instância **CurvePolygon** :  
  
-   O limite da instância **CurvePolygon** é definido pelo anel exterior e por todos os anéis interiores.  
  
-   O interior da instância **CurvePolygon** é o espaço entre o anel exterior e todos os anéis interiores.  
  
 Uma instância **CurvePolygon** é diferente de uma instância **Polygon** porque uma instância **CurvePolygon** pode conter os seguintes segmentos de arco circular: **CircularString** e **CompoundCurve**.  
  
## <a name="compoundcurve-instances"></a>Instâncias CompoundCurve  
 A ilustração a seguir mostra figuras de **CurvePolygon** válidas:  
  
### <a name="accepted-instances"></a>Instâncias aceitas  
 Para uma instância **CurvePolygon** ser aceita, ela precisa estar vazia ou conter apenas anéis de arco circular que sejam aceitos. Um anel de arco circular aceito atende aos requisitos a seguir.  
  
1.  É uma instância **LineString**, **CircularString**ou **CompoundCurve** aceita. Para obter mais informações sobre instâncias aceitas, consulte [LineString](../../relational-databases/spatial/linestring.md), [CircularString](../../relational-databases/spatial/circularstring.md)e [CompoundCurve](../../relational-databases/spatial/compoundcurve.md).  
  
2.  Tem pelo menos quatro pontos.  
  
3.  O ponto inicial e o ponto de extremidade têm as mesmas coordenadas de X e Y.  
  
    > [!NOTE]  
    >  Os valores de Z e M são ignorados.  
  
 O exemplo a seguir mostra instâncias **CurvePolygon** aceitas.  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON EMPTY';  
DECLARE @g2 geometry = 'CURVEPOLYGON((0 0, 0 0, 0 0, 0 0))';  
DECLARE @g3 geometry = 'CURVEPOLYGON((0 0 1, 0 0 2, 0 0 3, 0 0 3))'  
DECLARE @g4 geometry = 'CURVEPOLYGON(CIRCULARSTRING(1 3, 3 5, 4 7, 7 3, 1 3))';  
DECLARE @g5 geography = 'CURVEPOLYGON((-122.3 47, 122.3 -47, 125.7 -49, 121 -38, -122.3 47))';  
```  
  
 `@g3` é aceito, embora os pontos inicial e de extremidade tenham valores de Z diferentes, pois esses valores são ignorados. `@g5` é aceito, embora a instância de tipo **geography** não seja válida.  
  
 Os exemplos a seguir geram um `System.FormatException`.  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON((0 5, 0 0, 0 0, 0 0))';  
DECLARE @g2 geometry = 'CURVEPOLYGON((0 0, 0 0, 0 0))';  
```  
  
 `@g1` não é aceito porque os pontos inicial e de extremidade não têm o mesmo valor de Y. `@g2` não é aceito porque o anel não contém pontos suficientes.  
  
### <a name="valid-instances"></a>Instâncias válidas  
 Para que uma instância **CurvePolygon** seja válida, os anéis exterior e interior devem atender aos seguintes critérios:  
  
1.  Eles podem tocar apenas em pontos tangentes únicos.  
  
2.  Eles não podem se cruzar.  
  
3.  Cada anel deve conter pelo menos quatro pontos.  
  
4.  Cada anel deve ser um tipo de curva aceitável.  
  
 As instâncias**CurvePolygon** também deverão atender a critérios específicos se fouem tipos de dados **geometry** ou **geography** .  
  
#### <a name="geometry-data-type"></a>Tipo de dados geometry  
 Uma instância **geometryCurvePolygon** válida deve ter os seguintes atributos:  
  
1.  Todos os anéis interiores devem estar dentro do anel exterior.  
  
2.  Pode ter vários anéis interiores, mas um anel interior não pode conter outro anel interior.  
  
3.  Nenhum anel pode cruzar com outro anel ou com si próprio.  
  
4.  Os anéis podem tocar apenas pontos tangentes únicos (o número de pontos onde os anéis tocam deve ser finito).  
  
5.  O interior do polígono deve estar conectado.  
  
 O exemplo a seguir mostra uma instância **geometryCurvePolygon** válida.  
  
```  
DECLARE @g1 geometry = 'CURVEPOLYGON EMPTY';  
DECLARE @g2 geometry = 'CURVEPOLYGON(CIRCULARSTRING(1 3, 3 5, 4 7, 7 3, 1 3))';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
 As instâncias CurvePolygon têm as mesmas regras de validade que as instâncias Polygon, com exceção de que as instâncias CurvePolygon podem aceitar os novos tipos de segmento de arco circular. Para obter mais exemplos de instâncias válidas ou não válidas, consulte [Polygon](../../relational-databases/spatial/polygon.md).  
  
#### <a name="geography-data-type"></a>Tipo de dados geography  
 Uma instância **geographyCurvePolygon** válida deve ter os seguintes atributos:  
  
1.  O interior do polígono é conectado usando a regra do lado esquerdo.  
  
2.  Nenhum anel pode cruzar com outro anel ou com si próprio.  
  
3.  Os anéis podem tocar apenas pontos tangentes únicos (o número de pontos onde os anéis tocam deve ser finito).  
  
4.  O interior do polígono deve estar conectado.  
  
 O exemplo a seguir mostra uma instância CurvePolygon de geography válida.  
  
```  
DECLARE @g geography = 'CURVEPOLYGON((-122.3 47, 122.3 47, 125.7 49, 121 38, -122.3 47))';  
SELECT @g.STIsValid();  
```  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-curvepolygon"></a>A. Criando uma instância geométrica com um CurvePolygon vazio  
 Esse exemplo mostra como criar uma instância **CurvePolygon** vazia:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON EMPTY');  
```  
  
### <a name="b-declaring-and-instantiating-a-geometry-instance-with-a-curvepolygon-in-the-same-statement"></a>B. Declarando e criando uma instância geométrica com um CurvePolygon na mesma instrução  
 Este snippet de código mostra como declarar e iniciar uma instância de geometry com um **CurvePolygon** na mesma instrução:  
  
```sql  
DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))'  
```  
  
### <a name="c-instantiating-a-geography-instance-with-a-curvepolygon"></a>C. Criando uma instância geográfica com um CurvePolygon  
 Este snippet de código mostra como declarar e iniciar uma instância de **geography** com um **CurvePolygon**:  
  
```sql  
DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
```  
  
### <a name="d-storing-a-curvepolygon-with-only-an-exterior-bounding-ring"></a>D. Armazenando um CurvePolygon com apenas um anel delimitador exterior  
 Este exemplo mostra como armazenar um círculo simples em uma instância **CurvePolygon** (apenas um anel delimitador exterior é usado para definir o círculo):  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))');  
SELECT @g.STArea() AS Area;  
```  
  
### <a name="e-storing-a-curvepolygon-containing-interior-rings"></a>E. Armazenando um CurvePolygon que contém anéis interiores  
 Este exemplo cria uma rosca em uma instância **CurvePolygon** (um anel delimitador exterior e um anel interior são usados para definir a rosca):  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 4, 4 0, 8 4, 4 8, 0 4), CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))');  
SELECT @g.STArea() AS Area;  
```  
  
 Este exemplo mostra uma instância **CurvePolygon** válida e uma instância inválida ao usar anéis interiores:  
  
```sql  
DECLARE @g1 geometry, @g2 geometry;  
SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 5, 5 0, 0 -5, -5 0, 0 5), (-2 2, 2 2, 2 -2, -2 -2, -2 2))');  
IF @g1.STIsValid() = 1  
  BEGIN  
     SELECT @g1.STArea();  
  END  
SET @g2 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 5, 5 0, 0 -5, -5 0, 0 5), (0 5, 5 0, 0 -5, -5 0, 0 5))');  
IF @g2.STIsValid() = 1  
  BEGIN  
     SELECT @g2.STArea();  
  END  
SELECT @g1.STIsValid() AS G1, @g2.STIsValid() AS G2;  
```  
  
 Tanto o @g1 quanto o @g2 usam o mesmo anel delimitador exterior: um círculo com um raio de 5 e ambos usam um quadrado para um anel interior.  Entretanto, a instância @g1 é válida, mas a instância @g2 é inválida.  A razão pela qual @g2 é inválida é que o anel interior divide o espaço interno limitado pelo anel exterior em quatro regiões separadas.  O desenho a seguir mostra o que ocorreu:  
  
## <a name="see-also"></a>Consulte Também  
 [Polygon](../../relational-databases/spatial/polygon.md)   
 [CircularString](../../relational-databases/spatial/circularstring.md)   
 [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)   
 [Referência de método de tipo de dados geometry](https://msdn.microsoft.com/library/d88e632b-6b2f-4466-a15f-9fbef1a347a7)   
 [Referência de método de tipo de dados geography](https://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)   
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
