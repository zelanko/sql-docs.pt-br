---
title: Alterar as colunas existentes para colunas XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- tables [XML]
ms.assetid: 0d951424-9862-41fe-bd46-127f1c059bcb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a33f37c092c71185f00c6b3ddf3a02e6961d890d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47639524"
---
# <a name="change-existing-columns-to-xml-columns"></a>Converter colunas existentes em colunas XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  A instrução ALTER TABLE oferece suporte ao tipo de dados **xml** . Por exemplo, é possível alterar qualquer coluna de tipo cadeia de caracteres para o tipo de dados **xml** . Observe que nesses casos os documentos contidos na coluna devem estar bem formados. Além disso, se você estiver alterando o tipo da coluna de cadeia de caracteres para xml com tipo, os documentos da coluna serão validados em relação aos esquemas XSD especificados.  
  
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
>  Se uma tabela for grande, a modificação de uma coluna de tipo **xml** poderá ser dispendiosa. Isso ocorre porque a boa formação de cada documento deve ser verificada e o XML com tipo também deve ser validado.  
  
 Para obter mais informações sobre XML com tipo, consulte [Comparar XML com e sem tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
  
