---
description: Método isSparseColumnSet (SQLServerResultSetMetaData)
title: Método isSparseColumnSet (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ac363670-78ae-49f1-aeda-4fba3329a258
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86fbbcdc34259e6b3d783d34ca77af57bcfba89f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433368"
---
# <a name="issparsecolumnset-method-sqlserverresultsetmetadata"></a>Método isSparseColumnSet (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica se uma coluna em um conjunto de resultados é um conjunto de colunas esparsas.  
  
## <a name="syntax"></a>Sintaxe  
  
```scr  
public boolean isSparseColumnSet(int column)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *column*  
  
 O índice (base um) da coluna.  
  
## <a name="return-value"></a>Valor de retorno  
 **true** se uma coluna em um conjunto de resultados for um conjunto de colunas esparsas, caso contrário, **false**.  
  
## <a name="remarks"></a>Comentários  
 Esse método não recupera informações do banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [SQLServerResultSetMetaData Methods](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Membros SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Classe SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
