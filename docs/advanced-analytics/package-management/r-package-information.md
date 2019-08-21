---
title: Obter informações do pacote do R
description: Saiba como obter informações sobre pacotes R instalados em SQL Server Serviços de Machine Learning e SQL Server R Services.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 8c3cf3c1debc03c169c585521b8b46dd8b1365c5
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69641153"
---
# <a name="get-r-package-information"></a>Obter informações do pacote do R

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como obter informações sobre pacotes R instalados em SQL Server Serviços de Machine Learning e SQL Server R Services. Scripts R de exemplo mostram como listar informações do pacote, como o caminho de instalação e a versão.

## <a name="default-r-library-location"></a>Local da biblioteca do R padrão

Quando você instala o Machine Learning com o SQL Server, uma única biblioteca de pacote é criada no nível da instância para cada idioma que você instalar. No Windows, a biblioteca de instâncias é uma pasta segura registrada com SQL Server.

Todo script que é executado no banco de dados no SQL Server deve carregar funções da biblioteca de instâncias. SQL Server não pode acessar pacotes instalados em outras bibliotecas. Isso também se aplica a clientes remotos: qualquer script R em execução no contexto de computação do servidor só pode usar pacotes instalados na biblioteca de instâncias.
Para proteger ativos de servidor, a biblioteca de instância padrão pode ser modificada somente por um administrador de computador.

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

Isso pressupõe a instância SQL padrão, MSSQLSERVER. Se SQL Server for instalado como uma instância nomeada definida pelo usuário, o nome fornecido será usado em seu lugar.

<!-- I don't think this note is necessary. If you have these other products installed, you'd already know about them.
> [!NOTE]
> If you find other folders having similar subfolder names and files, you probably have a standalone installation of  Microsoft R Server or Machine Learning Server. These server products have different installers and paths: C:\Program Files\Microsoft\R Server\R_SERVER or C:\Program Files\Microsoft\ML SERVER\R_SERVER. For more information, see [Install R Server 9.1 for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) or [Install Machine Learning Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).
-->

Execute a seguinte instrução para verificar a biblioteca padrão do pacote R para a instância atual:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

A instrução a seguir usa [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) para retornar o caminho da biblioteca de instâncias e a versão do RevoScaleR usada pelo SQL Server:

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
> A função [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) pode ser executada somente no computador local. A função não pode retornar caminhos de biblioteca para conexões remotas.

## <a name="default-r-packages"></a>Pacotes R padrão

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

Os pacotes R a seguir são instalados com o SQL Server R Services.

|Packages | Versão | Descrição |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | Usado para contextos de computação remota, streaming, execução paralela de funções RX para importação e transformação de dados, modelagem, visualização e análise. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | Usado para incluir o script R em procedimentos armazenados. |

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

Os pacotes R a seguir são instalados com SQL Server Serviços de Machine Learning quando você seleciona o recurso do R durante a instalação.

|Packages | Versão | Descrição |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 9,2 | Usado para contextos de computação remota, streaming, execução paralela de funções RX para importação e transformação de dados, modelagem, visualização e análise. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 9,2 | Usado para incluir o script R em procedimentos armazenados. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| 9,2 | Adiciona algoritmos de aprendizado de máquina em R. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 9,2 | Usado para escrever instruções MDX em R. |

::: moniker-end

### <a name="component-upgrades"></a>Atualizações de componentes

Por padrão, os pacotes do R são atualizados por meio de Service Packs e atualizações cumulativas. Pacotes adicionais e atualizações de versão completa dos principais componentes do R são possíveis apenas por meio de atualizações de produto ou pela vinculação do suporte a R para Microsoft Machine Learning Server.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Além disso, você pode adicionar pacotes MicrosoftML e olapr a uma instância SQL Server por meio de uma atualização de componente.
::: moniker-end

Para obter mais informações, consulte [upgrade R and Python Components in SQL Server](../install/upgrade-r-and-python.md).

## <a name="default-open-source-r-packages"></a>Pacotes de R de código-fonte aberto padrão

O suporte a r inclui código-fonte aberto para que você possa chamar as funções base do R e instalar pacotes adicionais de software livre e de terceiros. O suporte à linguagem R inclui a funcionalidade básica, como **base**, **estatísticas**, **utils**e outros. Uma instalação básica do R também inclui vários conjuntos de dados de exemplo e ferramentas padrão do R, como **RGui** (um editor interativo leve) e **RTerm** (um prompt de comando do R).

A distribuição do R de software livre incluído na sua instalação é o [Microsoft R Open (MRO)](https://mran.microsoft.com/open). O MRO agrega valor ao R base, incluindo pacotes de software livre adicionais, como a [biblioteca de kernel de matemática da Intel](https://en.wikipedia.org/wiki/Math_Kernel_Library).

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
A versão do R fornecida pelo MRO usando a instalação do SQL Server R Services é 3.2.2.
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
A versão do R fornecida pelo MRO usando SQL Server Serviços de Machine Learning configuração é 3.3.3.
::: moniker-end

> [!IMPORTANT]
> Você nunca deve substituir manualmente a versão do R instalada pela instalação do SQL Server com versões mais recentes na Web. Os pacotes do Microsoft R são baseados em versões específicas do R. modificar sua instalação pode desestabilizar.

## <a name="list-all-installed-r-packages"></a>Listar todos os pacotes R instalados

O exemplo a seguir usa a função `installed.packages()` r em [!INCLUDE[tsql](../../includes/tsql-md.md)] um procedimento armazenado para exibir uma lista de pacotes do r que foram instalados na biblioteca R_SERVICES para a instância do SQL atual. Esse script retorna os campos de nome e versão do pacote no arquivo de descrição.

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

Para obter mais informações sobre os campos opcionais e padrão para o campo de descrição do [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)pacote R, consulte.

## <a name="find-a-single-r-package"></a>Localizar um único pacote R

Se você instalou um pacote do R e deseja certificar-se de que ele está disponível para uma instância específica do SQL Server, você pode executar um procedimento armazenado para carregar o pacote e retornar as mensagens.

Por exemplo, a instrução a seguir procura e carrega o pacote de [União](https://cran.r-project.org/web/packages/glue/) , se disponível.
Se o pacote não puder ser localizado ou carregado, você receberá um erro contendo o texto "não há um pacote chamado ' Glue '".

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("glue")'
GO
```

Para ver mais informações sobre o pacote, exiba o `packageDescription`.
A instrução a seguir retorna informações para o pacote de **cola** .

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("glue"))
  '
```

## <a name="next-steps"></a>Próximas etapas

+ [Instalar os novos pacotes R](../r/install-additional-r-packages-on-sql-server.md)
+ [Obter informações do pacote do Python](python-package-information.md)
+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais de R e Python](../tutorials/machine-learning-services-tutorials.md)
