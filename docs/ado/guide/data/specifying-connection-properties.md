---
title: Especificando propriedades de conexão | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5aee5946f3087956a0117b88f4044ef8a6c9bd9f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924133"
---
# <a name="specifying-connection-properties"></a>Especificar propriedades de conexão
Você pode fornecer grande parte das informações especificadas por uma [cadeia de conexão](../../../ado/guide/data/creating-a-connection-string.md) definindo as propriedades do objeto de **conexão** antes de abrir a conexão. Por exemplo, você pode obter o mesmo efeito que a cadeia de conexão discutida na [criação de uma cadeia de conexão](../../../ado/guide/data/creating-a-connection-string.md) usando o código a seguir.  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 DefaultDatabase só será definido depois que você abrir a conexão.  
  
> [!NOTE]
>  No ADO, você não deve usar uma senha que contém ponto e vírgula (";"), a menos que a senha esteja entre aspas simples.
