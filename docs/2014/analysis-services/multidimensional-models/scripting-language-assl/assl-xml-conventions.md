---
title: ASSL convenções XML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- whitespace [Analysis Services Scripting Language]
- trailing whitespace
- XSD data types [Analysis Services Scripting Language]
- inheritance [Analysis Services Scripting Language]
- cardinality [Analysis Services Scripting Language]
- white space [Analysis Services Scripting Language]
- ASSL, XML conventions
- defaults [Analysis Services Scripting Language]
- leading whitespace
- Analysis Services Scripting Language, XML conventions
- XML [Analysis Services Scripting Language]
- hierarchies [Analysis Services Scripting Language]
- inherited defaults [Analysis Services Scripting Language]
ms.assetid: bce4edad-4420-41ce-9672-8c00c5c0dec6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 41e0a3fcf4348efcb2108a1205c1d2d8eabfb85c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62736389"
---
# <a name="assl-xml-conventions"></a>Convenções de XML do ASSL
  A ASSL (Analysis Services Scripting Language) representa a hierarquia de objetos como um conjunto de tipos de elementos, cada um definindo os elementos filhos que podem conter.  
  
 Para representar a hierarquia de objeto, a ASSL usa as seguintes convenções XML:  
  
-   Todos os objetos e propriedades são representados como elementos, exceto os atributos XML padrão, como ' XML: lang '.  
  
-   Os nomes de elemento e os valores de enumeração seguem a convenção de nomenclatura do Microsoft .NET Framework de combinação de maiúsculas e minúsculas de Pascal sem sublinhados.  
  
-   Os valores de maiúsculas e minúsculas é preservado. Os valores para enumerações também apresentam diferenciação de maiúsculas e minúsculas.  
  
 Além dessa lista de convenções, o Analysis Services segue também certas convenções relativas a cardinalidade, a herança, a espaço em branco, a tipos de dados e a valores padrão.  
  
## <a name="cardinality"></a>Cardinalidade  
 Quando um elemento tiver uma cardinalidade maior do que 1, haverá uma coleção de elementos XML que encapsula esse elemento. O nome de coleção usa a forma plural dos elementos contidos na coleção. Por exemplo, o fragmento XML a seguir representa a coleção `Dimensions` em um elemento `Database`:  
  
 `<Database>`  
  
 `...`  
  
 `<Dimensions>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `...`  
  
 `</Dimension>`  
  
 `</Dimensions>`  
  
 `</Database>`  
  
 ``  
  
 A ordem na qual os elementos aparecem não tem importância.  
  
## <a name="inheritance"></a>Herança  
 A herança é usada quando existem objetos distintos com sobrepostos mas significativamente diferentes de propriedades. Exemplos desses objetos sobrepostos mas distintos são cubos virtuais, cubos vinculados e cubos normais. Para objetos sobrepostos mas distintos, o Analysis Services usa o atributo `type` padrão do Namespace da Instância XML para indicar a herança. Por exemplo, o fragmento XML a seguir mostra como o atributo `type` identifica se um elemento `Cube` herda de um cubo normal ou de um cubo virtual:  
  
 `<Cubes>`  
  
 `<Cube xsi:type="RegularCube">`  
  
 `<Name>Sales</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `<Cube xsi:type="VirtualCube">`  
  
 `<Name>SalesAndInventory</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `</Cubes>`  
  
 ``  
  
 Geralmente, a herança não é usada quando vários tipos têm uma propriedade com o mesmo nome. Por exemplo, as propriedades `Name` e `ID` aparecem em muitos elementos, mas não foram elevadas a um tipo abstrato.  
  
## <a name="whitespace"></a>Espaço em branco  
 O espaço em branco dentro de um valor de elemento é preservado. No entanto, os espaços em branco inicial e final são sempre retirados. Por exemplo, os elementos a seguir contêm o mesmo texto mas quantidades diferentes de espaços em branco no texto e, portanto, são tratados como se tivessem valores diferentes:  
  
 `<Description>My text<Description>`  
  
 `<Description>My  text<Description>`  
  
 ``  
  
 Entretanto, os elementos a seguir só variam nos espaços em branco inicial e final e, portanto, serão tratados como se tivessem valores equivalentes:  
  
 `<Description>My text<Description>`  
  
 `<Description>  My text  <Description>`  
  
 ``  
  
## <a name="data-types"></a>Tipos de dados  
 O Analysis Services usa os seguintes tipos de dados XSD (linguagem de definição de esquema XML) padrão:  
  
 `Int`  
 Um valor inteiro no intervalo de-231 a 231-1.  
  
 `Long`  
 Um valor inteiro no intervalo de-263 a 263-1.  
  
 `String`  
 Um valor de cadeia de caracteres em conformidade com as seguintes regras globais:  
  
-   Os caracteres de controle são retirados.  
  
-   Os espaços em branco inicial e final são retirados.  
  
-   O espaço em branco interno é preservado.  
  
 As propriedades `Name` e `ID` têm limitações especiais de caracteres válidos em elementos de cadeia de caracteres. Para obter informações adicionais `Name` sobre `ID` convenções e, consulte [objetos e características do objeto ASSL](assl-objects-and-object-characteristics.md).  
  
 `DateTime`  
 Uma `DateTime` estrutura da .NET Framework. Um valor `DateTime` não pode ser NULL. A data mais antiga suportada pelo tipo de dados `DataTime` é 1º de janeiro de 1601, disponível a programadores como `DateTime.MinValue`. A data mais antiga suportada indica que um valor `DateTime` está ausente.  
  
 `Boolean`  
 Uma enumeração só com dois valores, como {verdadeiro, falso} ou {0, 1}.  
  
## <a name="default-values"></a>Valores padrão  
 O Analysis Services usa os padrões listados na tabela seguinte.  
  
|Tipo de dados XML|Valor padrão|  
|-------------------|-------------------|  
|`Boolean`|Falso|  
|`String`|"" (cadeia de caracteres vazia)|  
|`Integer` ou `Long`|0 (zero)|  
|`Timestamp`|12:00:00 AM, 1/1/0001 (correspondente a um .NET Framework `System.DateTime` com 0 tiques)|  
  
 Um elemento que está presente mas vazio será interpretado como tendo um valor de uma cadeia de caracteres nula, e não como o valor padrão.  
  
### <a name="inherited-defaults"></a>Padrões herdados  
 Algumas propriedades especificadas em um objeto fornecem valores padrão para a mesma propriedade em objetos filhos ou descendentes. Por exemplo, `Cube.StorageMode` fornece o valor padrão para `Partition.StorageMode`. As regras que o Analysis Services aplica para valores padrão herdados são as seguintes:  
  
-   Quando a propriedade do objeto filho for nula no XML, o padrão do seu valor será o valor herdado. No entanto, se você consultar o valor a partir do servidor, este retornará o valor nulo do elemento XML.  
  
-   Não é possível determinar programaticamente se a propriedade ou objeto filho foi definida corretamente no objeto filho ou herdado.  
  
 Alguns elementos definiram padrões que se aplicarão quando o elemento estiver ausente. Por exemplo, os elementos `Dimension` do fragmento XML a seguir são equivalentes, mesmo se um elemento `Dimension` contiver um elemento `Visible` e se o outro elemento `Dimension` não.  
  
 `<Dimension>`  
  
 `<Name>Product</Name>`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `<Name>Product</ Name>`  
  
 `<Visible>true</Visible>`  
  
 `</Dimension>`  
  
 Para obter mais informações sobre padrões herdados, consulte [objetos ASSL e características de objeto](assl-objects-and-object-characteristics.md).  
  
  
