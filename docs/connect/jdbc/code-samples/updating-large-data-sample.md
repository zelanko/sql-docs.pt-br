---
title: Como atualizar o exemplo de dados grandes | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76ecc05f-a77d-40a2-bab9-91a7fcf17347
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bd284f6fb8021164aa3edf6aa31761b7483406e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69028265"
---
# <a name="updating-large-data-sample"></a>Atualizando o exemplo de dados grandes

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Este aplicativo de exemplo do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] demonstra como atualizar uma coluna grande em um banco de dados.

O arquivo de código desta amostra chama-se UpdateLargeData.java e pode ser encontrado no seguinte local:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>Requisitos

Para executar este aplicativo de exemplo, você precisará ter acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Defina também o classpath para incluir o arquivo sqljdbc4.jar. Se no classpath faltar uma entrada para sqljdbc4.jar, o aplicativo de exemplo lançará a exceção comum "Class not found". Para obter mais informações sobre como definir o caminho de classe, confira [Como usar o JDBC Driver](../../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes sqljdbc.jar, sqljdbc4.jar, sqljdbc41.jar ou sqljdbc42.jar a serem usados de acordo com suas configurações preferenciais do JRE (Java Runtime Environment). Esta amostra usa os métodos [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) e [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md), que são introduzidos na API do JDBC 4.0, para acessar os métodos de buffer de resposta específicos do driver. A fim de compilar e executar este exemplo, você precisará da biblioteca de classes sqljdbc4.jar que oferece suporte para JDBC 4.0. Para saber mais sobre qual arquivo JAR escolher, confira os [Requisitos do sistema para o JDBC Driver](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

## <a name="example"></a>Exemplo

No exemplo a seguir, o código de exemplo faz uma conexão com o banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Em seguida, o código de exemplo cria um objeto Statement e usa o método [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) para verificar se o objeto Statement é um wrapper para a classe [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) especificada. O método [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) é usado para acessar os métodos de buffer de resposta específicos do driver.

Em seguida, o código de exemplo define o modo de buffer de resposta como "**adaptável**" usando o método [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) da classe [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) e também demonstra como obter o modo de buffer adaptável.

Em seguida, ele executa a instrução SQL e coloca os dados retornados em um objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) atualizável.

Por fim, o código de exemplo itera pelas linhas de dados do conjunto de resultados. Se ele localizar um resumo vazio do documento, usará a combinação dos métodos [updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) e [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) para atualizar a linha de dados e novamente persisti-la no banco de dados. Se já houver dados, usará o método [getString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) para exibir alguns dos dados.

O comportamento padrão do driver é"**adaptável**". Porém, para os conjuntos de resultados atualizáveis somente de avanço e quando os dados no conjunto de resultados são maiores que a memória do aplicativo, o aplicativo precisa definir o modo de buffer adaptável explicitamente usando o método [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) da classe [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).

[!code[JDBC#UsingAdaptiveBuffering3](../../../connect/jdbc/codesnippet/Java/updating-large-data-sample_1.java)]

## <a name="see-also"></a>Confira também

[Trabalhando com dados grandes](../../../connect/jdbc/code-samples/working-with-large-data.md)
