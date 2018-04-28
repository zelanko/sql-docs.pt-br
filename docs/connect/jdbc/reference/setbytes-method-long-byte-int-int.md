---
title: Método (long, byte, int, int) setBytes | Microsoft Docs
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
- SQLServerBlob.setBytes (long.byte[], int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7def226c-b211-459e-8c1a-08592d75d4a4
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 04162acd8f204306d60b5af73637a5835b818861
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="setbytes-method-long-byte-int-int"></a>Método (long, byte, int, int) setBytes
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Grava toda ou parte da matriz de bytes fornecida no BLOB iniciando na posição, no deslocamento e no comprimento determinados e, em seguida, retorna o número de bytes gravados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes,  
                    int offset,  
                    int len)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *POS*  
  
 A posição (baseada em 1) no BLOB em que a gravação de dados é iniciada.  
  
 *bytes*  
  
 A matriz de bytes a ser gravada no BLOB.  
  
 *offset*  
  
 O deslocamento de bytes onde iniciar a leitura de dados de matriz a **bytes** matriz.  
  
 *len*  
  
 O número de bytes que tentará ser lido da matriz de bytes no BLOB.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** que contém o número de bytes gravados.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 Esse método setBytes é especificado pelo método setBytes na interface Java.SQL.  
  
 Dados são substituídos iniciando na posição especificada e podem ultrapassar o comprimento inicial do BLOB. A especificação de valores posição+1 acrescentará bytes. A transmissão de um valor posição+2 ou maior (ou zero ou menos) lançará um erro de posição. Passando um comprimento zero **bytes** matriz retornará zero, pois nenhum byte foi gravado.  
  
## <a name="see-also"></a>Consulte também  
 [Método setBytes &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [Métodos SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [Membros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Classe SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
