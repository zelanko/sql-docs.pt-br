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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 59110e6686307e9555355fb72fefdbf6099bbc69
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52767318"
---
# <a name="null-handling-sqlxml-40"></a>Manipulação de NULL (SQLXML 4.0)
  A sintaxe XML indica NULL como uma ausência. (Por exemplo, se o valor de um atributo ou elemento for NULL, esse atributo ou elemento estará ausente do documento XML.) No [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML, o atributo `updg:nullvalue` habilita a especificação de NULL como valor de um elemento ou atributo.  
  
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
  
  
