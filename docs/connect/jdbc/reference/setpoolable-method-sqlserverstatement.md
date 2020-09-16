---
description: Método setPoolable (SQLServerStatement)
title: Método setPoolable (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f0f798c8-cafb-4acc-b85d-2e0059c91d92
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f75e1ffad80d1442689da6d32eafcaf74cb48fdf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458468"
---
# <a name="setpoolable-method-sqlserverstatement"></a>Método setPoolable (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Solicita que uma instrução seja colocada ou não em pool.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setPoolable(boolean poolable) throws SQLException  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *poolable*  
  
 Se **true**, solicita que a instrução seja colocada em pool. Se **false**, solicita que a instrução não seja colocada em pool.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 O valor especificado no parâmetro *poolable* é uma dica para a implementação do pool de instrução que indica se o aplicativo deseja que a instrução seja colocada em pool. O gerenciador de pools de instrução decidirá se usará a dica.  
  
 O valor do pool de uma instrução aplica-se aos caches de instrução internos implementados pelo driver e aos caches de instrução externos implementados por servidores de aplicativos e outros aplicativos.  
  
 Por padrão, um objeto SQLServerStatement não pode ser colocado em pool quando criado. Os objetos SQLServerPreparedStatement e SQLServerCallableStatement podem ser colocados em pool quando criados.  
  
 Uma [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) será gerada se esse método for chamado em uma instrução fechada.  
  
 [isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md) retorna um valor que indica se o objeto pode ser colocado em pool.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
