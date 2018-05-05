---
title: Método getLockTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLockTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 676094e9-ec18-4524-9b21-1f9c5b16dd52
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: feac1b27f0a76492083b4cfcdb63968ff09ac5af
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getlocktimeout-method-sqlserverdatasource"></a>Método getLockTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna um **int** valor que indica o número de milissegundos que o banco de dados aguardará antes de relatar um tempo limite de bloqueio.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public int getLockTimeout()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **int** valor que contém o número de milissegundos que o banco de dados esperará.  
  
## <a name="remarks"></a>Remarks  
 O tempo limite de bloqueio é o número de milissegundos de espera antes de o banco de dados informar um tempo limite de bloqueio. O valor padrão de -1 significa que ele aguardará por tempo indefinido. Se especificado, esse valor será o padrão para todas as instruções sobre a conexão.  
  
> [!NOTE]  
>  Um valor de 0 significa que não haverá espera. Se a propriedade lockTimeout não estiver definida, o método getLockTimeout retornará o valor padrão de -1.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
