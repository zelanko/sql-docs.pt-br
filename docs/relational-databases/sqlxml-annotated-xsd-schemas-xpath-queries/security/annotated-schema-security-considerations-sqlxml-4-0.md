---
title: Anotado considerações sobre segurança de esquemas (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 802f79c1f979e46dbc2dd7ee750122291daab83b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47699794"
---
# <a name="annotated-schema-security-considerations-sqlxml-40"></a>Considerações sobre a segurança de esquemas anotados (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Seguem diretrizes de segurança para o uso de esquemas anotados:  
  
-   Evite usar o mapeamento padrão nos esquemas de mapeamento. O mapeamento padrão expõe as informações do banco de dados (nomes de colunas e tabelas) no documento XML resultante porque, por padrão, os nomes de elementos são mapeados para nomes de tabelas e os nomes de atributos são mapeados para nomes de colunas. Assim, qualquer usuário que vê o documento XML tem acesso às informações de coluna e tabela do banco de dados, o que representa um possível risco de segurança. Para evitar esse risco, especifique nomes de elementos e atributos arbitrários no esquema e use anotações para mapeá-los explicitamente para as tabelas e colunas. Para obter mais informações sobre como usar o mapeamento padrão quando você cria esquemas XSD, consulte [mapeamento padrão de elementos XSD e os atributos para tabelas e colunas &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md).  
  
-   O mapeamento explícito especificado usando as anotações expõe as informações do banco de dados (como nomes de tabelas e nomes de colunas). Assim, talvez você não queira disponibilizar esses esquemas publicamente.  
  
-   Determinadas consultas, como aquelas especificadas em relação ao esquema de mapeamento com recursão (especificada usando **max-depth** anotação definida como um valor mais alto) pode levar mais tempo para executar. Opcionalmente, você pode especificar um tempo limite, definindo a propriedade de tempo limite do comando (em segundos). Por exemplo:  
  
    ```  
    cn.Open "Provider=SQLOLEDB;Server=localhost;Database=tempdb;Integrated Security=SSPI;Command Properties='Command Time Out=50';"  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Esquemas XSD anotados em SQLXML 4.0](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
  
  
