---
title: (SQLXML 4.0) de tratamento de NULL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 01367b6031ebce709fc80294d0a4ce131193c578
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006786"
---
# <a name="null-handling-sqlxml-40"></a>Manipulação de NULL (SQLXML 4.0)
  A sintaxe XML indica NULL como uma ausência. (Por exemplo, se o valor de um atributo ou elemento for NULL, esse atributo ou elemento estará ausente do documento XML.) No [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML, o atributo `updg:nullvalue` habilita a especificação de NULL como valor de um elemento ou atributo.  
  
 Por exemplo, o diagrama a seguir assegura que o **título** valor de um contato com **ContactID** 64 seja NULL e, em seguida, atualiza o **título** valor para "SR." para esse contato.  
  
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
  
 Quando os parâmetros são passados para um diagrama de atualização, é possível passar NULL como o valor do parâmetro. Isto é feito especificando o atributo `nullvalue` no bloco `<updg:header>`. Para obter um exemplo, consulte [passando parâmetros para diagramas de atualização &#40;SQLXML 4.0&#41;](passing-parameters-to-updategrams-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Consulte também  
 [Considerações de segurança do diagrama de atualização &#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  