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
ms.openlocfilehash: 0c91b965498c0b617a02c7707e369a2ba61c0065
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67976149"
---
# <a name="preparestatement-method-javalangstring"></a>Método prepareStatement (java.lang.String)

Cria um objeto [SQLServerPreparedStatement](./sqlserverpreparedstatement-class.md) para enviar instruções SQL com parâmetros ao banco de dados.

## <a name="syntax"></a>Sintaxe

```
public java.sql.PreparedStatement prepareStatement(java.lang.String sql)
```

#### <a name="parameters"></a>parâmetros
*sql*

Uma **String** contendo uma instrução SQL.

## <a name="return-value"></a>Valor retornado
Um objeto PreparedStatement.

## <a name="exceptions"></a>Exceções  
[SQLServerException](./sqlserverexception-class.md)

## <a name="remarks"></a>Comentários
Esse método prepareStatement é especificado pelo método prepareStatement na interface java.sql.Connection.

## <a name="see-also"></a>Consulte Também

[Método prepareStatement &#40;SQLServerConnection&#41;](./preparestatement-method-sqlserverconnection.md)

[Membros de SQLServerConnection](./sqlserverconnection-members.md)

[Classe SQLServerConnection](./sqlserverconnection-class.md)
