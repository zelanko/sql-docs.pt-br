---
title: Método (Java.IO. InputStream) updateBinaryStream | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 56883144-26a0-4f45-ad36-4f616369af3e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e228e4914fb9fd5790450d5f246592581bf0397a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream"></a>Método updateBinaryStream (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor de fluxo binário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
                               java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnLabel*  
  
 Um **cadeia de caracteres** que contém o rótulo da coluna.  
  
 *x*  
  
 Um objeto InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método updateBinaryStream é especificado pelo método updateBinaryStream na interface Java.SQL. resultset.  
  
 Usando esse método para o **imagem**, **texto**, e **ntext** tipos de dados do SQL Server podem afetar o desempenho.  
  
 Esse método passa bytes de um objeto InputStream selecionado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] colunas binárias, como binary, varbinary, varbinary (max), imagem, xml e udt. Não há suporte para a atualização de colunas de caracteres nesse método. Para atualizar colunas de caracteres com um InputStream, use o [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) método.  
  
## <a name="see-also"></a>Consulte também  
 [Método updateBinaryStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
