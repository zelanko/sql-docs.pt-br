---
title: Método getSelectMethod (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getSelectMethod
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b6255d2e-0028-474a-afa8-553ef092243e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4a9a4a0a3f05e6f5bd8bfe8fbcb111a9ed4208f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704054"
---
# <a name="getselectmethod-method-sqlserverdatasource"></a>Método getSelectMethod (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o tipo de cursor padrão usado em todos os conjuntos de resultados criados com o objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getSelectMethod()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um valorque contém o tipo de cursor padrão.  
  
## <a name="remarks"></a>Remarks  
 A propriedade selectMethod especifica o tipo de cursor padrão que é usado para um conjunto de resultados. Essa propriedade é útil quando você está lidando com conjuntos de resultados grandes e não deseja armazenar o conjunto de resultados inteiro na memória no lado do cliente. Ao definir a propriedade como "cursor", você pode criar um cursor do lado do servidor que pode buscar partes menores de dados por vez. Se a propriedade selectMethod não for definida, getSelectMethod retornará o valor padrão "direto".  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
