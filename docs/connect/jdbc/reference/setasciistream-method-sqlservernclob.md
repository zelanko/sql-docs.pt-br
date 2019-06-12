---
title: Método setAsciiStream (SQLServerNClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 617ece92-0fb1-4f95-b32d-29b5b56eb3fb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: aebc713ab5256527571eb1a4277caa74e53623d7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765050"
---
# <a name="setasciistream-method-sqlservernclob"></a>Método setAsciiStream (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera um fluxo a ser usado para gravar caracteres ASCII no valor **NCLOB** que o objeto **java.sql.NClob** em questão representa, começando na posição especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.OutputStream setAsciiStream(long pos)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pos*  
  
 A posição em que a gravação no objeto **NCLOB** deve ser iniciada; a primeira posição é 1.  
  
## <a name="return-value"></a>Valor retornado  
 Um objeto OutputStream que representa o fluxo no qual os caracteres ASCII codificados podem ser gravados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método setAsciiStream é especificado pelo método setAsciiStream na interface do NCLOB.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [Membros SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [Classe SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
