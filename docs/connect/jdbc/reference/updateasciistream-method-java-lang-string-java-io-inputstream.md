---
description: Método updateAsciiStream (java.lang.String, java.io.InputStream)
title: Método updateAsciiStream (java.lang.String, java.io.InputStream)
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 747b0308-1ce6-4eba-bdfc-af29c21c18cf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5f42bda7c4938d1dc0a4ed3fad9bf446c63bad2d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478503"
---
# <a name="updateasciistream-method-javalangstring-javaioinputstream"></a>Método updateAsciiStream (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Atualiza a coluna designada com um valor de fluxo ASCII.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void updateAsciiStream(java.lang.String columnLabel,  
                              java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *columnLabel*  
  
 Uma **Cadeia de Caracteres** que contém o rótulo da coluna.  
  
 *x*  
  
 Um objeto InputStream.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método updateAsciiStream é especificado pelo método updateAsciiStream na interface java.sql.ResultSet.  
  
 Esse método passa caracteres ASCII (bytes) de um objeto InputStream para colunas de caracteres conversíveis, que são o intervalo ASCII [0x00 - 0x7F] do Unicode e as páginas de código 874, 932, 936, 949, 950 e 1250 a 1258. Esse método executa uma conversão na página de ordenação de destino. A tentativa de atualizar uma coluna de destino não conversível fará com que uma exceção seja lançada. Para colunas binárias, são passados bytes brutos.  
  
 O uso deste método nos tipos de dados **image**, **text** e **ntext** do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode afetar o desempenho.  
  
## <a name="see-also"></a>Consulte Também  
 [Método updateAsciiStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
