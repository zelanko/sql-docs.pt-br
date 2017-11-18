---
title: Classe SQLServerResultSet | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eaffcff1-286c-459f-83da-3150778480c9
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ac9db37012a51c8ba365b22dd7e56b30ae5b5b6d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverresultset-class"></a>Classe SQLServerResultSet
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa um conjunto de resultados JDBC.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Implementa:** [ISQLServerResultSet](../../../connect/jdbc/reference/isqlserverresultset-interface.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final class SQLServerResultSet  
```  
  
## <a name="remarks"></a>Comentários  
 Há dois tipos de conjuntos de resultados: lado do cliente e lado do servidor.  
  
 Os conjuntos de resultados do lado do cliente são usados quando os resultados cabem na memória de processo do cliente. Esses resultados fornecem o melhor desempenho e são lidos pelo [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] integralmente no banco de dados. Esses conjuntos de resultados não impõem carga adicional ao banco de dados, acarretando a sobrecarga da criação de cursores do lado do servidor. No entanto, esses tipos de conjuntos de resultados não podem ser atualizados.  
  
 Os conjuntos de resultados do lado do servidor podem ser usados quando os resultados não cabem na memória de processo do cliente ou quando o conjunto de resultados deve ser atualizável. Com esse tipo de conjunto de resultados, o driver JDBC cria um cursor do lado do servidor e busca linhas do conjunto de resultados de maneira transparente à medida que o usuário o percorre.  
  
 A classe SQLServerResultSet fornece muitos métodos para permitir atualizar o conjunto de resultados com qualquer tipo de dados Java nativo e muitos tipos de objeto Java.  
  
 Esta classe dá suporte ao desencapsulamento para a classe SQLServerResultSet, a interface de ISQLServerResultSet e a interface resultset. Para obter mais informações, consulte [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Referência da API do Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  

