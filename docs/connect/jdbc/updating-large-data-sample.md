---
title: Atualizando exemplo de dados grandes | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76ecc05f-a77d-40a2-bab9-91a7fcf17347
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: dbfb41e7a36471eedff13b0776ff811412c8e8ce
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66788290"
---
# <a name="updating-large-data-sample"></a>Atualizando exemplo de dados grande

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Este aplicativo de exemplo do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] demonstra como atualizar uma coluna grande em um banco de dados.

O arquivo de código desta amostra chama-se UpdateLargeData.java e pode ser encontrado no seguinte local:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>Requisitos

Para executar este aplicativo de exemplo, você precisará ter acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Você também precisará definir o classpath para incluir o arquivo sqljdbc4.jar. Se no classpath faltar uma entrada para sqljdbc4.jar, o aplicativo de exemplo lançará a exceção comum "Class not found". Para obter mais informações sobre como definir o classpath, consulte [usando o Driver JDBC](../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar ou sqljdbc42.jar a serem usados de acordo com suas configurações preferenciais do JRE (Java Runtime Environment). Esta amostra usa os métodos [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) e [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md), que são introduzidos na API do JDBC 4.0, para acessar os métodos de buffer de resposta específicos do driver. A fim de compilar e executar este exemplo, você precisará da biblioteca de classes sqljdbc4.jar que oferece suporte para JDBC 4.0. Para saber mais sobre qual arquivo JAR escolher, confira os [requisitos do sistema para o JDBC Driver](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Exemplo

No exemplo a seguir, o código de exemplo faz uma conexão com o banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Em seguida, o código de exemplo cria um objeto Statement e usa o método [isWrapperFor](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) para verificar se o objeto Statement é um wrapper para a classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) especificada. O método [unwrap](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) é usado para acessar os métodos de buffer de resposta específicos do driver.

Em seguida, o código de exemplo define o modo de buffer de resposta como "**adaptável**" usando o método [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) da classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) e também demonstra como obter o modo de buffer adaptável.

Em seguida, ele executa a instrução SQL e coloca os dados retornados em um objeto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) atualizável.

Por fim, o código de exemplo itera pelas linhas de dados do conjunto de resultados. Se ele localizar um resumo vazio do documento, usará a combinação dos métodos [updateString](../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) e [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) para atualizar a linha de dados e novamente persisti-la no banco de dados. Se já houver dados, usará o método [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) para exibir alguns dos dados.

O comportamento padrão do driver é"**adaptável**". Porém, para os conjuntos de resultados atualizáveis somente de avanço e quando os dados no conjunto de resultados são maiores que a memória do aplicativo, o aplicativo precisa definir o modo de buffer adaptável explicitamente usando o método [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) da classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md).

[!code[JDBC#UsingAdaptiveBuffering3](../../connect/jdbc/codesnippet/Java/updating-large-data-sample_1.java)]

## <a name="see-also"></a>Consulte Também

[Manipular dados grandes](../../connect/jdbc/working-with-large-data.md)
