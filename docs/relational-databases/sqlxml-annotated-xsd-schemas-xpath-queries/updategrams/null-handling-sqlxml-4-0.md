---
title: Manipulação nula (SQLXML)
description: 'Saiba como atributos ou elementos nulos podem ser especificados em um updategram 4,0 do SQLXML usando o atributo updg: NullValue.'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 57a0517bc698d2969d1ee1808cb52769fa8ef4ae
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790568"
---
# <a name="null-handling-sqlxml-40"></a>Manipulação de NULL (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  A sintaxe XML indica NULL como uma ausência. (Por exemplo, se um atributo ou valor de elemento for nulo, esse atributo ou elemento estará ausente do documento XML.) No [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML, o atributo **updg: NullValue** habilita a especificação de NULL para um valor de elemento ou atributo.  
  
 Por exemplo, o updategram a seguir garante que o valor de **título** de um contato com **contactid** de 64 seja NULL e, em seguida, atualiza o valor do **título** para "Mr". para este contato.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync updg:nullvalue="IsNULL"  >  
    <updg:before>  
       <Person.Contact ContactID="64" Title="IsNULL" />  
    </updg:before>  
    <updg:after>  
       <Person.Contact ContactID="64" Title="Mr." />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Quando os parâmetros são passados para um diagrama de atualização, é possível passar NULL como o valor do parâmetro. Isso é feito especificando o atributo **NullValue** no **\<updg:header>** bloco. Para obter um exemplo, consulte [passando parâmetros para updategrams &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Considerações de segurança do updategram &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
