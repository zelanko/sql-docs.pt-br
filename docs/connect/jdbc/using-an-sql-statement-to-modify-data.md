---
title: Usando uma instrução SQL para modificar dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4704199b-c0ae-4c77-8a2e-6963715b4ffb
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0d02d5187e869eb626cfddde9e12bcf55feed51a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32851381"
---
# <a name="using-an-sql-statement-to-modify-data"></a>Usando uma instrução SQL para modificar dados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para modificar os dados contidos em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados usando uma instrução SQL, você pode usar o [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) método o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) classe. O método executeUpdate passar a instrução SQL para o banco de dados para processamento e, em seguida, retornar um valor que indica o número de linhas afetadas.  
  
 Para fazer isso, você deve primeiro criar um objeto SQLServerStatement usando o [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) método o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe.  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função, é construída uma instrução SQL que adiciona novos dados à tabela e a instrução é executada e o valor de retorno é exibido.  
  
 [!code[JDBC#UsingSQLToModifyData1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_1_1.java)]  
  
> [!NOTE]  
>  Se você deve usar uma instrução SQL que contém parâmetros para modificar os dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados, você deve usar o [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md) método o [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) classe.  
>   
>  Se a coluna em que estiver tentando inserir dados contiver caracteres especiais como espaços, você deverá fornecer os valores a serem inseridos, mesmo se forem valores padrão. Se isso não acontecer, haverá falha na operação.  
>   
>  Se você quiser que o driver JDBC retorne todas as contagens de atualização, inclusive contagens de atualização retornadas por gatilhos que possam ter sido acionados, defina a propriedade da cadeia de conexão lastUpdateCount como "false". Para obter mais informações sobre a propriedade lastUpdateCount, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Usando instruções com SQL](../../connect/jdbc/using-statements-with-sql.md)  
  
  
