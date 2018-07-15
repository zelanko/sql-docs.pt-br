---
title: Objeto SqlXmlAdapter (Classes gerenciadas SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- void Update(DataSet ds) method
- SqlXmlAdapter object
- void Fill(DataSet ds) method
- SQLXML Managed Classes, SqlXmlAdapter object
- Managed Classes [SQLXML], SqlXmlAdapter object
ms.assetid: 0a16eddf-fc26-4d92-82d4-359b5fb905d5
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 192f356052289725043ae2b3dc748931aedb11fd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37331406"
---
# <a name="sqlxmladapter-object-sqlxml-managed-classes"></a>Objeto SqlXmlAdapter (classes gerenciadas SQLXML)
  Este objeto fornece métodos que facilitam a interação com o conjunto de dados no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework. Para obter um exemplo funcional, consulte [acessando a funcionalidade SQLXML no ambiente .NET](accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 O objeto SqlXmlAdapter dá suporte a esses métodos:  
  
 void Fill (DataSet ds)  
 Preenche o conjunto de dados no .NET Framework com os dados XML recuperados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 void Update (DataSet ds)  
 Aplica atualizações a registros no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a partir dos dados do conjunto de dados.  
  
 O objeto SqlXmlAdapter dá suporte a estes construtores:  
  
```  
public SqlXmlAdapter(SqlXmlCommand  cmd)   
  
public SqlXmlAdapter(  
                     string commandText,   
                     SqlXmlCommandType cmdType,   
                     string connectionString  
                      )   
  
public SqlXmlAdapter(  
                     Stream commandStream,   
                     SqlXmlCommandType cmdType,   
                     string connectionString  
                     )   
```  
  
## <a name="see-also"></a>Consulte também  
 [Objeto SqlXmlCommand &#40;Classes gerenciadas SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)   
 [Objeto SqlXmlParameter &#40;Classes gerenciadas SQLXML&#41;](sqlxml-managed-classes-sqlxmlparameter-object.md)  
  
  
