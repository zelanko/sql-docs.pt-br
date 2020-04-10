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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b4edd69c4712c1842163bcb48797edc154cc5cf
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80929031"
---
# <a name="setcharacterstream-method-sqlserverclob"></a>Método setCharacterStream (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um fluxo a ser usado para gravar um fluxo de caracteres Unicode no CLOB, iniciando na posição fornecida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.io.Writer setCharacterStream(long pos)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *pos*  
  
 A posição em que a gravação deve ser iniciada no objeto CLOB.  
  
## <a name="return-value"></a>Valor retornado  
 Um fluxo no qual os caracteres Unicode codificados podem ser gravados.  
  
## <a name="exceptions"></a>Exceções  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentários  
 Esse método setCharacterStream é especificado pelo método setCharacterStream na interface java.sql.Clob.  
  
 Os dados de caractere no CLOB são substituídos pelo gravador, iniciando na posição especificada, e podem ultrapassar o comprimento inicial do CLOB. A especificação de um valor posição +1 acrescentará caracteres. A especificação de um valor posição +2 ou maior (ou zero ou menos) lançará um erro de posição.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [Membros SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [Classe SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
