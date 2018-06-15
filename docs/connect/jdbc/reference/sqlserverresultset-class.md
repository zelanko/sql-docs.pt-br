---
title: Classe SQLServerResultSet | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eaffcff1-286c-459f-83da-3150778480c9
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 671eda7647b1381feeedcf76c9cca1a81d8fc267
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32846691"
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
  
## <a name="remarks"></a>Remarks  
 Há dois tipos de conjuntos de resultados: lado do cliente e lado do servidor.  
  
 Os conjuntos de resultados do lado do cliente são usados quando os resultados cabem na memória de processo do cliente. Esses resultados fornecem o melhor desempenho e são lidos pelo [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] integralmente no banco de dados. Esses conjuntos de resultados não impõem carga adicional ao banco de dados, acarretando a sobrecarga da criação de cursores do lado do servidor. No entanto, esses tipos de conjuntos de resultados não podem ser atualizados.  
  
 Os conjuntos de resultados do lado do servidor podem ser usados quando os resultados não cabem na memória de processo do cliente ou quando o conjunto de resultados deve ser atualizável. Com esse tipo de conjunto de resultados, o driver JDBC cria um cursor do lado do servidor e busca linhas do conjunto de resultados de maneira transparente à medida que o usuário o percorre.  
  
 A classe SQLServerResultSet fornece muitos métodos para permitir atualizar o conjunto de resultados com qualquer tipo de dados Java nativo e muitos tipos de objeto Java.  
  
 Esta classe dá suporte ao desencapsulamento para a classe SQLServerResultSet, a interface de ISQLServerResultSet e a interface resultset. Para obter mais informações, consulte [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Referência da API do Driver JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
