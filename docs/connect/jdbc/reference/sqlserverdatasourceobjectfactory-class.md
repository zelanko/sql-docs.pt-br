---
title: Classe SQLServerDataSourceObjectFactory | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b616632b-5987-470d-b36c-b22fa9213145
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 135dad379d0642059af19060b9df27baec0e3e24
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47615184"
---
# <a name="sqlserverdatasourceobjectfactory-class"></a>Classe SQLServerDataSourceObjectFactory
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa um alocador de objeto para materializar fontes de dados da JNDI (Java Naming and Directory Interface).  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** java.lang.Object  
  
 **Implementa:** javax.naming.spi.ObjectFactory  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerDataSourceObjectFactory  
```  
  
## <a name="remarks"></a>Remarks  
 Esse método é herdado por todas as classes de fonte de dados. Como parte de seu suporte para a interface Referenceable, o [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] expõe essa classe que implementa um ObjectFactory. Servidores de aplicativos Java chamarão getReference em uma classe de fonte de dados e isso criará um objeto Reference que internamente usa o nome de classe como sua fábrica de classes.  
  
 Quando o servidor de aplicativos Java tiver que remover o objeto de referência a, ele cria uma instância do objeto SQLServerDataSourceObjectFactory e chamadas a [getObjectInstance](../../../connect/jdbc/reference/getobjectinstance-method-sqlserverdatasourceobjectfactory.md) método, passando o objeto de referência, como recupere a instância de fonte de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [Referência de API do JDBC Driver](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
