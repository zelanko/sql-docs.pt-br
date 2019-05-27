---
title: NULL de tratamento (SQLXML 4.0) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11f7ca96ca65ae23202b84030140e0eaef945de2
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014686"
---
# <a name="null-handling-sqlxml-40"></a>Manipulação de NULL (SQLXML 4.0)
  A sintaxe XML indica NULL como uma ausência. (Por exemplo, se um valor de atributo ou elemento for NULL, esse atributo ou elemento estiver ausente do documento XML.) Na [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML, o `updg:nullvalue` atributo permite especificar NULL para um valor de elemento ou atributo.  
  
 Por exemplo, o seguinte diagrama de atualização garante que o **Title** o valor de um contato com **ContactID** 64 seja NULL e, em seguida, atualiza o **título** valor para "SR." para esse contato.  
  
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
  
 Quando os parâmetros são passados para um diagrama de atualização, é possível passar NULL como o valor do parâmetro. Isto é feito especificando o atributo `nullvalue` no bloco `<updg:header>`. Por exemplo, consulte [passando parâmetros para diagramas de atualização &#40;SQLXML 4.0&#41;](passing-parameters-to-updategrams-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Consulte também  
 [Considerações de segurança do diagrama de atualização &#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
