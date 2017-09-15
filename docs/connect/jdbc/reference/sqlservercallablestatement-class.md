---
title: Classe SQLServerCallableStatement | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 15c8a944d4130e496c051d163c4724fe6d87f74e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlservercallablestatement-class"></a>Classe SQLServerCallableStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Permite especificar o nome do procedimento armazenado para chamar juntamente com os parâmetros de entrada e saída. Essa classe também fornece a capacidade de recuperar o valor de status de retorno com a sintaxe ? sintaxe = call( ?, ..).  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Implementa:** [ISQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
 **Estende:** [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final class SQLServerCallableStatement  
```  
  
## <a name="remarks"></a>Comentários  
 SQLServerCallableStatement permite que você especifique o nome do procedimento armazenado para chamar juntamente com os parâmetros de entrada e saídos. SQLServerCallableStatement também fornece a capacidade de recuperar o valor de status de retorno com o `? = call( ?, ..)` sintaxe.  
  
 Esta classe dá suporte ao desencapsulamento para a classe SQLServerCallableStatement, interface de ISQLServerCallableStatement, interface CallableStatement, as classes e interfaces suportadas por SQLServerPreparedStatement para desencapsulamento. Para obter mais informações, consulte [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
 Quando um dos SQLServerCallableStatement definir métodos é chamado de um tipo, se esse tipo está em conflito com o tipo especificado com [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md), o tipo especificado pelo último método definido SQLServerCallableStatement é usado. Entretanto, isso pode gerar erros de conversão de tipos de dados incompatíveis. Se um SQLServerCallableStatement definir o método não for chamado, o tipo especificado com a primeira [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) chamada é usada.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC Driver 3.0 está em conformidade com a recomendação do JDBC 4.0 que um conjunto de resultados e contagens de atualização devem ser recuperadas antes de recuperar os parâmetros de saída. Se os parâmetros OUT forem recuperados antes da conclusão do processamento do conjunto de resultados e de contagens de atualização, quaisquer conjuntos de resultados e contagens de atualização que não tiverem sido processados serão perdidos.  
  
## <a name="see-also"></a>Consulte também  
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Referência da API do Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
