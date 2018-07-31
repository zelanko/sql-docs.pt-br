---
title: Classe SQLServerDataSourceObjectFactory | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b616632b-5987-470d-b36c-b22fa9213145
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ecec8f58587d6a57468f8078e1f680675bede77
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38046844"
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
  
  
