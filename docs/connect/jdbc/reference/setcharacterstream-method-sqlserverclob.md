---
title: Método setCharacterStream (SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.setCharacterStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c02778f2-6681-4a84-a58b-2bcfac4233e4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8650ffe29710670bae8d3a934cd4caceaf74f723
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795655"
---
# <a name="setcharacterstream-method-sqlserverclob"></a>Método setCharacterStream (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um fluxo a ser usado para gravar um fluxo de caracteres Unicode no CLOB, iniciando na posição fornecida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.Writer setCharacterStream(long pos)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *pos*  
  
 A posição em que a gravação deve ser iniciada no objeto CLOB.  
  
## <a name="return-value"></a>Valor retornado  
 Um fluxo no qual os caracteres Unicode codificados podem ser gravados.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método setCharacterStream é especificado pelo método setCharacterStream na interface do CLOB.  
  
 Os dados de caractere no CLOB são substituídos pelo gravador, iniciando na posição especificada, e podem ultrapassar o comprimento inicial do CLOB. A especificação de um valor posição +1 acrescentará caracteres. A especificação de um valor posição +2 ou maior (ou zero ou menos) lançará um erro de posição.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
