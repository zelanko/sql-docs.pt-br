---
title: Alterar as colunas existentes para colunas XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- tables [XML]
ms.assetid: 0d951424-9862-41fe-bd46-127f1c059bcb
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ef71809c5d54fff77bed4ff3a1fd7c9b471337b7
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889362"
---
# <a name="change-existing-columns-to-xml-columns"></a>Converter colunas existentes em colunas XML
  A instrução ALTER TABLE dá suporte a `xml` tipo de dados. Por exemplo, você pode alterar qualquer coluna de tipo de cadeia de caracteres para o `xml` tipo de dados. Observe que nesses casos os documentos contidos na coluna devem estar bem formados. Além disso, se você estiver alterando o tipo da coluna de cadeia de caracteres para xml com tipo, os documentos da coluna serão validados em relação aos esquemas XSD especificados.  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 nvarchar(max))  
GO  
INSERT INTO T   
VALUES (1, '<Root><Product ProductID="1"/></Root>')  
GO  
ALTER TABLE T   
ALTER COLUMN Col2 xml  
GO  
```  
  
 É possível alterar uma coluna de tipo `xml` de XML sem-tipo para XML com tipo. Por exemplo:  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T   
values (1, '<p1:ProductDescription ProductModelID="1"   
xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
            </p1:ProductDescription>')  
GO   
-- Make it a typed xml column by specifying a schema collection.  
ALTER TABLE T   
ALTER COLUMN Col2 xml (Production.ProductDescriptionSchemaCollection)  
GO  
```  
  
> [!NOTE]  
>  O script será executado no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] porque a coleção de esquema XML, `Production.ProductDescriptionSchemaCollection`, é criada como parte do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
 No exemplo anterior, todas as instâncias armazenadas na coluna são validadas e classificadas nos esquemas XSD na coleção especificada. Se a coluna contiver uma ou mais instâncias XML inválidas em relação ao esquema especificado, haverá falha na instrução `ALTER TABLE` e você não poderá alterar a coluna de XML sem-tipo para XML com tipo.  
  
> [!NOTE]  
>  Se uma tabela for grande, modificando um `xml` coluna de tipo pode ser dispendiosa. Isso ocorre porque a boa formação de cada documento deve ser verificada e o XML com tipo também deve ser validado.  
  
 Para obter mais informações sobre XML com tipo, consulte [Comparar XML com e sem tipo](compare-typed-xml-to-untyped-xml.md).  
  
  
