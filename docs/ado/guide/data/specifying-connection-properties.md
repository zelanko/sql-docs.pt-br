---
title: "Especificar as propriedades de Conexão | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87bcb0bed714e3fd2719405fbd1887a7943d219d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="specifying-connection-properties"></a>Especificar as propriedades de Conexão
Você pode fornecer muito as informações especificadas por um [cadeia de caracteres de conexão](../../../ado/guide/data/creating-a-connection-string.md) definindo propriedades do **Conexão** objeto antes de abrir a conexão. Por exemplo, você pode obter o mesmo efeito como a cadeia de caracteres de conexão é discutido em [criando uma cadeia de caracteres de Conexão](../../../ado/guide/data/creating-a-connection-string.md) usando o código a seguir.  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 DefaultDatabase é definido somente depois que você abrir a conexão.  
  
> [!NOTE]
>  No ADO, você não deve usar uma senha com ponto e vírgula (";"), a menos que a senha é colocada entre aspas simples.
