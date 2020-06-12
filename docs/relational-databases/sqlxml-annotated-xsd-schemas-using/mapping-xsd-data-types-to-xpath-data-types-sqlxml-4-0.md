---
title: Mapeando tipos de dados XSD para tipos de dados XPath (SQLXML)
description: Saiba como mapear tipos de dados XSD para tipos de dados XPath ao executar uma consulta XPath no SQLXML 4,0.
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- XPath queries [SQLXML], mapping data types
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XPath data types [SQLXML]
- XSD schemas [SQLXML], mapping data types
ms.assetid: ced1a95e-18d4-4a5a-8da8-dbb6d58bbd45
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1dd2800d89016223e172e11ebde2cc3f8332e7d4
ms.sourcegitcommit: 9921501952147b9ce3e85a1712495d5b3eb13e5b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2020
ms.locfileid: "84215706"
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>Mapeando tipos de dados XSD para tipos de dados XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Quando uma consulta XPath é executada em um esquema XSD e o tipo XSD é especificado no atributo **xsd: Type** , o XPath usa o tipo de dados especificado quando processa a consulta.  
  
 O tipo de dados XPath de um nó é derivado do tipo de dados XSD no esquema, conforme mostra tabela a seguir. (O nó de EmployeeID é usado para fins meramente ilustrativos.)  
  
|Tipo de dados XSD|Tipo de dados XDR|Equivalente<br /><br /> tipos de dados XPath|SQL Server<br /><br /> conversão que é usada|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**Base64Binary**<br /><br /> **HexBinary**|**Nenhum**<br /><br /> **bin. base64bin. Hex**|**Não aplicável**|Nenhum<br /><br /> EmployeeID|  
|**Booliano**|**booleano**|**booleano**|CONVERT(bit, EmployeeID)|  
|**Decimal, inteiro, flutuante, byte, curto, int, longo, float, Double, unsignedByte, unsignedShort, unsignedInt, unsignedLong**|**number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8**|**number**|CONVERT(float(53), EmployeeID)|  
|**ID, IDREF, idrefsentity, entidades, notação, NMTOKEN, NMTOKENS, DateTime, Cadeia de caracteres, anyURI**|**ID, IDREF, idrefsentity, Entities, enumeração, notação, NMTOKEN, NMTOKENS, Char, dateTime, dateTime.tz, String, Uri, UUID**|**cadeia de caracteres**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**fixed14.4**|**Não aplicável (não há nenhum tipo de dados no XPath que seja equivalente ao tipo de dados do XDR do 14.4 corrigido.)**|CONVERT(money, EmployeeID)|  
|**date**|**date**|**cadeia de caracteres**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**time**|**time**<br /><br /> **time.tz**|**cadeia de caracteres**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
