---
title: Classe SQLServerParameterMetaData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 546290e0-9411-4a2b-aa36-61251e70e9cf
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04b9ff9c4e68c568d2f2c685c6f9dcac0d9d678b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverparametermetadata-class"></a>Classe SQLServerParameterMetaData
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa os metadados para parâmetros de instrução preparada.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** java.lang.Object  
  
 **Implementa:** Java.SQL. parametermetadata  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerParameterMetaData  
```  
  
## <a name="remarks"></a>Remarks  
 Para recuperar metadados de parâmetro, as instruções preparadas são executadas com SET FMT ONLY. As instruções que podem ser chamadas chamam call sp_sproc_columns para recuperar nomes e metadados para os parâmetros de procedimento.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Referência da API do Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
