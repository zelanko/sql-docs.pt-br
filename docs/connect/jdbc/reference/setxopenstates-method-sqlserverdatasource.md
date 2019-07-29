---
title: Método setXopenStates (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9723591f-e987-426f-b70a-07f5c70dc094
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e63dbb2ef8864c07bf1deb58e99a08ea70fafdf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972058"
---
# <a name="setxopenstates-method-sqlserverdatasource"></a>Método setXopenStates (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um valor **booliano** que indica se a conversão de estados SQL em estados em conformidade com XOPEN está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setXopenStates(boolean xopenStates)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *xopenStates*  
  
 **true** se a conversão de Estados SQL em Estados compatíveis com XOPEN estiver habilitada. Caso contrário, **false**.  
  
## <a name="remarks"></a>Remarks  
 Se a propriedade xopenStates for definida como **true**, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] converterá estados de SQL em estados em conformidade com o XOPEN. O padrão é **false**, que faz o driver JDBC gerar os códigos de estado SQL 99. Se xopenStates não for definido, o método **getXopenStates** retornará o valor padrão [false](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
