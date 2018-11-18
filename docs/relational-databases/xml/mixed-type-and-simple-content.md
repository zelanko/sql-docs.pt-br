---
title: Tipo misto e conteúdo simples | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- mixed types [SQL Server]
ms.assetid: 6ea1f11d-e64b-4ebb-ab68-4eb6e4027665
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ea0036898d14e86e02b1625bbff494423a1b2292
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51674915"
---
# <a name="mixed-type-and-simple-content"></a>Tipo misto e conteúdo simples
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte à restrição de tipo misto a conteúdo simples.  
  
## <a name="example"></a>Exemplo  
 Na coleção de esquema XML a seguir, `myComplexTypeA` é um tipo complexo que pode ser esvaziado. Isto é, seus dois elementos têm `minOccurs` definido como 0. A tentativa de restringir isso a um conteúdo simples, como na declaração `myComplexTypeB` , não tem suporte. Portanto a criação da seguinte coleção de esquema XML não tem êxito:  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="https://www.w3.org/2001/XMLSchema" targetNamespace="https://ns" xmlns:ns="https://ns"  
xmlns:ns1="https://ns1">  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Requisitos e limitações de uso de coleções de esquema XML no servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
