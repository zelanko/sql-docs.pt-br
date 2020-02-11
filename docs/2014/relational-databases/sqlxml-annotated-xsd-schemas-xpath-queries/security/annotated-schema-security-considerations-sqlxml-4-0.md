---
title: Considerações de segurança de esquema anotado (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping schema [SQLXML], security
- annotated XDR schemas, security
- XDR schemas [SQLXML], security
- annotations [SQLXML]
- annotated XSD schemas, security
- SQLXML, annotated XSD schemas
- SQLXML, annotated XDR schemas
- security [SQLXML], annotated schemas
- XSD schemas [SQLXML], security
ms.assetid: 7d7e44dc-b6d3-4e0f-95c7-8f99930c94f2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 635c5c433f583ecad9f8dda1e35e4c981742212e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66010578"
---
# <a name="annotated-schema-security-considerations-sqlxml-40"></a>Considerações sobre a segurança de esquemas anotados (SQLXML 4.0)
  Seguem diretrizes de segurança para o uso de esquemas anotados:  
  
-   Evite usar o mapeamento padrão nos esquemas de mapeamento. O mapeamento padrão expõe as informações do banco de dados (nomes de colunas e tabelas) no documento XML resultante porque, por padrão, os nomes de elementos são mapeados para nomes de tabelas e os nomes de atributos são mapeados para nomes de colunas. Assim, qualquer usuário que vê o documento XML tem acesso às informações de coluna e tabela do banco de dados, o que representa um possível risco de segurança. Para evitar esse risco, especifique nomes de elementos e atributos arbitrários no esquema e use anotações para mapeá-los explicitamente para as tabelas e colunas. Para obter mais informações sobre como usar o mapeamento padrão ao criar esquemas XSD, consulte [mapeamento padrão de elementos e atributos XSD para tabelas e colunas &#40;SQLXML 4,0&#41;](../../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md).  
  
-   O mapeamento explícito especificado usando as anotações expõe as informações do banco de dados (como nomes de tabelas e nomes de colunas). Assim, talvez você não queira disponibilizar esses esquemas publicamente.  
  
-   Determinadas consultas, como as especificadas com relação ao esquema de mapeamento com recursão (especificada usando a anotação `max-depth` definida com um valor superior), podem levar mais tempo para serem executadas. Opcionalmente, você pode especificar um limite de tempo limite definindo a propriedade de tempo limite do comando (em segundos). Por exemplo:  
  
    ```  
    cn.Open "Provider=SQLOLEDB;Server=localhost;Database=tempdb;Integrated Security=SSPI;Command Properties='Command Time Out=50';"  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Esquemas XSD anotados em SQLXML 4.0](../../sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
  
  
