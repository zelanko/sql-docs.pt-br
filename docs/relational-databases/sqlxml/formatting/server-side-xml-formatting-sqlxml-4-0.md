---
title: Formatação de XML do lado do servidor (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cd49b8b5304956cd37c9037ff47cc825e1ec8522
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47604475"
---
# <a name="server-side-xml-formatting-sqlxml-40"></a>Formatação XML do lado do servidor (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este tópico fornece informações sobre a formatação de documentos XML no lado do servidor a partir de conjuntos de linhas gerados por consultas executadas com relação a um banco de dados no Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você pode armazenar e recuperar documentos XML para e de tabelas de banco de dados. Para recuperar um documento XML, use a extensão de consulta FOR XML em uma consulta SELECT.  
  
 Por exemplo, suponha que um aplicativo cliente executa um comando em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que consiste no seguinte [!INCLUDE[tsql](../../../includes/tsql-md.md)] consulta:  
  
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
  
 Para obter mais informações sobre a cláusula FOR XML, consulte [construindo XML usando FOR XML](../../../relational-databases/xml/for-xml-sql-server.md).  
  
## <a name="see-also"></a>Consulte também  
 [Arquitetura de formatação de XML do lado do cliente e servidor &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [Formatação XML do lado do cliente &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML &#40;SQL Server&#41;](../../../relational-databases/xml/for-xml-sql-server.md)  
  
  
