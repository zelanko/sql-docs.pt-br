---
title: Obter informações sobre o pacote do R
description: Saiba como obter informações sobre os pacotes do R instalados nos Serviços de Machine Learning do SQL Server e os SQL Server R Services.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 41e5f384878dfb284c31d6ba2886c9e223d03ca3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74479420"
---
# <a name="get-r-package-information"></a>Obter informações sobre o pacote do R

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como obter informações sobre os pacotes do R instalados nos Serviços de Machine Learning do SQL Server e os SQL Server R Services. Os exemplos de scripts R mostram como listar informações de pacote, como o caminho e a versão de instalação.

## <a name="default-r-library-location"></a>Localização da biblioteca padrão do R

Quando você instala o aprendizado de máquina com o SQL Server, uma única biblioteca de pacotes é criada no nível de instância para cada linguagem instalada. No Windows, a biblioteca de instâncias é uma pasta protegida registrada no SQL Server.

Todo script executado no banco de dados no SQL Server deve carregar funções da biblioteca de instâncias. O SQL Server não pode acessar pacotes instalados em outras bibliotecas. Isso se aplica a clientes remotos também: qualquer script R em execução no contexto de computação do servidor só pode usar pacotes instalados na biblioteca de instâncias.
Para proteger os ativos do servidor, a biblioteca de instâncias padrão pode ser modificada apenas por um administrador do computador.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
O caminho padrão dos binários para R é:

`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
O caminho padrão dos binários para R é:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
O caminho padrão dos binários para R é:

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

Isso pressupõe a instância SQL padrão, MSSQLSERVER. Se o SQL Server estiver instalado como uma instância nomeada definida pelo usuário, o nome fornecido será usado.

<!-- I don't think this note is necessary. If you have these other products installed, you'd already know about them.
> [!NOTE]
> If you find other folders having similar subfolder names and files, you probably have a standalone installation of  Microsoft R Server or Machine Learning Server. These server products have different installers and paths: C:\Program Files\Microsoft\R Server\R_SERVER or C:\Program Files\Microsoft\ML SERVER\R_SERVER. For more information, see [Install R Server 9.1 for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) or [Install Machine Learning Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).
-->

Execute a instrução a seguir para verificar a biblioteca de pacotes do R padrão para a instância atual:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

A instrução a seguir usa [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) para retornar o caminho da biblioteca de instâncias e a versão do RevoScaleR usado pelo SQL Server:

```sql
EXECUTE sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> A função [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) pode ser executada apenas no computador local. A função não pode retornar caminhos de biblioteca para conexões remotas.

## <a name="default-r-packages"></a>Pacotes do R padrão

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

Os seguintes pacotes do R são instalados com o SQL Server R Services.

|Pacotes | Versão | Descrição |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | Usada para contextos de computação remota, streaming, execução paralela de funções rx para importação e transformação de dados, modelagem, visualização e análise. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 1.0.0 | Usada para incluir o script R em procedimentos armazenados. |

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

Os pacotes do R a seguir são instalados com os Serviços de Machine Learning do SQL Server quando você seleciona o recurso do R durante a instalação.

|Pacotes | Versão | Descrição |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 9.2 | Usada para contextos de computação remota, streaming, execução paralela de funções rx para importação e transformação de dados, modelagem, visualização e análise. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 1.0.0 | Usada para incluir o script R em procedimentos armazenados. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| 1.4.0 | Adiciona algoritmos de aprendizado de máquina em R. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0.0 | Usada para escrever instruções MDX em R. |

::: moniker-end

### <a name="component-upgrades"></a>Atualizações de componentes

Por padrão, os pacotes do R são atualizados por meio de service packs e atualizações cumulativas. Pacotes adicionais e atualizações de versão completa dos principais componentes do R são possíveis apenas por meio de atualizações de produto ou pela associação do suporte a R para Microsoft Machine Learning Server.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Além disso, você pode adicionar pacotes MicrosoftML e olapR a uma instância do SQL Server por meio de uma atualização de componente.
::: moniker-end

Para obter mais informações, confira [Atualizar componentes do R e do Python no SQL Server](../install/upgrade-r-and-python.md).

## <a name="default-open-source-r-packages"></a>Pacotes do R de software livre padrão

O suporte ao R inclui o R de software livre para que você possa chamar funções básicas do R e instalar pacotes de terceiros e de software livre adicionais. O suporte à linguagem R inclui a principal funcionalidade, como **base**, **stats**, **utils** e outros. Uma instalação básica do R também inclui vários conjuntos de dados de exemplo e ferramentas padrão do R, como **RGui** (um editor interativo leve) e **RTerm** (um prompt de comando do R).

A distribuição do R de software livre incluída em sua instalação é [MRO (Microsoft R Open)](https://mran.microsoft.com/open). O MRO agrega valor ao R básico, incluindo pacotes de software livre adicionais, como a [Biblioteca Intel Math Kernel](https://en.wikipedia.org/wiki/Math_Kernel_Library).

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
A versão do R fornecida pelo MRO usando a Instalação dos SQL Server R Services é a 3.2.2.
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
A versão do R fornecida pelo MRO usando a Instalação dos Serviços de Machine Learning do SQL Server é a 3.3.3.
::: moniker-end

> [!IMPORTANT]
> Você nunca deve substituir manualmente a versão do R instalada pela Instalação do SQL Server por versões mais recentes na Web. Os pacotes do Microsoft R são baseados em versões específicas do R. Modificar sua instalação poderia desestabilizá-lo.

## <a name="list-all-installed-r-packages"></a>Listar todos os pacotes do R instalados

O exemplo a seguir usa a função do R `installed.packages()` em um procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] para exibir uma lista de pacotes do R que foram instalados na biblioteca R_SERVICES da instância do SQL atual. Esse script retorna os campos de nome e versão do pacote no arquivo DESCRIPTION.

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
Name <- packagematrix[,1];
Version <- packagematrix[,3];
OutputDataSet <- data.frame(Name, Version);',
@input_data_1 = N'
  '
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

Para obter mais informações sobre os campos opcionais e padrão do campo DESCRIÇÃO do pacote do R, confira [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

## <a name="find-a-single-r-package"></a>Localizar um único pacote do R

Se você tiver instalado um pacote do R e desejar verificar se ele está disponível para uma instância específica do SQL Server, poderá executar um procedimento armazenado para carregar o pacote e retornar as mensagens.

Por exemplo, a instrução a seguir procura e carrega o pacote [glue](https://cran.r-project.org/web/packages/glue/), se disponível.
Se o pacote não puder ser localizado ou carregado, você receberá um erro contendo o texto, "não há nenhum pacote chamado 'glue'."

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("glue")'
GO
```

Para ver mais informações sobre o pacote, exiba o `packageDescription`.
A instrução a seguir retorna informações para o pacote **glue**.

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("glue"))
  '
```

## <a name="next-steps"></a>Próximas etapas

::: moniker range="<=sql-server-2017||=sqlallproducts-allversions"
+ [Instalar pacotes com ferramentas de R](install-r-packages-standard-tools.md)
::: moniker-end
::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
+ [Instalar novos pacotes de R com sqlmlutils](install-additional-r-packages-on-sql-server.md)
::: moniker-end
+ [Obter informações sobre o pacote do Python](python-package-information.md)
+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais do R e do Python](../tutorials/machine-learning-services-tutorials.md)
