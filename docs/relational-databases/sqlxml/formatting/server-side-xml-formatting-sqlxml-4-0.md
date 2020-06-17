---
title: Formatação XML do lado do servidor (SQLXML)
description: Saiba mais sobre a formatação XML do lado do servidor de documentos gerados por consultas do SQLXML 4,0 executadas em um banco de dados Microsoft SQL Server.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- server-side XML formatting
ms.assetid: ae9ea068-0857-4505-a3b2-f53d256b644c
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: be657e9fa17be6c6ea2b0441d852f51efa6882be
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84882140"
---
# <a name="server-side-xml-formatting-sqlxml-40"></a>Formatação XML do lado do servidor (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este tópico fornece informações sobre a formatação de documentos XML no lado do servidor a partir de conjuntos de linhas gerados por consultas executadas com relação a um banco de dados no Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você pode armazenar e recuperar documentos XML para e de tabelas de banco de dados. Para recuperar um documento XML, use a extensão de consulta FOR XML em uma consulta SELECT.  
  
 Por exemplo, suponha que um aplicativo cliente execute um comando em relação [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ao que consiste na seguinte [!INCLUDE[tsql](../../../includes/tsql-md.md)] consulta:  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
FOR XML AUTO  
```  
  
 O servidor executa a consulta em duas etapas. Primeiro, o servidor executa esta instrução SELECT:  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
```  
  
 O servidor aplica a transformação FOR XML ao conjunto de linhas gerado. O XML resultante é enviado para o cliente como um conjunto de linhas de uma coluna. Nesta documentação, esse processo é chamado de formatação XML do lado do servidor.  
  
 No lado do servidor, você pode especificar os seguintes modos com uma cláusula FOR XML:  
  
-   RAW  
  
-   AUTO  
  
-   EXPLICIT  
  
 Para obter mais informações sobre a cláusula FOR XML, consulte [construindo XML Using for XML](../../../relational-databases/xml/for-xml-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Arquitetura da formatação XML do lado do cliente e do servidor &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/formatting/architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [Formatação XML do lado do cliente &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML &#40;SQL Server&#41;](../../../relational-databases/xml/for-xml-sql-server.md)  
  
  
