---
title: Criando e alterando objetos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: 3dcc6eedc97b3d476d79420b4e067883e17f03d2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62702300"
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
  
-   Fontes de dados  
  
 Você usa o comando [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) para criar um objeto principal em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e o comando [ALTER](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) para alterar um objeto principal existente em uma instância. Ambos os comandos são executados usando o método [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) .  
  
## <a name="creating-objects"></a>Criando objetos  
 Quando você cria objetos usando o método `Create`, primeiro deve identificar o objeto pai que contém o objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a ser criado. Você identifica o objeto pai fornecendo uma referência de objeto na propriedade [ParentObject](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) do `Create` comando. Cada referência de objeto contém os identificadores de objetos necessários para a identificação exclusiva do objeto pai para o comando `Create`. Para obter mais informações sobre referências de objeto, consulte [definindo e identificando objetos &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects).  
  
 Por exemplo, você deve fornecer uma referência de objeto a um cubo para criar um grupo de medidas novo para ele. A referência de objeto para o cubo na propriedade `ParentObject` contém um identificador de banco de dados e um identificador de cubo, já que, potencialmente, o mesmo identificador de cubo poderia ser usado em um banco de dados diferente.  
  
 O elemento [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) contém Analysis Services elementos de linguagem de script (ASSL) que definem o objeto principal a ser criado. Para obter mais informações sobre o ASSL, consulte [desenvolvendo com a linguagem de script Analysis Services &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Se você definir o atributo `AllowOverwrite` do comando `Create` como verdadeiro, poderá substituir um objeto principal existente que tenha o identificador especificado. Caso contrário, ocorrerá um erro se um objeto principal com o identificador especificado já existir no objeto pai.  
  
 Para obter mais informações sobre `Create` o comando, consulte [criar elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla).  
  
### <a name="creating-session-objects"></a>Criando objetos de sessão  
 Os objetos de sessão são objetos temporários que só estão disponíveis para a sessão explícita ou implícita usada por um aplicativo cliente e são excluídos quando a sessão é encerrada. Você pode criar objetos de sessão definindo o `Scope` atributo do `Create` comando para *sessão*.  
  
> [!NOTE]  
>  Ao usar a configuração de *sessão* , `ObjectDefinition` o elemento só pode conter elementos de [dimensão](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl), [cubo](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)ou [MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL.  
  
## <a name="altering-objects"></a>Alterando objetos  
 Ao modificar objetos usando o `Alter` método, primeiro você deve identificar o objeto a ser modificado fornecendo uma referência de objeto na propriedade [Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) do `Alter` comando. Cada referência de objeto contém os identificadores de objetos necessários para a identificação exclusiva do objeto para o comando `Alter`. Para obter mais informações sobre referências de objeto, consulte [definindo e identificando objetos &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects).  
  
 Por exemplo, você deve fornecer uma referência de objeto a um cubo para modificar a sua estrutura. A referência de objeto para o cubo na propriedade `Object` contém um identificador de banco de dados e um identificador de cubo, já que, potencialmente, o mesmo identificador de cubo poderia ser usado em um banco de dados diferente.  
  
 O elemento `ObjectDefinition` contém elementos da ASSL que definem o objeto principal a ser modificado. Para obter mais informações sobre o ASSL, consulte [desenvolvendo com a linguagem de script Analysis Services &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
 Se você definir o atributo `AllowCreate` do comando `Alter` como verdadeiro, poderá criar o um objeto principal especificado caso ele ainda não exista. Caso contrário, ocorrerá um erro se um objeto principal especificado ainda não existir.  
  
### <a name="using-the-objectexpansion-attribute"></a>Usando o atributo ObjectExpansion  
 Se você estiver alterando apenas as propriedades do objeto principal e não estiver redefinindo objetos secundários contidos pelo objeto principal, poderá definir o `ObjectExpansion` atributo do `Alter` comando para *ObjectProperties*. A propriedade `ObjectDefinition` só precisará conter os elementos para as propriedades do objeto principal, e o comando `Alter` não tocará nos objetos secundários associados ao objeto principal.  
  
 Para redefinir objetos secundários para um objeto principal, você deve definir o `ObjectExpansion` atributo como *ExpandFull* e a definição do objeto deve incluir todos os objetos secundários contidos pelo objeto principal. Se a propriedade `ObjectDefinition` do comando `Alter` não incluir explicitamente um objeto secundário contido pelo objeto principal, esse objeto secundário será excluído.  
  
### <a name="altering-session-objects"></a>Alterando objetos de sessão  
 Para modificar objetos de sessão criados pelo `Create` comando, defina o `Scope` atributo do `Alter` comando para *sessão*.  
  
> [!NOTE]  
>  Ao usar a configuração de *sessão* , `ObjectDefinition` o elemento só pode conter elementos de [dimensão](https://docs.microsoft.com/bi-reference/assl/objects/dimension-element-assl), [cubo](https://docs.microsoft.com/bi-reference/assl/objects/cube-element-assl)ou [MiningModel](https://docs.microsoft.com/bi-reference/assl/objects/miningmodel-element-assl) ASSL.  
  
## <a name="creating-or-altering-subordinate-objects"></a>Criando ou alterando objetos subordinados  
 Embora um comando `Create` ou `Alter` crie ou altere somente o objeto principal superior, o objeto principal criado ou modificado poderá conter definições na propriedade de circunscrição `ObjectDefinition` para outros objetos principais e secundários subordinados a ele. Por exemplo, se você definir um cubo, especificará o banco de dados pai em `ParentObject`, na definição do cubo em `ObjectDefinition`, você poderá definir grupos de medidas para o cubo e no grupo de medidas poderá definir partições para cada grupo de medidas. Um objeto secundário só pode ser definido sob o objeto principal que o contém. Para obter mais informações sobre objetos principais e secundários, consulte [objetos de banco de dados &#40;Analysis Services-&#41;multidimensional ](../multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="description"></a>DESCRIÇÃO  
 O exemplo a seguir cria uma fonte de dados relacional que [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] faz [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] referência ao banco de dado de exemplo.  
  
### <a name="code"></a>Código  
  
```  
<Create xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
  
### <a name="description"></a>DESCRIÇÃO  
 O exemplo a seguir altera a fonte de dados relacional criada no exemplo anterior para definir o tempo limite da consulta para a fonte de dados como 30 segundos.  
  
### <a name="code"></a>Código  
  
```  
<Alter ObjectExpansion="ObjectProperties" xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
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
 O `ObjectExpansion` atributo do `Alter` comando foi definido como *ObjectProperties*. Essa configuração permite que o elemento [ImpersonationInfo](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl) , um objeto secundário, seja excluído da fonte de dados definida em `ObjectDefinition`. Dessa forma, a informações de representação para aquela fonte de dados permanece definida para a conta de serviço, como especificado no primeiro exemplo.  
  
## <a name="see-also"></a>Consulte Também  
 [Método execute &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)   
 [Desenvolvendo com a linguagem de script Analysis Services &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
