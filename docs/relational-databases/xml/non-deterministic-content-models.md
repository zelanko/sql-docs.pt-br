---
title: "Modelos de conteúdo não determinístico | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- non-deterministic content models
- content models [XML in SQL Server]
ms.assetid: 9d4513e7-dd19-4491-b7c7-28bc7c2f8589
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7b0f88c06eea8c1b15ead500eb365ac4fce8d5c1
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="non-deterministic-content-models"></a>modelos de conteúdo não determinístico
  Antes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 (SP1), o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rejeitava esquemas XML que tinham modelos de conteúdo não determinístico.  
  
 No entanto, a partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1 os modelos de conteúdo não determinístico serão aceitos se as restrições de ocorrência forem 0,1 ou não associadas.  
  
## <a name="example-non-deterministic-content-model-rejected"></a>Exemplo: Modelo de conteúdo não determinístico rejeitado  
 O exemplo a seguir tenta criar um esquema XML com um modelo de conteúdo não determinístico. Há falha no código porque não está claro se o elemento `<root>` deve ter uma sequência de dois elementos `<a>` ou se o elemento `<root>` deve ter duas sequências, cada uma com um elemento `<a>` .  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
    <element name="root">  
        <complexType>  
            <sequence minOccurs="1" maxOccurs="2">  
                <element name="a" type="string" minOccurs="1" maxOccurs="2"/>  
            </sequence>  
        </complexType>  
    </element>  
</schema>  
'  
GO  
```  
  
 O esquema pode ser fixado movendo a restrição de ocorrência para um local exclusivo. Por exemplo, a restrição pode ser movida para a partícula da sequência de contenção:  
  
```  
<sequence minOccurs="1" maxOccurs="4">  
    <element name="a" type="string" minOccurs="1" maxOccurs="1"/>  
</sequence>  
```  
  
 Ou a restrição pode ser movida para o elemento contido:  
  
```  
<sequence minOccurs="1" maxOccurs="1">  
     <element name="a" type="string" minOccurs="1" maxOccurs="4"/>  
</sequence>  
```  
  
## <a name="example-non-deterministic-content-model-accepted"></a>Exemplo: Modelo de conteúdo não determinístico aceito  
 O esquema a seguir deve ser rejeitado em versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1.  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
    <element name="root">  
        <complexType>  
            <sequence minOccurs="0" maxOccurs="unbounded">  
                <element name="a" type="string" minOccurs="0" maxOccurs="1"/>  
                <element name="b" type="string" minOccurs="1" maxOccurs="unbounded"/>  
            </sequence>  
        </complexType>  
    </element>  
</schema>  
'  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos e limitações de uso de coleções de esquema XML no servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
