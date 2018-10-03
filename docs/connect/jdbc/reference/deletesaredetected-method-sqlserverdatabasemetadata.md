---
title: Método deletesAreDetected (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.deletesAreDetected
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 73f3d994-bbd7-43d2-8b64-50057e278983
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20007b2918d8e0b8675c082edc5040c092973579
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806086"
---
# <a name="deletesaredetected-method-sqlserverdatabasemetadata"></a>Método deletesAreDetected (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se a exclusão de uma linha visível pode ser detectada ou não com a chamada do método [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) da classe [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean deletesAreDetected(int type)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *tipo*  
  
 Um **int** que indica o tipo do conjunto de resultados, que pode ser um dos valores a seguir, conforme definido em java.sql.ResultSet ou SQLServerResultSet:  
  
## <a name="javasqlresultset-types"></a>Tipos java.sql.ResultSet  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>Tipos SQLServerResultSet  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
## <a name="return-value"></a>Valor retornado  
 **True** se um buraco substitui a linha excluída. **False** se a linha excluída for removida.  
  
 Ao usar o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] com um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], este método retorna **true** para cursores de TYPE_SS_SCROLL_KEYSET e **false** para todos os outros tipos de conjunto de resultados.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 Esse método deletesAreDetected é especificado pelo método deletesAreDetected na interface DatabaseMetadata.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] detecta linhas excluídas para todos os tipos de cursores atualizáveis, embora a detecção seja transiente para cursores dinâmicos e de avanço.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
