---
title: "Método (Java) prepareStatement | Microsoft Docs"
ms.custom: 
ms.date: 02/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.prepareStatement (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e825765c-eb55-4800-951b-f3495da36641
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c2452837aba5b8c5a146c12de838a3259f65be38
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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

