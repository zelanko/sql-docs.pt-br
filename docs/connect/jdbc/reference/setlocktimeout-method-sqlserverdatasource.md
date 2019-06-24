---
title: Método setLockTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLockTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10dca5aa-1851-4326-9ae9-7a8430d12d11
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 32f61572dca7124e552a9d40497a3385bc243b31
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66790471"
---
# <a name="setlocktimeout-method-sqlserverdatasource"></a>Método setLockTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define um valor **int** que indica o número de milissegundos que o banco de dados precisa aguardar antes de informar um tempo limite de bloqueio.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setLockTimeout(int lockTimeout)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *lockTimeout*  
  
 Um valor **int** que contém o número de milissegundos de espera.  
  
## <a name="remarks"></a>Remarks  
 O tempo limite de bloqueio é o número de milissegundos de espera antes de o banco de dados informar um tempo limite de bloqueio. O valor padrão de -1 significa que ele aguardará por tempo indefinido. Se for especificado, esse valor será o padrão para todas as instruções na conexão.  
  
> [!NOTE]  
>  Um valor de 0 significa que não haverá espera. Se a propriedade lockTimeout não estiver definida, o método [getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md) retornará o valor padrão de -1.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
