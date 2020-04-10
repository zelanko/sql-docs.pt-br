---
title: Método updateBytes (int, byte) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBytes (int, byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 625f48ba-53d0-45a6-8fcb-643f1e0cbe8a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4448eb96ab1b9678fffaa1fdc8a6071c7b89c7da
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928771"
---
# <a name="updatebytes-method-int-byte"></a>Método updateBytes (int, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com uma matriz de valores de **byte** dados no índice da coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateBytes(int index,  
                        byte[] x)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *index*  
  
 Um **int** que indica o índice de coluna.  
  
 *x*  
  
 Uma matriz de valores **byte**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateBytes é especificado pelo método updateBytes na interface java.sql.ResultSet.  
  
 Em uma versão anterior do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], era possível usar o SQLServerResultSet.updateBytes para converter valores entre matrizes de bytes e o tipo de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**date**, **time**, **datetime2** ou **datetimeoffset**. Agora, ao usar esse método com esses tipos de dados, ocorrerá uma exceção indicando que não há suporte para a conversão.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateBytes &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
