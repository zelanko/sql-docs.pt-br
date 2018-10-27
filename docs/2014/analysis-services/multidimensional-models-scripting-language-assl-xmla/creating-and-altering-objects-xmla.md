---
title: Criando e alterando objetos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- objects [XML for Analysis]
- subordinate objects [XML for Analysis]
- XML for Analysis, objects
- modifying objects
- removing objects
- deleting objects
- XMLA, objects
ms.assetid: a2080867-e130-440c-92eb-f768869f34a8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 16d4b84c5d1dec2a09300fe23dab58774bf74cdb
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146242"
---
# <a name="creating-and-altering-objects-xmla"></a>Criando e alterando objetos (XMLA)
  Os objetos principais podem ser criados, alterados e excluídos de forma independente. Os objetos principais incluem o seguinte:  
  
-   Servidores  
  
-   Bancos de dados  
  
-   Dimensões  
  
-   Cubes  
  
-   Grupos de medidas  
  
-   Partições  
  
-   perspectivas  
  
-   Modelos de mineração  
  
-   Funções  
  
-   Comandos associados a um servidor ou a um banco de dados  
  
-   Fontes de Dados  
  
 Você usa o [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) comando para criar um objeto principal em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e o [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) comando para alterar um objeto principal existente em uma instância. Os dois comandos são executados usando o [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) método.  
  
## <a name="creating-objects"></a>Criando objetos  
 Quando você cria objetos usando o método `Create`, primeiro deve identificar o objeto pai que contém o objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a ser criado. Identifica o objeto pai fornecendo uma referência de objeto na [ParentObject](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) propriedade do `Create` comando. Cada referência de objeto contém os identificadores de objetos necessários para a identificação exclusiva do objeto pai para o comando `Create`. Para obter mais informações sobre referências de objeto, consulte [definindo e identificando objetos &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects).  
  
 Por exemplo, você deve fornecer uma referência de objeto a um cubo para criar um grupo de medidas novo para ele. A referência de objeto para o cubo na propriedade `ParentObject` contém um identificador de banco de dados e um identificador de cubo, já que, potencialmente, o mesmo identificador de cubo poderia ser usado em um banco de dados diferente.  
  
 O [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) elemento contém elementos ASSL Analysis Services Scripting Language () que definem o objeto principal a ser criado. Para obter mais informações sobre ASSL, consulte [desenvolver com o Analysis Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Se você definir o atributo `AllowOverwrite` do comando `Create` como verdadeiro, poderá substituir um objeto principal existente que tenha o identificador especificado. Caso contrário, ocorrerá um erro se um objeto principal com o identificador especificado já existir no objeto pai.  
  
 Para obter mais informações sobre o `Create` de comando, consulte [criar elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla).  
  
### <a name="creating-session-objects"></a>Criando objetos de sessão  
 Os objetos de sessão são objetos temporários que só estão disponíveis para a sessão explícita ou implícita usada por um aplicativo cliente e são excluídos quando a sessão é encerrada. Você pode criar objetos de sessão, definindo o `Scope` atributo do `Create` comando *sessão*.  
  
> [!NOTE]  
>  Ao usar o *sessão* definir, o `ObjectDefinition` elemento só pode conter [dimensão](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl), [cubo](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl), ou [MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL elementos.  
  
## <a name="altering-objects"></a>Alterando objetos  
 Ao modificar objetos usando o `Alter` método, primeiro você deve identificar o objeto a ser modificado fornecendo uma referência de objeto em de [objeto](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) propriedade do `Alter` comando. Cada referência de objeto contém os identificadores de objetos necessários para a identificação exclusiva do objeto para o comando `Alter`. Para obter mais informações sobre referências de objeto, consulte [definindo e identificando objetos &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects).  
  
 Por exemplo, você deve fornecer uma referência de objeto a um cubo para modificar a sua estrutura. A referência de objeto para o cubo na propriedade `Object` contém um identificador de banco de dados e um identificador de cubo, já que, potencialmente, o mesmo identificador de cubo poderia ser usado em um banco de dados diferente.  
  
 O elemento `ObjectDefinition` contém elementos da ASSL que definem o objeto principal a ser modificado. Para obter mais informações sobre ASSL, consulte [desenvolver com o Analysis Services Scripting Language &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Se você definir o atributo `AllowCreate` do comando `Alter` como verdadeiro, poderá criar o um objeto principal especificado caso ele ainda não exista. Caso contrário, ocorrerá um erro se um objeto principal especificado ainda não existir.  
  
### <a name="using-the-objectexpansion-attribute"></a>Usando o atributo ObjectExpansion  
 Se você estiver alterando apenas as propriedades do objeto principal e se não estiver redefinindo objetos secundários contidos pelo objeto principal, você pode definir a `ObjectExpansion` atributo o `Alter` comando *ObjectProperties*. A propriedade `ObjectDefinition` só precisará conter os elementos para as propriedades do objeto principal, e o comando `Alter` não tocará nos objetos secundários associados ao objeto principal.  
  
 Para redefinir objetos secundários para um objeto principal, você deve definir a `ObjectExpansion` de atributo para *ExpandFull* e a definição do objeto deve incluir todos os objetos secundários contidos pelo objeto principal. Se a propriedade `ObjectDefinition` do comando `Alter` não incluir explicitamente um objeto secundário contido pelo objeto principal, esse objeto secundário será excluído.  
  
### <a name="altering-session-objects"></a>Alterando objetos de sessão  
 Para modificar objetos de sessão criados pelo `Create` comando, defina a `Scope` atributo da `Alter` comando *sessão*.  
  
> [!NOTE]  
>  Ao usar o *sessão* definir, o `ObjectDefinition` elemento só pode conter [dimensão](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl), [cubo](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl), ou [MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL elementos.  
  
## <a name="creating-or-altering-subordinate-objects"></a>Criando ou alterando objetos subordinados  
 Embora um comando `Create` ou `Alter` crie ou altere somente o objeto principal superior, o objeto principal criado ou modificado poderá conter definições na propriedade de circunscrição `ObjectDefinition` para outros objetos principais e secundários subordinados a ele. Por exemplo, se você definir um cubo, especificará o banco de dados pai em `ParentObject`, na definição do cubo em `ObjectDefinition`, você poderá definir grupos de medidas para o cubo e no grupo de medidas poderá definir partições para cada grupo de medidas. Um objeto secundário só pode ser definido sob o objeto principal que o contém. Para obter mais informações sobre objetos principais e secundários, consulte [objetos de banco de dados &#40;Analysis Services - dados multidimensionais&#41;](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="description"></a>Description  
 O exemplo a seguir cria uma fonte de dados relacional que referencia o [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] amostra [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.  
  
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
 O `ObjectExpansion` atributo o `Alter` comando foi definido como *ObjectProperties*. Essa configuração permite que o [ImpersonationInfo](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl) elemento, um objeto secundário, a serem excluídos da fonte de dados definido no `ObjectDefinition`. Dessa forma, a informações de representação para aquela fonte de dados permanece definida para a conta de serviço, como especificado no primeiro exemplo.  
  
## <a name="see-also"></a>Consulte também  
 [Executar o método &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)   
 [Desenvolvendo com ASSL &#40;linguagem de script do Analysis Services&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
