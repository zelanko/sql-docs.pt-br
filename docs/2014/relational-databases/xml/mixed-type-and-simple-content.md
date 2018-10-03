---
title: Tipo misto e conteúdo simples | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- mixed types [SQL Server]
ms.assetid: 6ea1f11d-e64b-4ebb-ab68-4eb6e4027665
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 417954df470313af7ea90e7c0cdf2ff5ba9f1f7b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48162696"
---
# <a name="mixed-type-and-simple-content"></a>Tipo misto e conteúdo simples
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte à restrição de tipo misto a conteúdo simples.  
  
## <a name="example"></a>Exemplo  
 Na coleção de esquema XML a seguir, `myComplexTypeA` é um tipo complexo que pode ser esvaziado. Isto é, seus dois elementos têm `minOccurs` definido como 0. A tentativa de restringir isso a um conteúdo simples, como na declaração `myComplexTypeB` , não tem suporte. Portanto a criação da seguinte coleção de esquema XML não tem êxito:  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns"  
xmlns:ns1="http://ns1">  
  
    <complexType name="myComplexTypeA" mixed="true">  
        <sequence>  
            <element name="a" type="string" minOccurs="0"/>  
            <element name="b" type="string" minOccurs="0" maxOccurs="23"/>  
        </sequence>  
    </complexType>  
  
    <complexType name="myComplexTypeB">  
        <simpleContent>  
            <restriction base="ns:myComplexTypeA">  
                <simpleType>  
                    <restriction base="int">  
                        <minExclusive value="25"/>  
                    </restriction>  
                </simpleType>  
            </restriction>  
        </simpleContent>  
    </complexType>  
</schema>  
'  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos e limitações para o uso de Coleções de Esquemas XML no servidor](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
