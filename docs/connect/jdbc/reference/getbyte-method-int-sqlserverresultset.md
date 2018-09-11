---
title: Método getByte (int) (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.getByte (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b22ba097-6cb8-4c5d-916b-6360dd01d2c5
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 984c18407995e577bcafac596e8a7ef94ec7eb1d
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785715"
---
# <a name="getbyte-method-int-sqlserverresultset"></a>Método getByte (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do índice da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como um **byte** na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public byte getByte(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice de coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **byte**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método getByte é especificado pelo método getByte na interface do resultset.  
  
 Esse método só é compatível com os tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que podem retornar com segurança um valor byte, como tinyint e bit. Todos os outros tipos de dados fazem com que uma exceção seja lançada.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getByte &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbyte-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
