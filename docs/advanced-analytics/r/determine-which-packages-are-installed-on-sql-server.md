---
title: "Determinar quais pacotes de R são instalados no SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 10/09/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d2404680ce5c3ddccc0ac65a3b49c905a1fc30a8
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="determine-which-r-packages-are-installed-on-sql-server"></a>Determinar quais pacotes de R são instalados no SQL Server

Quando você instala o aprendizado de máquina no SQL Server com a opção de linguagem R, a instalação cria uma biblioteca de pacote de R associada com a instância. Cada instância tem uma biblioteca de pacote separada. As bibliotecas de pacote são **não** compartilhadas entre instâncias, portanto, é possível para pacotes diferentes para ser instalado em instâncias diferentes.

Este artigo descreve como você pode determinar quais pacotes de R são instalados para uma instância específica.

## <a name="generate-r-package-list-using-a-stored-procedure"></a>Gerar a lista de pacotes de R usando um procedimento armazenado

O exemplo a seguir usa a função R `installed.packages()` em uma [!INCLUDE [tsql](..\..\includes\tsql-md.md)] procedimento armazenado para obter uma matriz de pacotes que foram instalados na biblioteca do R_SERVICES para a instância atual. Para evitar a análise dos campos no arquivo DESCRIPTION, somente o nome será retornado.

```SQL
EXECUTE sp_execute_external_script
@language=N'R'  
,@script = N'str(OutputDataSet);  
packagematrix <- installed.packages();  
NameOnly <- packagematrix[,1];  
OutputDataSet <- as.data.frame(NameOnly);'  
,@input_data_1 = N'SELECT 1 as col'  
WITH RESULT SETS ((PackageName nvarchar(250) ))  
```

Para obter mais informações sobre opcional e campos padrão para o arquivo de descrição do pacote de R, consulte [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>Verificar se um pacote está instalado com uma instância

Se você tiver instalado um pacote e deseja ter certeza de que ele esteja disponível para uma determinada instância do SQL Server, você pode executar a seguinte chamada de procedimento armazenado para carregar o pacote e retornar apenas as mensagens.

```SQL
EXEC sp_execute_external_script  @language =N'R',
@script=N'library("RevoScaleR")'
GO
```

Este exemplo procura e carrega a biblioteca RevoScaleR.

+ Se o pacote for encontrado, a mensagem retornada deve ser algo como "Comandos concluída com êxito."

+ Se o pacote não pode ser localizado ou carregado, você receberá um erro como esse: "Ocorreu um erro de script externo: erro em library("RevoScaleR"): não há nenhum pacote chamado RevoScaleR"

## <a name="get-a-list-of-installed-packages-using-r"></a>Obter uma lista de pacotes instalados usando o R

Há várias maneiras de se obter uma lista de pacotes instalados ou carregados, usando ferramentas de R e funções de R. Muitas ferramentas de desenvolvimento do R fornecem um pesquisador de objetos ou uma lista de pacotes instalados ou carregados no espaço de trabalho atual do R.

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
## <a name="see-also"></a>Consulte também

[Instalar pacotes R adicionais no SQL Server](install-additional-r-packages-on-sql-server.md)
