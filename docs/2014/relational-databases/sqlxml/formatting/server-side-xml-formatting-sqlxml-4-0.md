---
title: Formatação XML do lado do servidor (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- server-side XML formatting
ms.assetid: ae9ea068-0857-4505-a3b2-f53d256b644c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 13e20c9c4b415ad5dabc53baad813126a81afcae
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702869"
---
# <a name="server-side-xml-formatting-sqlxml-40"></a>Formatação XML do lado do servidor (SQLXML 4.0)
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
  
 Para obter mais informações sobre a cláusula FOR XML, consulte [construindo XML Using for XML](../../xml/for-xml-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Arquitetura da formatação XML do lado do cliente e do servidor &#40;SQLXML 4,0&#41;](architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [Formatação XML do lado do cliente &#40;SQLXML 4,0&#41;](client-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML &#40;SQL Server&#41;](../../xml/for-xml-sql-server.md)  
  
  
