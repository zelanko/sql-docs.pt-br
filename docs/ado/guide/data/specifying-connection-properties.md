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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6fee9745bca206f00603b32a6c4cd29faab34eca
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760832"
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
