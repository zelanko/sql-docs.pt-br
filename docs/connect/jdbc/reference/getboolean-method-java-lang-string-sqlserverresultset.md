---
title: Método getBoolean (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBoolean (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ba98a27b-722d-4904-ac65-0f082fde1fe6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b9ba6e530942751521ef149a4fa53c4c84ab158
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926395"
---
# <a name="getboolean-method-javalangstring-sqlserverresultset"></a>Método getBoolean (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o valor do nome da coluna designada na linha atual do objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como um **booliano** na linguagem de programação Java.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean getBoolean(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *columnName*  
  
 Uma **Cadeia de Caracteres** que contém o nome da coluna.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **booliano**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método getBoolean é especificado pelo método getBoolean na interface java.sql.ResultSet.  
  
 Esse método tem suporte apenas em tipos de dados numéricos e de caractere. Ele converte os valores "1", 1 e "**true**" em **true** e os valores "0", 0 e "**false**" em **false**. Para todos os outros valores o comportamento é indefinido.  
  
## <a name="see-also"></a>Consulte Também  
 [Método getBoolean &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getboolean-method-sqlserverresultset.md)   
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
