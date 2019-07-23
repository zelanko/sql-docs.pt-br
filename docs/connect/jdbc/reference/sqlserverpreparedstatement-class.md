---
title: Classe SQLServerPreparedStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8481c06-fbba-432b-8c69-4f4619c20ad4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 96d2e01d4ca8d38b79906ee31cc5b50df0d8cb25
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970763"
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
 SQLServerPreparedStatement fornece métodos que permitem que você forneça parâmetros como qualquer tipo nativo do Java e vários tipos de objetos Java. SQLServerPreparedStatement prepara uma instrução usando o procedimento armazenado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **sp_prepare** e, em seguida, reutiliza a barra de instrução retornada para cada execução subsequente da instrução, normalmente usando diferentes parâmetros fornecidos pelo usuário.  
  
 SQLServerPreparedStatement é compatível com o processamento em lotes, em que um conjunto de instruções preparadas é executado em uma viagem de ida e volta do banco de dados individual, para melhorar o desempenho do tempo de execução.  
  
 Essa classe dá suporte à desencapsulamento da classe SQLServerPreparedStatement, Interface ISQLServerPreparedStatement, interface java. Sql. PreparedStatement e às classes e interfaces com suporte do SQLServerStatement para desencapsulamento. Para obter mais informações, consulte [wrappers e interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Referência de API do JDBC Driver](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
