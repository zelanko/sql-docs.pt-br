---
title: "Convenções de XML do ASSL | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3b7e4c800454a2e2eddac81a2420b5a6d6436c70
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="assl-xml-conventions"></a>Convenções de XML do ASSL
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
A ASSL (Analysis Services Scripting Language) representa a hierarquia de objetos como um conjunto de tipos de elementos, cada um definindo os elementos filhos que podem conter.  
  
 Para representar a hierarquia de objeto, a ASSL usa as seguintes convenções XML:  
  
-   Todos os objetos e as propriedades são representadas como elementos, com exceção de atributos XML padrão como 'xml:lang'.  
  
-   Nomes de elementos e valores de enumeração seguem a convenção de nomenclatura do Microsoft .NET Framework de Pascal sem sublinhados maiusculas e minúsculas.  
  
-   Os valores de maiúsculas e minúsculas é preservado. Os valores para enumerações também apresentam diferenciação de maiúsculas e minúsculas.  
  
 Além dessa lista de convenções, o Analysis Services segue também certas convenções relativas a cardinalidade, a herança, a espaço em branco, a tipos de dados e a valores padrão.  
  
## <a name="cardinality"></a>Cardinalidade  
 Quando um elemento tiver uma cardinalidade maior do que 1, haverá uma coleção de elementos XML que encapsula esse elemento. O nome de coleção usa a forma plural dos elementos contidos na coleção. Por exemplo, o fragmento XML a seguir representa o **dimensões** coleção dentro de um **banco de dados** elemento:  
  
 `<Database>`  
  
 `…`  
  
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
 A herança é usada quando existem objetos distintos com sobrepostos mas significativamente diferentes de propriedades. Exemplos desses objetos sobrepostos mas distintos são cubos virtuais, cubos vinculados e cubos normais. Para objetos sobrepostos mas distintos, o Analysis Services usa o padrão de **tipo** atributo de Namespace de instância de XML para indicar a herança. Por exemplo, que o fragmento de XML a seguir mostra como o **tipo** atributo identifica se um **cubo** elemento herda de um cubo normal ou de um cubo virtual:  
  
 `<Cubes>`  
  
 `<Cube xsi:type=”RegularCube”>`  
  
 `<Name>Sales</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `<Cube xsi:type=”VirtualCube”>`  
  
 `<Name>SalesAndInventory</Name>`  
  
 `...`  
  
 `</Cube>`  
  
 `</Cubes>`  
  
 ``  
  
 Geralmente, a herança não é usada quando vários tipos têm uma propriedade com o mesmo nome. Por exemplo, o **nome** e **ID** propriedades são exibidas em vários elementos, mas essas propriedades não foram promovidas para um tipo abstrato.  
  
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
  
 **Int**  
 Um valor inteiro no intervalo de -231 até 231 – 1.  
  
 **Longo**  
 Um valor inteiro no intervalo de -263 até 263 – 1.  
  
 **String**  
 Um valor de cadeia de caracteres em conformidade com as seguintes regras globais:  
  
-   Os caracteres de controle são retirados.  
  
-   Os espaços em branco inicial e final são retirados.  
  
-   O espaço em branco interno é preservado.  
  
 **Nome** e **ID** propriedades têm limitações especiais de caracteres válidos em elementos de cadeia de caracteres. Para obter informações adicionais sobre **nome** e **ID** convenções, consulte [objetos e características de objeto ASSL](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
 **DateTime**  
 Um **DateTime** estrutura do .NET Framework. Um **DateTime** valor não pode ser NULL. A data mais antiga suportada pelo **DataTime** tipo de dados é de 1 de janeiro de 1601, que está disponível a programadores como **DateTime. MinValue**. A data mais antiga suportada indica que um **DateTime** valor está ausente.  
  
 **Booliano**  
 Uma enumeração só com dois valores, como {verdadeiro, falso} ou {0, 1}.  
  
## <a name="default-values"></a>Valores padrão  
 O Analysis Services usa os padrões listados na tabela seguinte.  
  
|Tipo de dados XML|Valor padrão|  
|-------------------|-------------------|  
|**Booliano**|Falso|  
|**String**|"" (cadeia de caracteres vazia)|  
|**Inteiro** ou **longo**|0 (zero)|  
|**Timestamp**|12:00:00 AM, 1/1/0001 (correspondente a um .NET Frameworks **System. DateTime** com 0 tiques)|  
  
 Um elemento que está presente mas vazio será interpretado como tendo um valor de uma cadeia de caracteres nula, e não como o valor padrão.  
  
### <a name="inherited-defaults"></a>Padrões herdados  
 Algumas propriedades especificadas em um objeto fornecem valores padrão para a mesma propriedade em objetos filhos ou descendentes. Por exemplo, **Cube.StorageMode** fornece o valor padrão para **Partition.StorageMode**. As regras que o Analysis Services aplica para valores padrão herdados são as seguintes:  
  
-   Quando a propriedade do objeto filho for nula no XML, o padrão do seu valor será o valor herdado. No entanto, se você consultar o valor a partir do servidor, este retornará o valor nulo do elemento XML.  
  
-   Não é possível determinar programaticamente se a propriedade ou objeto filho foi definida corretamente no objeto filho ou herdado.  
  
 Alguns elementos definiram padrões que se aplicarão quando o elemento estiver ausente. Por exemplo, o **dimensão** elementos no fragmento XML a seguir são equivalentes, mesmo se um **dimensão** elemento contém um **visível** elemento, mas os outros  **Dimensão** elemento não.  
  
 `<Dimension>`  
  
 `<Name>Product</Name>`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `<Name>Product</ Name>`  
  
 `<Visible>true</Visible>`  
  
 `</Dimension>`  
  
 Para obter mais informações sobre padrões herdados, consulte [objetos e características de objeto ASSL](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
  
