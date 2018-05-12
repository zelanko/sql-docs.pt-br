---
title: Criando e alterando objetos (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fcfb8d2f7ec13c4dda5aa533096d3ff5d5820fe1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="creating-and-altering-objects-xmla"></a>Criando e alterando objetos (XMLA)
  Os objetos principais podem ser criados, alterados e excluídos de forma independente. Os objetos principais incluem o seguinte:  
  
-   Servidores  
  
-   Bancos de dados  
  
-   Dimensões  
  
-   Cubes  
  
-   Grupos de medidas  
  
-   Partições  
  
-   Perspectivas  
  
-   Modelos de mineração  
  
-   Funções  
  
-   Comandos associados a um servidor ou a um banco de dados  
  
-   Fontes de dados  
  
 Você usa o [criar](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md) comando para criar um objeto principal em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e o [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) comando para alterar um objeto principal existente em uma instância. Os dois comandos são executados usando o [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
## <a name="creating-objects"></a>Criando objetos  
 Quando você cria objetos usando o **criar** método, primeiro você deve identificar o objeto pai que contém o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto a ser criado. Identifica o objeto pai fornecendo uma referência de objeto no [ParentObject](../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md) propriedade o **criar** comando. Cada referência de objeto contém os identificadores de objeto necessários para identificar exclusivamente o objeto pai para o **criar** comando. Para obter mais informações sobre referências de objeto, consulte [definindo e identificando objetos &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md).  
  
 Por exemplo, você deve fornecer uma referência de objeto a um cubo para criar um grupo de medidas novo para ele. A referência de objeto para o cubo no **ParentObject** propriedade contém um identificador de banco de dados e um identificador de cubo, como o mesmo identificador de cubo poderia ser usado em um banco de dados diferente.  
  
 O [ObjectDefinition](../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md) elemento contém elementos do Analysis Services Scripting Language (ASSL) que definem o objeto principal a ser criado. Para obter mais informações sobre ASSL, consulte [desenvolvimento com o Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Se você definir o **AllowOverwrite** atributo o **criar** comando como true, você pode substituir um objeto principal existente que tem o identificador especificado. Caso contrário, ocorrerá um erro se um objeto principal com o identificador especificado já existir no objeto pai.  
  
 Para obter mais informações sobre o **criar** command, consulte [criar elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md).  
  
### <a name="creating-session-objects"></a>Criando objetos de sessão  
 Os objetos de sessão são objetos temporários que só estão disponíveis para a sessão explícita ou implícita usada por um aplicativo cliente e são excluídos quando a sessão é encerrada. Você pode criar objetos de sessão, definindo o **escopo** atributo o **criar** comando *sessão*.  
  
> [!NOTE]  
>  Ao usar o *sessão* configuração, o **ObjectDefinition** elemento só pode conter [dimensão](../../analysis-services/scripting/objects/dimension-element-assl.md), [cubo](../../analysis-services/scripting/objects/cube-element-assl.md), ou [ MiningModel](../../analysis-services/scripting/objects/miningmodel-element-assl.md) elementos ASSL.  
  
## <a name="altering-objects"></a>Alterando objetos  
 Ao modificar objetos usando o **Alter** método, primeiro você deve identificar o objeto a ser modificado fornecendo uma referência de objeto no [objeto](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) propriedade o **Alter**comando. Cada referência de objeto contém os identificadores de objeto necessários para identificar exclusivamente o objeto para o **Alter** comando. Para obter mais informações sobre referências de objeto, consulte [definindo e identificando objetos &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md).  
  
 Por exemplo, você deve fornecer uma referência de objeto a um cubo para modificar a sua estrutura. A referência de objeto para o cubo no **objeto** propriedade contém um identificador de banco de dados e um identificador de cubo, como o mesmo identificador de cubo poderia ser usado em um banco de dados diferente.  
  
 O **ObjectDefinition** elemento contém elementos ASSL que definem o objeto principal a ser modificada. Para obter mais informações sobre ASSL, consulte [desenvolvimento com o Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Se você definir o **AllowCreate** atributo o **Alter** comando como true, você pode criar o objeto principal especificado se o objeto não existe. Caso contrário, ocorrerá um erro se um objeto principal especificado ainda não existir.  
  
### <a name="using-the-objectexpansion-attribute"></a>Usando o atributo ObjectExpansion  
 Se você estiver alterando somente as propriedades do objeto principal e não estiver redefinindo objetos secundários contidos pelo objeto principal, você pode definir o **ObjectExpansion** atributo o **Alter** comando *ObjectProperties*. O **ObjectDefinition** propriedade só precisará conter os elementos para as propriedades do objeto principal e o **Alter** comando deixa objetos secundários associados ao objeto principal.  
  
 Para redefinir objetos secundários para um objeto principal, você deve definir o **ObjectExpansion** atributo *ExpandFull* e a definição de objeto deve incluir todos os objetos secundários contidos pelo objeto principal. Se o **ObjectDefinition** propriedade o **Alter** comando não incluir explicitamente um objeto secundário contido pelo objeto principal, o objeto secundário que não foi incluído é excluído.  
  
### <a name="altering-session-objects"></a>Alterando objetos de sessão  
 Para modificar objetos de sessão criados pelo **criar** comando, defina o **escopo** atributo do **Alter** comando *sessão*.  
  
> [!NOTE]  
>  Ao usar o *sessão* configuração, o **ObjectDefinition** elemento só pode conter [dimensão](../../analysis-services/scripting/objects/dimension-element-assl.md), [cubo](../../analysis-services/scripting/objects/cube-element-assl.md), ou [ MiningModel](../../analysis-services/scripting/objects/miningmodel-element-assl.md) elementos ASSL.  
  
## <a name="creating-or-altering-subordinate-objects"></a>Criando ou alterando objetos subordinados  
 Embora um **criar** ou **Alter** comando cria ou altera apenas um objeto principal superior, o objeto principal que está sendo criado ou modificado poderá conter definições na circunscrição  **ObjectDefinition** propriedade para outros objetos principais e secundárias que são subordinados a ele. Por exemplo, se você definir um cubo, você especificar o banco de dados pai na **ParentObject**e na definição do cubo no **ObjectDefinition** você pode definir grupos de medidas do cubo e dentro da medida grupos que você pode definir partições para cada grupo de medidas. Um objeto secundário só pode ser definido sob o objeto principal que o contém. Para obter mais informações sobre objetos principais e secundários, consulte [objetos de banco de dados &#40;Analysis Services - dados multidimensionais&#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="description"></a>Description  
 O exemplo a seguir cria uma fonte de dados relacional que referencia o [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] exemplo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.  
  
### <a name="code"></a>Código  
  
```  
<Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <ParentObject>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
    </ParentObject>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=localhost;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ImpersonationInfo>  
                <ImpersonationMode>ImpersonateServiceAccount</ImpersonationMode>  
            </ImpersonationInfo>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT0S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Create>  
```  
  
### <a name="description"></a>Description  
 O exemplo a seguir altera a fonte de dados relacional criada no exemplo anterior para definir o tempo limite da consulta para a fonte de dados como 30 segundos.  
  
### <a name="code"></a>Código  
  
```  
<Alter ObjectExpansion="ObjectProperties" xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
        <DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>  
        <DataSourceID>AdventureWorksDW2012</DataSourceID>  
    </Object>  
    <ObjectDefinition>  
        <DataSource xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="RelationalDataSource">  
            <ID>AdventureWorksDW2012</ID>  
            <Name>AdventureWorksDW2012</Name>  
            <ConnectionString>Data Source=fr-dwk-02;Initial Catalog=AdventureWorksDW2008R2;Integrated Security=True</ConnectionString>  
            <ManagedProvider>System.Data.SqlClient</ManagedProvider>  
            <Timeout>PT30S</Timeout>  
        </DataSource>  
    </ObjectDefinition>  
</Alter>  
```  
  
### <a name="comments"></a>Comentários  
 O **ObjectExpansion** atributo o **Alter** foi definido como *ObjectProperties*. Essa configuração permite que o [ImpersonationInfo](../../analysis-services/scripting/properties/impersonationinfo-element-assl.md) elemento, um objeto secundário, a serem excluídos da fonte de dados definida no **ObjectDefinition**. Dessa forma, a informações de representação para aquela fonte de dados permanece definida para a conta de serviço, como especificado no primeiro exemplo.  
  
## <a name="see-also"></a>Consulte também  
 [Método Execute &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)   
 [Desenvolvimento com o Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
