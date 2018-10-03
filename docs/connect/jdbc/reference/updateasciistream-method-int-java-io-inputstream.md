---
title: Método (java.io.InputStream) updateAsciiStream | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1dcc3d4f-ae30-45c0-afad-a531358807af
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0f8feed0894a21dacc43fb27f5d39fd961093b1e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47793750"
---
# <a name="updateasciistream-method-int-javaioinputstream"></a>Método updateAsciiStream (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor de fluxo ASCII.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateAsciiStream(int columnIndex,  
                              java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnIndex*  
  
 Um **int** que indica o índice de coluna.  
  
 *x*  
  
 Um objeto InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateAsciiStream é especificado pelo método updateAsciiStream na interface do resultset.  
  
 Esse método passa caracteres ASCII (bytes) de um objeto InputStream para colunas de caracteres conversíveis, que são o intervalo ASCII [0x00 – 0x7F] do Unicode e as páginas de código 874, 932, 936, 949, 950 e 1250 a 1258. Esse método executa uma conversão na página de agrupamento de destino. A tentativa de atualizar uma coluna de destino não conversível fará com que uma exceção seja lançada. Para colunas binárias, são passados bytes brutos.  
  
 Usando esse método para o **imagem**, **texto**, e **ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de dados podem afetar o desempenho.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateAsciiStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
