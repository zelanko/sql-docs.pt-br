---
title: "Determinar quais pacotes de R são instalados no SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e3f906e0c5290b6aa2cab375e4761390f84e718d
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="determine-which-r-packages-are-installed-on-sql-server"></a>Determinar quais pacotes de R são instalados no SQL Server

Quando você instala o aprendizado de máquina no SQL Server com a opção de linguagem R, uma biblioteca de pacote de R é criada especificamente para ser usada pela instância. Cada instância do servidor tem sua própria biblioteca de pacote. Bibliotecas de pacote não podem ser compartilhadas entre instâncias.

Este artigo descreve como você pode determinar quais pacotes de R são instalados para uma instância específica do SQL Server.

## <a name="generate-r-package-list-using-a-stored-procedure"></a>Gerar a lista de pacotes de R usando um procedimento armazenado

O exemplo a seguir usa a função R `installed.packages()` em uma [!INCLUDE [tsql](..\..\includes\tsql-md.md)] procedimento armazenado para obter uma matriz de pacotes que foram instalados na biblioteca do R_SERVICES para a instância atual. Para evitar a análise dos campos no arquivo DESCRIPTION, somente o nome será retornado.

```SQL
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
NameOnly <- packagematrix[,1];
OutputDataSet <- as.data.frame(NameOnly);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250) ))
```

Para obter mais informações sobre opcional e campos padrão para o campo de descrição do pacote de R, consulte [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>Verificar se um pacote está instalado com uma instância

Se você tiver instalado um pacote e deseja ter certeza de que ele esteja disponível para uma determinada instância do SQL Server, você pode executar a seguinte chamada de procedimento armazenado para carregar o pacote e retornar apenas as mensagens. Este exemplo procura e carrega a biblioteca RevoScaleR, se disponível.

```sql
EXEC sp_execute_external_script  @language =N'R',
@script=N'library("RevoScaleR")'
GO
```

+ Se o pacote for encontrado, uma mensagem será retornada: "Comandos concluída com êxito."

+ Se o pacote não pode ser localizado ou carregado, você receberá um erro que contém o texto: "não há nenhum pacote chamado 'MissingPackageName'"

## <a name="get-a-list-of-installed-packages-using-r"></a>Obter uma lista de pacotes instalados usando o R

Há várias maneiras de se obter uma lista de pacotes instalados ou carregados, usando ferramentas de R e funções de R. Muitas ferramentas de desenvolvimento do R fornecem um pesquisador de objetos ou uma lista de pacotes instalados ou carregados no espaço de trabalho atual do R. Esta seção fornece alguns comandos curtos que podem ser usadas em qualquer linha de comando de R ou SP\_executar\_externo\_script.

+ Do utilitário local do R, use uma função de base R, como `installed.packages()`, que está incluído o `utils` pacote. Para obter uma lista que é precisa para uma instância, você deve especificar explicitamente o caminho da biblioteca ou usar as ferramentas de R associadas com a biblioteca de instância.

+ Para verificar um pacote em um contexto de computação específico, você pode usar as seguintes funções do pacote RevoScaleR. Essas funções ajudam a identificar os pacotes em contextos de computação especificado:

+ [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)

+ [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)

Por exemplo, execute o seguinte código de R para obter uma lista de pacotes disponíveis no contexto de computação do SQL Server especificado.

```r
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```

## <a name="get-library-location-and-version"></a>Obter a versão e o local da biblioteca

O exemplo a seguir obtém a localização da biblioteca de RevoScaleR no contexto de computação local e a versão do pacote.

```r
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

## <a name="determine-path-of-library-used-by-sql-server"></a>Determinar o caminho de biblioteca usada pelo SQL Server

Se você atualizou a componentes usando associação de aprendizado de máquina, pode alterar o caminho para a biblioteca de R. Quando isso acontece, atalhos anteriores das ferramentas podem fazer referência a uma versão anterior. Para ter certeza da versão pacote e o caminho usado pelo SQL Server, você pode executar um comando como o seguinte:

```sql
EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    sql_r_path <- rxSqlLibPaths("local")
      print(sql_r_path)
    version_info <-packageVersion("RevoScaleR")
      print(version_info)'
```

**Resultados**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```
## <a name="see-also"></a>Consulte também

[Instalar pacotes R adicionais no SQL Server](install-additional-r-packages-on-sql-server.md)
