---
title: Método prepareStatement (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e825765c-eb55-4800-951b-f3495da36641
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4fd42fccc0e6e3e15feb3d866ccb8d40531a1d4f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796700"
---
# <a name="preparestatement-method-javalangstring"></a>Método prepareStatement (java.lang.String)

Cria um objeto [SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md) para enviar instruções SQL com parâmetros ao banco de dados.

## <a name="syntax"></a>Sintaxe

```
public java.sql.PreparedStatement prepareStatement(java.lang.String sql)
```

#### <a name="parameters"></a>Parâmetros
*sql*

Uma **String** contendo uma instrução SQL.

## <a name="return-value"></a>Valor retornado
Um objeto PreparedStatement.

## <a name="exceptions"></a>Exceções  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Remarks
Esse método prepareStatement é especificado pelo método prepareStatement na interface java.sql.Connection.

## <a name="see-also"></a>Consulte Também

[Método prepareStatement &#40;SQLServerConnection&#41;](./preparestatement-method-sqlserverconnection.md)

[Membros de SQLServerConnection](./sqlserverconnection-members.md)

[Classe SQLServerConnection](./sqlserverconnection-class.md)
