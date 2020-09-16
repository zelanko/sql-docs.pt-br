---
description: Método prepareStatement (java.lang.String)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f9cec12d2443e84ef3334e19253a64ff60fea1c9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432858"
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

## <a name="return-value"></a>Valor de retorno
Um objeto PreparedStatement.

## <a name="exceptions"></a>Exceções  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Comentários
Esse método prepareStatement é especificado pelo método prepareStatement na interface java.sql.Connection.

## <a name="see-also"></a>Consulte Também

[Método prepareStatement &#40;SQLServerConnection&#41;](./preparestatement-method-sqlserverconnection.md)

[Membros de SQLServerConnection](./sqlserverconnection-members.md)

[Classe SQLServerConnection](./sqlserverconnection-class.md)
