---
title: Método setTrustStorePassword (SQLServerDataSource) | Microsoft Docs
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
- setTrustStorePassword Method (SQLServerDataSource)
apilocation:
- setTrustStorePassword Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: fa87cbde-71cc-4f21-bc07-f8ba2b6a0a3f
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2dbd22d01c5c4523fdd04a12d68b9c716fd8643d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32847001"
---
# <a name="settruststorepassword-method-sqlserverdatasource"></a>Método setTrustStorePassword (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define a senha usada para verificar a integridade dos dados de trustStore.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setTrustStorePassword(java.lang.String trustStorePassword)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *trustStorePassword*  
  
 Um **cadeia de caracteres** que contém a senha que é usada para verificar a integridade dos dados de trustStore.  
  
## <a name="remarks"></a>Remarks  
 Uma propriedade trustStorePassword pode ser especificada juntamente com a propriedade trustStore e seu valor é usado para verificar a integridade do arquivo trustStore.  
  
 Se a propriedade trustStore for definida, mas a propriedade trustStorePassword não for definida, a integridade de trustStore não será verificada.  
  
 Quando as propriedades trustStore e trustStorePassword não forem especificadas, o driver usará as propriedades de sistema da máquina Virtual Java (JVM), "javax.NET.SSL. truststore" e "javax.NET.SSL". Se a propriedade do sistema "javax.net.ssl.trustStorePassword" não for especificada, a integridade de trustStore não será verificada.  
  
 Se a propriedade trustStore não estiver definida, mas a propriedade trustStorePassword estiver, o driver JDBC usará o arquivo especificado por "javax.net.ssl.trustStore" como um repositório confiável e a integridade dele será verificada com trustStorePassword. Isso pode ser necessário quando o aplicativo cliente não quiser armazenar a senha na propriedade do sistema JVM.  
  
 Para obter mais informações, consulte [definindo as propriedades de Conexão](../../../connect/jdbc/setting-the-connection-properties.md).  
  
 A partir do JDBC Driver 3.0, ao definir SQLServerDataSource.setTrustStorePassword antes de associar as propriedades da fonte de dados, você deverá chamar SQLServerDataSource.setTrustStorePassword antes de estabelecer a conexão. Para obter mais informações, consulte [Getreference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md).  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
