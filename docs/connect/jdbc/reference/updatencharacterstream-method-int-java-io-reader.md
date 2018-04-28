---
title: Método updateNCharacterStream (int, Java.IO. Reader) | Microsoft Docs
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
ms.assetid: fc746413-bdbf-4109-aee0-385a1270c847
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6b7d29d827fff4697eff6d3b6d9ed9f8d9afe41a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="updatencharacterstream-method-int-javaioreader"></a>Método updateNCharacterStream (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor de fluxo de caracteres.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateNCharacterStream(int columnIndex,  
                                  java.io.Reader x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice da coluna.  
  
 *x*  
  
 Um objeto do leitor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateNCharacterStream é especificado pelo método updateNCharacterStream na interface Java.SQL. resultset.  
  
 Esse método passa caracteres Unicode de um objeto do leitor selecionado **nchar**, **nvarchar (max)**, **ntext** e **xml** colunas. O uso em outras colunas de tipo de dados lançará uma exceção.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateNCharacterStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
