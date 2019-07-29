---
title: Método getLockTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLockTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 676094e9-ec18-4524-9b21-1f9c5b16dd52
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f9c94e0c69bd528f1c579f41319a4db18b7d4d3c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982565"
---
# <a name="getlocktimeout-method-sqlserverdatasource"></a>Método getLockTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um valor **int** que indica o número de milissegundos que o banco de dados esperará antes de informar um tempo limite de bloqueio.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getLockTimeout()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Um valor **int** que contém o número de milissegundos que o banco de dados esperará.  
  
## <a name="remarks"></a>Remarks  
 O tempo limite de bloqueio é o número de milissegundos de espera antes de o banco de dados informar um tempo limite de bloqueio. O valor padrão de -1 significa que ele aguardará por tempo indefinido. Se for especificado, esse valor será o padrão para todas as instruções na conexão.  
  
> [!NOTE]  
>  Um valor de 0 significa que não haverá espera. Se a propriedade lockTimeout não estiver definida, o método getLockTimeout retornará o valor padrão de -1.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
