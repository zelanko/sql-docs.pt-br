---
title: Método setSelectMethod (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setSelectMethod
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7934276d-5ac9-4cbc-a2a0-2c65c93733ac
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c48aabcb618ba16c0769210903318b0d386d941d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66767846"
---
# <a name="setselectmethod-method-sqlserverdatasource"></a>Método setSelectMethod (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o tipo de cursor padrão que é usado em todos os conjuntos de resultados criados com o objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setSelectMethod(java.lang.String selectMethod)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *selectMethod*  
  
 Um valor **String** que contém o tipo de cursor padrão.  
  
## <a name="remarks"></a>Remarks  
 O selectMethod é o tipo de cursor padrão que é usado para um conjunto de resultados. Essa propriedade é útil quando você está lidando com conjuntos de resultados grandes e não deseja armazenar o conjunto de resultados inteiro na memória no lado do cliente. Ao definir a propriedade como "cursor", você pode criar um cursor do lado do servidor que pode buscar partes menores de dados por vez. Se a propriedade selectMethod não for definida, [getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md) retornará o valor padrão "direto".  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
