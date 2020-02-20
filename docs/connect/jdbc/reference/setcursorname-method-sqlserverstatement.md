---
title: Método setCursorName (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setCursorName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3f3ec4f2-103a-4e16-9206-c5bd8639f946
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f743ddb27b079a4b98d5e00c8ab378a5a6859a1
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67974508"
---
# <a name="setcursorname-method-sqlserverstatement"></a>Método setCursorName (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o nome do cursor SQL como a cadeia de caracteres especificada, que será usada por métodos de execução subsequentes.  
  
> [!NOTE]  
>  No momento, este método não é compatível com [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Chamar este método não tem nenhum efeito.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setCursorName(java.lang.String name)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *name*  
  
 Uma **String** que contém o nome do cursor.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setCursorName é especificado pelo método setCursorName na interface java.sql.Statement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
