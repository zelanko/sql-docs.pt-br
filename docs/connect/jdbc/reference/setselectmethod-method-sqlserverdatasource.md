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
ms.openlocfilehash: e82bdcef16c854d0bcc1f11757b0bb2ed6030145
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67973003"
---
# <a name="setselectmethod-method-sqlserverdatasource"></a>Método setSelectMethod (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o tipo de cursor padrão que é usado em todos os conjuntos de resultados criados com o objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setSelectMethod(java.lang.String selectMethod)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *selectMethod*  
  
 Um valor **String** que contém o tipo de cursor padrão.  
  
## <a name="remarks"></a>Comentários  
 O selectMethod é o tipo de cursor padrão que é usado para um conjunto de resultados. Essa propriedade é útil quando você está lidando com conjuntos de resultados grandes e não deseja armazenar o conjunto de resultados inteiro na memória no lado do cliente. Ao definir a propriedade como "cursor", você pode criar um cursor do lado do servidor que pode buscar partes menores de dados por vez. Se a propriedade selectMethod não for definida, [getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md) retornará o valor padrão "direto".  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
