---
title: Método updateBinaryStream (int, java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1db3a975-c108-45d1-8c0d-14a094f391bd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ee42a7b0941fb3d485aae708a709a4f741d9825
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782864"
---
# <a name="updatebinarystream-method-int-javaioinputstream"></a>Método updateBinaryStream (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor de fluxo binário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateBinaryStream(int columnIndex,  
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
 Esse método updateBinaryStream é especificado pelo método updateBinaryStream na interface do resultset.  
  
 Usando esse método para o **imagem**, **texto**, e **ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de dados podem afetar o desempenho.  
  
 Esse método passa bytes de um objeto InputStream para colunas binárias [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] selecionadas do como binary, varbinary, varbinary(max), image, xml e udt. Não há suporte para a atualização de colunas de caracteres nesse método. Para atualizar colunas de caracteres com um InputStream, use o método [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateBinaryStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
