---
title: "Método (Java) prepareStatement | Microsoft Docs"
ms.custom: 
ms.date: 02/07/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerConnection.prepareStatement (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: e825765c-eb55-4800-951b-f3495da36641
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cbf8bdbb869f4a82133918d579f7dfc1fd23d3d0
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="preparestatement-method-javalangstring"></a>Método prepareStatement (java.lang.String)

Cria um [SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md) parametrizadas de objeto para enviar instruções SQL para o banco de dados.

## <a name="syntax"></a>Sintaxe

```
public java.sql.PreparedStatement prepareStatement(java.lang.String sql)
```

#### <a name="parameters"></a>Parâmetros
*SQL*

Um **cadeia de caracteres** que contém uma instrução SQL.

## <a name="return-value"></a>Valor de retorno
Um objeto PreparedStatement.

## <a name="exceptions"></a>Exceções  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Comentários
Esse método prepareStatement é especificado pelo método prepareStatement na interface Java.SQL.

## <a name="see-also"></a>Consulte também

[Método prepareStatement &#40; SQLServerConnection &#41;](./preparestatement-method-sqlserverconnection.md)

[Membros de SQLServerConnection](./sqlserverconnection-members.md)

[Classe SQLServerConnection](./sqlserverconnection-class.md)
