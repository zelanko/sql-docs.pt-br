---
title: Lendo exemplo de dados grande | Microsoft Docs
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
ms.assetid: 6c986144-3854-4352-8331-e79eccbefc28
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1898eb29b5c2e335fa355b43d8037ba9b4b2c910
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="reading-large-data-sample"></a>Lendo exemplo de dados grande
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Isso [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aplicativo de exemplo demonstra como recuperar um valor de coluna única grande de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] banco de dados usando o [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) método.  
  
 O arquivo de código deste exemplo chama-se readLargeData.java e pode ser encontrado neste local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \samples\adaptive  
  
## <a name="requirements"></a>Requisitos  
 Para executar este aplicativo de exemplo, você precisará acessar o [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] banco de dados de exemplo. Também será necessário definir o classpath para incluir o arquivo sqljdbc.jar ou o arquivo sqljdbc4.jar. Se no classpath faltar uma entrada para sqljdbc.jar ou sqljdbc4.jar, o aplicativo de exemplo lançará a exceção comum "Class not found". Para obter mais informações sobre como definir o classpath, consulte [usando o Driver JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes sqljdbc.jar e sqljdbc4.jar a serem usados, dependendo das configurações preferenciais do JRE (Java Runtime Environment). Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, o código de exemplo faz uma conexão para o [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] banco de dados. Em seguida, o código de exemplo cria dados de exemplo e atualiza a tabela Production.Document usando uma consulta parametrizada.  
  
 Além disso, o código de exemplo demonstra como obter o modo de buffer adaptável usando o [getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) método o [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) classe. Observe que, a partir da versão 2.0 do driver JDBC, a propriedade de conexão responseBuffering é definida por padrão como "adaptável".  
  
 Em seguida, usando uma instrução SQL com o [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) do objeto, o código de exemplo executa a instrução SQL e coloca os dados retornados em uma [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
 Finalmente, o código de exemplo itera pelas linhas de dados que estão contidas no conjunto de resultados e usa o [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) método acesse alguns dos dados que ele contém.  
  
 [!code[JDBC#UsingAdaptiveBuffering1](../../../connect/jdbc/codesnippet/Java/reading-large-data-sample_1.java)]  
  
## <a name="see-also"></a>Consulte também  
 [Manipular dados grandes](../../../connect/jdbc/working-with-large-data.md)  
  
  
