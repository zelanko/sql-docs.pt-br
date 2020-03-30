---
title: Método setCharacterStream (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 09042ee9-dfb1-4d0b-82bd-d1224b0aea80
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc966b97231f491a5f3c2cdb71c457f0324a8df3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67974854"
---
# <a name="setcharacterstream-method-sqlservernclob"></a>Método setCharacterStream (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera um fluxo a ser usado para gravar um fluxo de caracteres Unicode no valor **NCLOB** que o objeto **java.sql.NClob** em questão representa, começando na posição especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.Writer setCharacterStream(long pos)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *pos*  
  
 A posição em que a gravação no valor **NCLOB** deve ser iniciada; a primeira posição é 1.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto Writer que representa o fluxo no qual os caracteres Unicode codificados podem ser gravados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setCharacterStream é especificado pelo método setCharacterStream na interface java.sql.NClob.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
