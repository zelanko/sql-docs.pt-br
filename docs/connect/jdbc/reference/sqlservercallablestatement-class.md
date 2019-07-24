---
title: Classe SQLServerCallableStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 637b56c7f64d35501be0efef30e8f2a055b5be4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971908"
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
  
## <a name="remarks"></a>Remarks  
 SQLServerCallableStatement permite especificar o nome do procedimento armazenado para chamar juntamente com os parâmetros de entrada e saída. O SQLServerCallableStatement também fornece a capacidade de recuperar o valor de status de `? = call( ?, ..)` retorno com a sintaxe.  
  
 Essa classe dá suporte à desencapsulamento da classe SQLServerCallableStatement, interface ISQLServerCallableStatement, interface java. Sql. CallableStatement e às classes e interfaces com suporte do SQLServerPreparedStatement para desencapsulamento. Para obter mais informações, consulte [wrappers e interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
 Quando um dos métodos set SQLServerCallableStatement for chamado para um tipo, se esse tipo entrar em conflito com o tipo especificado com [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md), o tipo especificado pelo último método SQLServerCallableStatement set será usado. Entretanto, isso pode gerar erros de conversão de tipos de dados incompatíveis. Se um método SQLServerCallableStatement definido não for chamado, o tipo especificado com a primeira chamada de [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) será usado.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 está de acordo com a recomendação do JDBC 4.0, a qual declara que conjuntos de resultados e contagens de atualização devem ser recuperados antes da recuperação de parâmetros OUT. Se os parâmetros OUT forem recuperados antes da conclusão do processamento do conjunto de resultados e de contagens de atualização, quaisquer conjuntos de resultados e contagens de atualização que não tiverem sido processados serão perdidos.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Referência de API do JDBC Driver](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
