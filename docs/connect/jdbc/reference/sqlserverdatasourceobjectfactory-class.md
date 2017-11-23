---
title: Classe SQLServerDataSourceObjectFactory | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b616632b-5987-470d-b36c-b22fa9213145
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4903c8003f0eb866c2f877a2724e895d31d12409
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverdatasourceobjectfactory-class"></a>Classe SQLServerDataSourceObjectFactory
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa um alocador de objeto para materializar fontes de dados da JNDI (Java Naming and Directory Interface).  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** java.lang.Object  
  
 **Implementa:** javax.Naming.SPI. ObjectFactory  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerDataSourceObjectFactory  
```  
  
## <a name="remarks"></a>Comentários  
 Esse método é herdado por todas as classes de fonte de dados. Como parte de seu suporte para a interface Referenceable, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] expõe essa classe que implementa um ObjectFactory. Servidores de aplicativos Java chamarão getReference em uma classe de fonte de dados, e isso criará um objeto de referência que internamente usa o nome da classe como sua fábrica de classe.  
  
 Quando o servidor de aplicativos Java tiver a referência de objeto de referência, ele cria uma instância do objeto de SQLServerDataSourceObjectFactory e chama o [getObjectInstance](../../../connect/jdbc/reference/getobjectinstance-method-sqlserverdatasourceobjectfactory.md) método, passando o objeto de referência para recupere a instância de fonte de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [Referência da API do Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
