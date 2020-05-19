---
title: Manipulação nula (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d21c1a215b05896838c4127c9a35f8add334f713
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703038"
---
# <a name="null-handling-sqlxml-40"></a>Manipulação de NULL (SQLXML 4.0)
  A sintaxe XML indica NULL como uma ausência. (Por exemplo, se um atributo ou valor de elemento for nulo, esse atributo ou elemento estará ausente do documento XML.) No [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML, o `updg:nullvalue` atributo habilita a especificação de NULL para um valor de elemento ou atributo.  
  
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
  
 Quando os parâmetros são passados para um diagrama de atualização, é possível passar NULL como o valor do parâmetro. Isto é feito especificando o atributo `nullvalue` no bloco `<updg:header>`. Para obter um exemplo, consulte [passando parâmetros para updategrams &#40;SQLXML 4,0&#41;](passing-parameters-to-updategrams-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Considerações de segurança do updategram &#40;SQLXML 4,0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
