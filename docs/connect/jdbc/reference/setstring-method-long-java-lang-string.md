---
title: Método setString (long, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.setString (long, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1b2190e9-5ace-497a-8554-0e913ea9b0cb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8e3e1dfb6447907caa0bd5970df47fe9989b4aab
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67972634"
---
# <a name="setstring-method-long-javalangstring"></a>Método setString (long, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Grava o **String** fornecido no CLOB, começando na posição fornecida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int setString(long pos,  
                     java.lang.String s)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *pos*  
  
 A posição em que a gravação deve ser iniciada no CLOB.  
  
 *s*  
  
 A **cadeia de caracteres** a ser gravada no CLOB.  
  
## <a name="return-value"></a>Valor retornado  
 O número de caracteres gravados.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentários  
 Esse método setString é especificado pelo método setString na interface java.sql.Clob.  
  
 Os dados de caractere são substituídos iniciando na posição especificada e podem ultrapassar o comprimento inicial do CLOB. A especificação de um valor posição +1 acrescentará a cadeia de caracteres. A especificação de valores de posição+2 ou maiores (ou zero ou menos) causarão o lançamento de um erro de posição.  
  
## <a name="see-also"></a>Consulte Também  
 [Método setString &#40;SQLServerClob&#41;](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)   
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
