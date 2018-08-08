---
title: Amostra de leitura de dados grandes com procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 58c76635-a117-4661-8781-d6cb231c5809
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f02c6f338ed7901813abd13b68bec97cf0e31645
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39453040"
---
# <a name="reading-large-data-with-stored-procedures-sample"></a>Exemplo de leitura de dados grandes com procedimentos armazenados

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Este aplicativo de exemplo do [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] demonstra como recuperar um parâmetro OUT grande de um procedimento armazenado.

O arquivo de código desta amostra chama-se ExecuteStoredProcedure.java e pode ser encontrado neste local:

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>Requisitos

Para executar este aplicativo de exemplo, você precisará ter acesso ao banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Defina também o classpath para incluir o arquivo mssql-jdbc.jar. Para obter mais informações sobre como definir o classpath, consulte [usando o Driver JDBC](../../../connect/jdbc/using-the-jdbc-driver.md).

> [!NOTE]  
> O [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] fornece os arquivos de biblioteca de classes mssql-jdbc a serem usados de acordo com suas configurações preferenciais do JRE (Java Runtime Environment). Para obter mais informações sobre qual arquivo JAR escolher, consulte [requisitos do sistema para o Driver JDBC](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md).

Crie o seguinte procedimento armazenado no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]:

```sql
CREATE PROCEDURE GetLargeDataValue
  (@Document_ID int,
   @Document_ID_out int OUTPUT,
   @Document_Title varchar(50) OUTPUT,  
   @Document_Summary nvarchar(max) OUTPUT)  

AS
BEGIN
   SELECT @Document_ID_out = DocumentID,
          @Document_Title = Title,  
          @Document_Summary = DocumentSummary
    FROM  Production.Document  
    WHERE DocumentID = @Document_ID  
END  
```

## <a name="example"></a>Exemplo

No exemplo a seguir, o código de exemplo faz uma conexão com o banco de dados [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]. Em seguida, o código de exemplo cria dados de exemplo e atualiza a tabela Production.Document usando uma consulta parametrizada. Em seguida, o código de exemplo obtém o modo de buffer adaptável usando o método [getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) da classe [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) e executa o procedimento armazenado GetLargeDataValue. Observe que, a partir da versão 2.0 do driver JDBC, a propriedade de conexão responseBuffering é definida por padrão como "adaptável".

Por fim, o código de exemplo exibe os dados retornados com os parâmetros OUT e também demonstra como usar os métodos `mark` e `reset` no fluxo para reler qualquer parte dos dados.

[!code[JDBC#UsingAdaptiveBuffering2](../../../connect/jdbc/codesnippet/Java/reading-large-data-with-_1_1.java)]

## <a name="see-also"></a>Consulte Também

[Manipular dados grandes](../../../connect/jdbc/code-samples/working-with-large-data.md)
