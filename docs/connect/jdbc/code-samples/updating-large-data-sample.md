---
title: Atualizando exemplo de dados grandes | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76ecc05f-a77d-40a2-bab9-91a7fcf17347
caps.latest.revision: "27"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.openlocfilehash: 4820063233abe12d59ec961ee9b05a63c6547112
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="updating-large-data-sample"></a>Atualizando exemplo de dados grande
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Isso [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] aplicativo de exemplo demonstra como atualizar uma coluna grande em um banco de dados.  
  
 O arquivo de código deste exemplo chama-se updateLargeData.java e pode ser encontrado neste local:  
  
 \<*diretório de instalação*> \sqljdbc_\<*versão*>\\<*idioma*> \samples\adaptive  
  
## <a name="requirements"></a>Requisitos  
 Para executar este aplicativo de exemplo, você precisará acessar o [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] banco de dados de exemplo. Você também precisará definir o classpath para incluir o arquivo sqljdbc4.jar. Se no classpath faltar uma entrada para sqljdbc4.jar, o aplicativo de exemplo lançará a exceção comum "Class not found". Para obter mais informações sobre como definir o classpath, consulte [usando o Driver JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).  
  
> [!NOTE]  
>  O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar ou sqljdbc42.jar para serem usados dependendo das suas configurações preferidas do Java Runtime Environment (JRE). Este exemplo usa o [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) e [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) métodos, que são introduzidos na API do JDBC 4.0, para acessar os métodos de buffer de resposta específicos do driver. A fim de compilar e executar este exemplo, você precisará da biblioteca de classes sqljdbc4.jar que oferece suporte para JDBC 4.0. Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, o código de exemplo faz uma conexão para o [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] banco de dados. Em seguida, o código de exemplo cria um objeto de instrução e usa o [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) método para verificar se o objeto de instrução é um wrapper para especificado [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) classe. O [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) método é usado para acessar os métodos de buffer de resposta específicos do driver.  
  
 Em seguida, o código de exemplo define a modo como de buffer de resposta "**adaptável**" usando o [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método o [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) classe e também Demonstra como obter o modo de buffer adaptável.  
  
 Em seguida, ele executa a instrução SQL e coloca os dados retornados em um atualizável [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
 Por fim, o código de exemplo itera pelas linhas de dados que estão contidas no conjunto de resultados. Se ele encontrar um documento vazio resumo, ele usa a combinação de [updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) e [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) métodos para atualizar a linha de dados e novamente persisti-los para o banco de dados. Se já houver dados, ele usa o [getString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) método para exibir alguns dos dados que ele contém.  
  
 O comportamento padrão do driver é "**adaptável.**" No entanto, para os conjuntos de resultados atualizáveis de somente avanço e quando os dados no conjunto de resultados for maiores do que a memória de aplicativo, o aplicativo precisa definir o modo de buffer adaptável explicitamente usando o [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) classe.  
  
 [!code[JDBC#UsingAdaptiveBuffering3](../../../connect/jdbc/codesnippet/Java/updating-large-data-sample_1.java)]  
  
## <a name="see-also"></a>Consulte também  
 [Manipular dados grandes](../../../connect/jdbc/working-with-large-data.md)  
  
  
