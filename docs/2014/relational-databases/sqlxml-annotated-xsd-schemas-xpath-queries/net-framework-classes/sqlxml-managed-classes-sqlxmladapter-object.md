---
title: Objeto SqlXmlAdapter (classes gerenciadas SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- void Update(DataSet ds) method
- SqlXmlAdapter object
- void Fill(DataSet ds) method
- SQLXML Managed Classes, SqlXmlAdapter object
- Managed Classes [SQLXML], SqlXmlAdapter object
ms.assetid: 0a16eddf-fc26-4d92-82d4-359b5fb905d5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 86231096c8eef084b36d6195a1c720bd4f9038a3
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717953"
---
# <a name="sqlxmladapter-object-sqlxml-managed-classes"></a>Objeto SqlXmlAdapter (classes gerenciadas SQLXML)
  Este objeto fornece métodos que facilitam a interação com o conjunto de dados no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework. Para obter um exemplo funcional, consulte [acessando a funcionalidade SQLXML no ambiente .net](accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 O objeto SqlXmlAdapter dá suporte a esses métodos:  
  
 void Fill (DataSet DS)  
 Preenche o conjunto de dados no .NET Framework com os dados XML recuperados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 anular atualização (DataSet DS)  
 Aplica atualizações a registros no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a partir dos dados do conjunto de dados.  
  
 O objeto SqlXmlAdapter dá suporte a esses construtores:  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Objeto SqlXmlCommand &#40;classes gerenciadas SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)   
 [Objeto SqlXmlParameter &#40;classes gerenciadas SQLXML&#41;](sqlxml-managed-classes-sqlxmlparameter-object.md)  
  
  
