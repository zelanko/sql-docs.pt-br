---
title: Lendo exemplo de dados grandes | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6c986144-3854-4352-8331-e79eccbefc28
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 51f1925c55fc3ece88aa8354afb181af8aec38ce
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278629"
---
# <a name="reading-large-data-sample"></a>Lendo exemplo de dados grande
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Este aplicativo de exemplo do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] demonstra como recuperar um valor grande de coluna única de um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] usando o método [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md).  
  
 O arquivo de código desta amostra chama-se ReadLargeData.java e pode ser encontrado no seguinte local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \samples\adaptive  
  
## <a name="requirements"></a>Requisitos  
 Para executar este aplicativo de exemplo, você precisará ter acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Também defina o classpath para incluir o arquivo de jar mssql-jdbc. Para obter mais informações sobre como definir o classpath, consulte [usando o Driver JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes mssql-jdbc a serem usados de acordo com suas configurações preferenciais do JRE (Java Runtime Environment). Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, o código de exemplo faz uma conexão com o banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Em seguida, o código de exemplo cria dados de exemplo e atualiza a tabela Production.Document usando uma consulta parametrizada.  
  
 Além disso, o código de exemplo demonstra como obter o modo de buffer adaptável usando o método [getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) da classe [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md). Observe que, a partir da versão 2.0 do driver JDBC, a propriedade de conexão responseBuffering é definida por padrão como "adaptável".  
  
 Em seguida, usando uma instrução SQL com o objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), o código de exemplo executa a instrução SQL e coloca os dados retornados em um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
 Por fim, o código de exemplo itera pelas linhas de dados do conjunto de resultados e usa o método [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) para acessar alguns dos dados.  
  
 [!code[JDBC#UsingAdaptiveBuffering1](../../../connect/jdbc/codesnippet/Java/reading-large-data-sample_1.java)]  
  
## <a name="see-also"></a>Consulte Também  
 [Manipular dados grandes](../../../connect/jdbc/working-with-large-data.md)  
  
  
