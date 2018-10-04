---
title: Trabalhando com tipos de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- DataType object
- SQL Server Management Objects, data types
- data types [SMO]
- SMO [SQL Server], data types
ms.assetid: 1e0e736a-c709-4d89-aeb2-b32dcfd641fa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a649e00e5b77a7b3276e82e34c04657cd8307284
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48121576"
---
# <a name="working-with-data-types"></a>Trabalhando com tipos de dados
  Existem muitos tipos e tamanhos de dados, como uma cadeia de caracteres com comprimento definido, um número com uma precisão específica ou um tipo de dados definido pelo usuário que é um outro objeto com seu próprio conjunto de regras. O <xref:Microsoft.SqlServer.Management.Smo.DataType> objeto classifica o tipo de dados para que possa ser tratada corretamente pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O objeto <xref:Microsoft.SqlServer.Management.Smo.DataType> é associado a objetos que aceitam dados. O seguinte [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] objetos Management Objects (SMO) aceitam dados que devem ser definidos por um <xref:Microsoft.SqlServer.Management.Smo.DataType> propriedade de objeto:  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Column>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedAggregateParameter>  
  
 A propriedade `DataType` para objetos que aceitam dados pode ser definida de várias maneiras.  
  
-   Use o construtor padrão e especifique <xref:Microsoft.SqlServer.Management.Smo.DataType> explicitamente as propriedades do objeto  
  
-   Use um construtor sobrecarregado e especifique o <xref:Microsoft.SqlServer.Management.Smo.DataType> propriedades como parâmetros.  
  
-   Especifique o <xref:Microsoft.SqlServer.Management.Smo.DataType> embutido no construtor de objeto.  
  
-   Use um dos membros estáticos da classe <xref:Microsoft.SqlServer.Management.Smo.DataType>, por exemplo `Int`. Isso retornará, na realidade, uma instância de um objeto <xref:Microsoft.SqlServer.Management.Smo.DataType>.  
  
 O objeto <xref:Microsoft.SqlServer.Management.Smo.DataType> tem várias propriedades que definem o tipo de dados. Por exemplo, a propriedade <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> especifica o tipo de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os valores constantes que representam [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de dados são listados no <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> enumeração. Isso se refere a tipos de dados como `varchar`, `nchar`, `currency`, `integer`, `float` e `datetime`.  
  
 Quando o tipo de dados for estabelecido, propriedades específicas deverão ser definidas para os dados. Por exemplo, se ele for um tipo `nchar`, o comprimento dos dados de cadeia de caracteres deverá ser definido na propriedade `Length`. O mesmo se aplica a valores numéricos, nos quais você teria que especificar a precisão e a escala.  
  
 Os tipos de dados<xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> e <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> se referem a objetos que contêm a definição do tipo de dados definido pelo usuário. O <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> se baseia em tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da enumeração <xref:Microsoft.SqlServer.Management.Smo.SqlDataType>. O <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> se baseia no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] tipos de dados do .NET. Normalmente, esses representariam dados de um tipo específico que é reutilizado com frequência pelo banco de dados por causa de regras comerciais definidas pela organização. Por exemplo, um tipo de dados que armazena uma quantia de dinheiro e um denominador monetário seria útil em uma empresa que trabalha com várias moedas.  
  
 O <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> enumeração contém uma lista de todos os [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-tipos de dados com suporte.  
  
## <a name="examples"></a>Exemplos  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-basic"></a>Construindo um objeto DataType com a especificação do construtor no Visual Basic  
 Este exemplo de código mostra como usar o construtor para criar instâncias de tipos de dados que são baseadas em diferentes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de dados.  
  
> [!NOTE]  
>  Todos os tipos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> e XML exigem um valor de nome para identificação do objeto.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDataTypes1](SMO How to#SMO_VBDataTypes1)]  -->  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-c"></a>Construindo um objeto DataType com a especificação do construtor no Visual C#  
 Este exemplo de código mostra como usar o construtor para criar instâncias de tipos de dados que são baseadas em diferentes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de dados.  
  
> [!NOTE]  
>  Todos os tipos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> e XML exigem um valor de nome para identificação do objeto.  
  
```  
{   
//Declare a DataType object variable and define the data type in the constructor.   
DataType dt;   
//For the decimal data type the following two arguements specify precision, and scale.   
dt = new DataType(SqlDataType.Decimal, 10, 2);   
}  
```  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-basic"></a>Construindo um objeto DataType com o construtor padrão no Visual Basic  
 Este exemplo de código mostra como usar o construtor padrão para criar instâncias de tipos de dados que são baseadas em diferentes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de dados. As propriedades são, então, usadas para especificar o tipo de dados.  
  
 **Observação** as <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>, e todos os tipos XML exigem um valor de nome para identificar o objeto.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDataTypes2](SMO How to#SMO_VBDataTypes2)]  -->  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-c"></a>Construindo um objeto DataType com o construtor padrão no Visual C#  
 Este exemplo de código mostra como usar o construtor padrão para criar instâncias de tipos de dados que são baseadas em diferentes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de dados. As propriedades são, então, usadas para especificar o tipo de dados.  
  
 **Observação** as <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>, e todos os tipos XML exigem um valor de nome para identificar o objeto.  
  
```  
{   
//Declare and create a DataType object variable.   
DataType dt;   
dt = new DataType();   
//Define the data type by setting the SqlDataType property.   
dt.SqlDataType = SqlDataType.VarChar;   
//The VarChar data type requires a value for the MaximumLength property.   
dt.MaximumLength = 100;   
}  
```  
  
  
