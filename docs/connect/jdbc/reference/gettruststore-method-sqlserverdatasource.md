---
title: Método getTrustStore (SQLServerDataSource) | Microsoft Docs
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
apiname:
- getTrustStore Method (SQLServerDataSource)
apilocation:
- getTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 8f5850e4-8627-49a8-ba0e-b1f4014322a5
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5035c150e0e66b55893397d2d840a5a3239b51c8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="gettruststore-method-sqlserverdatasource"></a>Método getTrustStore (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o caminho (inclusive o nome do arquivo) para o arquivo trustStore do certificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getTrustStore()  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** que contém o caminho (incluindo o nome do arquivo) para o arquivo trustStore do certificado ou nulo se nenhum valor for definido.  
  
## <a name="remarks"></a>Remarks  
 Se a propriedade trustStore não for definida, o [getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md) método retornará nulo.  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
