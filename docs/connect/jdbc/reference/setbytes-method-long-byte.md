---
title: setBytes (long, byte) do método | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerBlob.setBytes (long.byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ffb8f107-0f9d-4410-957f-62b718e1e872
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cdb1b7185d60f474d180143fe6d78dc9fd2fa42b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="setbytes-method-long-byte"></a>setBytes (long, byte) do método
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Grava a matriz de bytes fornecida no BLOB iniciando na posição determinada e, em seguida, retorna o número de bytes gravados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *POS*  
  
 A posição (base 1) no BLOB no qual iniciar a gravação de dados.  
  
 *bytes*  
  
 A matriz de bytes a ser gravada no BLOB.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **longo** valor que especifica o número de bytes gravados.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método setBytes é especificado pelo método setBytes na interface Java.SQL.  
  
 Os dados são substituídos iniciando na posição especificada e podem ultrapassar o comprimento inicial do BLOB. A especificação de valores posição+1 acrescentará bytes. A transmissão de um valor posição+2 ou maior (ou zero ou menos) lançará um erro de posição. Passando um comprimento zero **bytes** matriz retornará zero, pois nenhum byte foi gravado.  
  
## <a name="see-also"></a>Consulte também  
 [Método setBytes &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
