---
title: Método setCharacterStream (SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerClob.setCharacterStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c02778f2-6681-4a84-a58b-2bcfac4233e4
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e3e1166b5ce5f5fbe6f1763c0de387c19bfcb26
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="setcharacterstream-method-sqlserverclob"></a>Método setCharacterStream (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um fluxo a ser usado para gravar um fluxo de caracteres Unicode no CLOB, iniciando na posição fornecida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.Writer setCharacterStream(long pos)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *POS*  
  
 A posição em que a gravação deve ser iniciada no objeto CLOB.  
  
## <a name="return-value"></a>Valor de retorno  
 Um fluxo no qual os caracteres Unicode codificados podem ser gravados.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método setCharacterStream é especificado pelo método setCharacterStream na interface do CLOB.  
  
 Os dados de caractere no CLOB são substituídos pelo gravador, iniciando na posição especificada, e podem ultrapassar o comprimento inicial do CLOB. A especificação de um valor posição +1 acrescentará caracteres. A especificação de um valor posição +2 ou maior (ou zero ou menos) lançará um erro de posição.  
  
## <a name="see-also"></a>Consulte também  
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
