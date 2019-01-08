---
title: Convenções de XML do ASSL | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c357efe4636c1b502cdb57305b9072907d4b2e98
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52532075"
---
# <a name="assl-xml-conventions"></a>Convenções de XML do ASSL
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  A ASSL (Analysis Services Scripting Language) representa a hierarquia de objetos como um conjunto de tipos de elementos, cada um definindo os elementos filhos que podem conter.  
  
 Para representar a hierarquia de objeto, a ASSL usa as seguintes convenções XML:  
  
-   Todos os objetos e propriedades são representadas como elementos, com exceção de atributos XML padrão como 'XML: lang'.  
  
-   Nomes de elementos e valores de enumeração seguem a convenção de nomenclatura do Microsoft .NET Framework do Pascal casing sem sublinhados.  
  
-   Os valores de maiúsculas e minúsculas é preservado. Os valores para enumerações também apresentam diferenciação de maiúsculas e minúsculas.  
  
 Além dessa lista de convenções, o Analysis Services segue também certas convenções relativas a cardinalidade, a herança, a espaço em branco, a tipos de dados e a valores padrão.  
  
## <a name="cardinality"></a>Cardinalidade  
 Quando um elemento tiver uma cardinalidade maior do que 1, haverá uma coleção de elementos XML que encapsula esse elemento. O nome de coleção usa a forma plural dos elementos contidos na coleção. Por exemplo, o fragmento XML a seguir representa o **dimensões** coleção dentro de uma **banco de dados** elemento:  
  
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
 A herança é usada quando existem objetos distintos com sobrepostos mas significativamente diferentes de propriedades. Exemplos desses objetos sobrepostos mas distintos são cubos virtuais, cubos vinculados e cubos normais. Para objetos sobrepostos mas distintos, o Analysis Services usa o padrão **tipo** atributo do Namespace de instância de XML para indicar a herança. Por exemplo, que o fragmento de XML a seguir mostra como o **tipo** atributo identifica se um **cubo** elemento herda de um cubo normal ou de um cubo virtual:  
  
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
 Um valor inteiro no intervalo de-231 até 231-1.  
  
 **Long**  
 Um valor inteiro no intervalo de -263 até 263-1.  
  
 **String**  
 Um valor de cadeia de caracteres em conformidade com as seguintes regras globais:  
  
-   Os caracteres de controle são retirados.  
  
-   Os espaços em branco inicial e final são retirados.  
  
-   O espaço em branco interno é preservado.  
  
 **Nome da** e **ID** propriedades têm limitações especiais em caracteres válidos em elementos de cadeia de caracteres. Para obter mais informações sobre **nome** e **ID** convenções, consulte [objetos e características de objeto ASSL](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
 **DateTime**  
 Um **DateTime** estrutura do .NET Framework. Um **DateTime** valor não pode ser NULL. A data mais antiga compatível com o **DataTime** tipo de dados é de 1º de janeiro de 1601, que está disponível a programadores como **MinValue**. A data mais antiga suportada indica que um **DateTime** valor está ausente.  
  
 **Booliano**  
 Uma enumeração só com dois valores, como {verdadeiro, falso} ou {0, 1}.  
  
## <a name="default-values"></a>Valores padrão  
 O Analysis Services usa os padrões listados na tabela seguinte.  
  
|Tipo de dados XML|Valor padrão|  
|-------------------|-------------------|  
|**Booliano**|Falso|  
|**String**|"" (cadeia de caracteres vazia)|  
|**Número inteiro** ou **longo**|0 (zero)|  
|**carimbo de hora**|12:00:00 AM, 1/1/0001 (correspondente a um .NET Frameworks **System. DateTime** com 0 tiques)|  
  
 Um elemento que está presente mas vazio será interpretado como tendo um valor de uma cadeia de caracteres nula, e não como o valor padrão.  
  
### <a name="inherited-defaults"></a>Padrões herdados  
 Algumas propriedades especificadas em um objeto fornecem valores padrão para a mesma propriedade em objetos filhos ou descendentes. Por exemplo, **Cube.StorageMode** fornece o valor padrão de **Partition.StorageMode**. As regras que o Analysis Services aplica para valores padrão herdados são as seguintes:  
  
-   Quando a propriedade do objeto filho for nula no XML, o padrão do seu valor será o valor herdado. No entanto, se você consultar o valor a partir do servidor, este retornará o valor nulo do elemento XML.  
  
-   Não é possível determinar programaticamente se a propriedade ou objeto filho foi definida corretamente no objeto filho ou herdado.  
  
 Alguns elementos definiram padrões que se aplicarão quando o elemento estiver ausente. Por exemplo, o **dimensão** elementos no fragmento XML a seguir são equivalentes, mesmo se um **dimensão** elemento contém um **Visible** elemento, mas os outros  **Dimensão** elemento não faz isso.  
  
 `<Dimension>`  
  
 `<Name>Product</Name>`  
  
 `</Dimension>`  
  
 `<Dimension>`  
  
 `<Name>Product</ Name>`  
  
 `<Visible>true</Visible>`  
  
 `</Dimension>`  
  
 Para obter mais informações sobre padrões herdados, consulte [objetos e características de objeto ASSL](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md).  
  
  
