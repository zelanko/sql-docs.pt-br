---
title: Objeto SqlXmlAdapter (Classes gerenciadas SQLXML) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- void Update(DataSet ds) method
- SqlXmlAdapter object
- void Fill(DataSet ds) method
- SQLXML Managed Classes, SqlXmlAdapter object
- Managed Classes [SQLXML], SqlXmlAdapter object
ms.assetid: 0a16eddf-fc26-4d92-82d4-359b5fb905d5
caps.latest.revision: "22"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 999504b39724033f885d533f8177567455205276
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sqlxml-managed-classes---sqlxmladapter-object"></a>SQLXML Classes gerenciadas por - objeto SqlXmlAdapter
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Esse objeto fornece métodos que facilitam a interação com o conjunto de dados a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] do .NET Framework. Para obter um exemplo de funcionamento, consulte [acessando a funcionalidade SQLXML no ambiente .NET](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 O objeto SqlXmlAdapter dá suporte a estes métodos:  
  
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
 [Objeto SqlXmlCommand &#40; Gerenciadas do SQLXML Classes &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlcommand-object.md)   
 [Objeto SqlXmlParameter &#40; Gerenciadas do SQLXML Classes &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlparameter-object.md)  
  
  
