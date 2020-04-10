---
title: Método setEscapeProcessing (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setEscapeProcessing
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6ac0682e-e04c-4fdb-893b-92408d42051e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8b19314337fd78f85ab79d186c0d0956f0ed5aaa
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922369"
---
# <a name="setescapeprocessing-method-sqlserverstatement"></a>Método setEscapeProcessing (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o modo de processamento de escape.  
  
> [!NOTE]  
>  O processamento de escape para o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] sempre está habilitado. Definir este método como false não tem nenhum efeito.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final void setEscapeProcessing(boolean enable)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *enable*  
  
 **true** para habilitar o processamento de escape. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método setEscapeProcessing é especificado pelo método setEscapeProcessing na interface java.sql.Statement.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
