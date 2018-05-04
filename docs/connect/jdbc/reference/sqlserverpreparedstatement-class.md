---
title: Classe SQLServerPreparedStatement | Microsoft Docs
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
ms.assetid: a8481c06-fbba-432b-8c69-4f4619c20ad4
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cffeadf5a5e7085e81349516dd8eb9393c937c81
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverpreparedstatement-class"></a>Classe SQLServerPreparedStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa a implementação básica da funcionalidade de instrução preparada JDBC.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** SQLServerStatement  
  
 **Implementa:** [ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerPreparedStatement fornece métodos que permitem fornecer parâmetros como qualquer tipo de Java nativo e muitos tipos de objeto Java. SQLServerPreparedStatement prepara uma instrução usando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **sp_prepare** procedimento armazenado e reutiliza o identificador da instrução retornada para cada subsequentes em execução da instrução, normalmente usando diferentes parâmetros fornecidos pelo usuário.  
  
 SQLServerPreparedStatement oferece suporte ao envio em lote, onde um conjunto de instruções preparadas é executado em um único banco de dados ida e volta, para melhorar o desempenho de tempo de execução.  
  
 Esta classe dá suporte ao desencapsulamento para a classe SQLServerPreparedStatement, interface ISQLServerPreparedStatement, interface PreparedStatement e as classes e interfaces suportadas por SQLServerStatement para desencapsulamento. Para obter mais informações, consulte [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Referência da API do Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
