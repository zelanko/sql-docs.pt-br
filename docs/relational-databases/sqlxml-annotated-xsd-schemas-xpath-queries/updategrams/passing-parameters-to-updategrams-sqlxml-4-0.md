---
title: Passando parâmetros para diagramas de atualização (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- nullvalue attribute
- passing parameters [SQLXML]
- parameters [SQLXML]
- updategrams [SQLXML], passing parameters
- null values [SQLXML]
ms.assetid: 2354e6e7-1860-471f-8711-4e374c5a4ed2
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cdfe34072c9eeda158cc36279e2e4371a197447e
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43077505"
---
# <a name="passing-parameters-to-updategrams-sqlxml-40"></a>Transmitindo parâmetros a diagramas de atualização (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Os diagramas de atualização (updategrams) são modelos; portanto, é possível passar parâmetros para eles. Para obter mais informações sobre como passar parâmetros para modelos, consulte [considerações de segurança do diagrama de atualização &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md).  
  
 Diagramas de atualização permitem passar NULL como um valor de parâmetro. Para passar o valor do parâmetro NULL, você deve especificar o **nullvalue** atributo. O valor que é atribuído para o **nullvalue** atributo, em seguida, é fornecido como o valor do parâmetro. Diagramas de atualização tratam esse valor como NULL.  
  
> [!NOTE]  
>  Na  **\<sql:header >** e  **\<updg:header >**, você deve especificar o **nullvalue** como não qualificado; enquanto isso, no  **\<updg:sync >**, você especifica a **nullvalue** como qualificado (por exemplo, **updg: NullValue**).  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, você deve atender aos requisitos especificados em [requisitos para executar exemplos do SQLXML](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
 Antes de usar os exemplos de diagrama de atualização, observe o seguinte:  
  
-   Os exemplos usam mapeamento padrão (quer dizer, nenhum esquema de mapeamento é especificado no diagrama de atualização). Para obter mais exemplos de diagramas de atualização que usam esquemas de mapeamento, consulte [especificando um esquema de mapeamento anotado em um diagrama de atualização &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
### <a name="a-passing-parameters-to-an-updategram"></a>A. Passando parâmetros para um diagrama de atualização  
 Neste exemplo, o diagrama de atualização altera o sobrenome de um funcionário na tabela HumanResources.Shift. O diagrama de atualização é passado com dois parâmetros: ShiftID, usado para identificar exclusivamente uma troca e Name.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header>  
  <updg:param name="ShiftID"/>  
  <updg:param name="Name" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="$ShiftID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="$Name" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Copie o updategram acima no Bloco de Notas e salve-o em um arquivo como UpdategramWithParameters.xml.  
  
2.  Prepare o script de teste SQLXML 4.0 (Sqlxml4test.vbs) em [usando o ADO para executar consultas do SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md) para executar o updategram adicionando as seguintes linhas depois de `cmd.Properties("Output Stream").Value = outStream`:  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value  
    cmd.Parameters.Append cmd.CreateParameter("@ShiftID",  2, 1,  0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@Name",   200, 1, 50, "New Name")  
    ```  
  
### <a name="b-passing-null-as-a-parameter-value-to-an-updategram"></a>B. Passando NULL como um valor de parâmetro para um updategram  
 Na execução de um updategram, o valor "isnull" é atribuído ao parâmetro que você deseja definir como NULL. O diagrama de atualização converte o valor do parâmetro "isnulll" em NULL e o processa de acordo.  
  
 O seguinte diagrama de atualização define um cargo de funcionário como NULL:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:header nullvalue="isnull" >  
  <updg:param name="EmployeeID"/>  
  <updg:param name="ManagerID" />  
</updg:header>  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Employee EmployeeID="$EmployeeID" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Employee ManagerID="$ManagerID" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para testar o diagrama de atualização  
  
1.  Copie o diagrama de atualização acima no Bloco de Notas e salve-o em um arquivo como UpdategramPassingNullvalues.xml.  
  
2.  Prepare o script de teste SQLXML 4.0 (Sqlxml4test.vbs) em [usando o ADO para executar consultas do SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md) para executar o updategram adicionando as seguintes linhas depois de `cmd.Properties("Output Stream").Value = outStream`:  
  
    ```  
    cmd.NamedParameters = True  
    ' CreateParameter arguments: Name, Type, Direction, Size, Value   
    cmd.Parameters.Append cmd.CreateParameter("@EmployeeID", 3, 1, 0, 1)  
    cmd.Parameters.Append cmd.CreateParameter("@ManagerID",  3, 1, 0, Null)  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Considerações de segurança do diagrama de atualização &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
