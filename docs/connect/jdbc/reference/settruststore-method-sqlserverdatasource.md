---
title: "Método setTrustStore (SQLServerDataSource) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- setTrustStore Method (SQLServerDataSource)
apilocation:
- setTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: bab5485d-4547-426c-adbe-44e2b5702d1d
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3e6de008468da81facf98c039457f9248ddddc49
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="settruststore-method-sqlserverdatasource"></a>Método setTrustStore (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define o caminho (inclusive o nome de arquivo) para o arquivo trustStore do certificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setTrustStore(java.lang.String trustStore)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *trustStore*  
  
 Um **cadeia de caracteres** que contém o caminho (incluindo o nome do arquivo) para o arquivo trustStore do certificado.  
  
## <a name="remarks"></a>Comentários  
 Se a propriedade trustStore for especificado ou definido como null, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] dependerá das regras para determinar qual repositório de certificados para usar de pesquisa da fábrica do Gerenciador de confiança. SunX509 TrustManagerFactory padrão tenta localizar o material de confiança nos locais a seguir nesta ordem:  
  
-   1. Um arquivo especificado pela propriedade do sistema JVM (Máquina Virtual Java) "javax.net.ssl.trustStore".  
  
-   2. "\<java-home >/lib/security/jssecacerts" arquivo.  
  
-   3. "\<java-home >/lib/security/cacerts" arquivo.  
  
 Para obter mais informações, consulte a documentação da interface do SunX509 TrustManager no site da Sun Microsystems.  
  
 Se a propriedade trustStore for definida como uma cadeia de caracteres ou uma cadeia de caracteres vazia "", o driver usará esse valor para localizar o arquivo trustStore para validar o certificado SSL do servidor.  
  
 Uma propriedade trustStorePassword pode ser especificada junto com a propriedade trustStore e seu valor é usado para abrir o arquivo trustStore. Para obter mais informações, consulte [setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md).  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
