---
title: Bibliotecas de pacote de R e Python - serviços de Machine Learning do SQL Server padrão
description: Pacotes de R e Python instalados pelo SQL Server R Services, Microsoft R Server, serviços do Machine Learning (no banco de dados) e Machine Learning Server (autônomo)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0a8c4c0f14a099dd4b6d8e6c48b8d84e209f6024
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432324"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>Pacotes de R padrão e Python no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo lista os pacotes de R e Python instalados com o SQL Server e onde encontrar a biblioteca de pacote.  

## <a name="r-package-list-for-sql-server"></a>Lista de pacotes de R para SQL Server

Pacotes R são instalados com [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) e [serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) quando você seleciona o recurso do R durante a instalação. 

Packages         | 2016 | 2017 | Descrição |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9.2 | Usado para contextos de computação remota, streaming, a execução paralela de funções de rx para importação de dados e transformação, modelagem, visualização e análise. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9.2 |Usado para a inclusão de script R em procedimentos armazenados. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| NA | 9.2 | Adiciona os algoritmos de aprendizado de máquina em R. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | NA  | 9.2 | Usado para escrever instruções MDX no R. |

MicrosoftML e olapR estão disponíveis por padrão nos serviços de aprendizado de máquina do SQL Server 2017. Em uma instância do SQL Server 2016 R Services, você pode adicionar esses pacotes por meio de um [atualização do componente](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md). Uma atualização de componente também obtém as versões mais recentes dos pacotes (por exemplo, as versões mais recentes do RevoScaleR incluem funções para gerenciamento de pacotes no SQL Server).

## <a name="python-package-list-for-sql-server"></a>Lista de pacotes do Python para o SQL Server

Pacotes de Python estão disponíveis apenas no SQL Server 2017 quando você instala [serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) e selecione o recurso de Python.

| Packages         | 2017    |  Descrição |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | Usado para contextos de computação remota, streaming, a execução paralela de funções de rx para importação de dados e transformação, modelagem, visualização e análise. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | Adiciona os algoritmos de aprendizado de máquina em Python. |

## <a name="open-source-r-in-your-installation"></a>R de código-fonte aberto em sua instalação

Suporte ao R inclui código-fonte aberto para que você pode chamar funções de R base e instalar pacotes adicionais do código-fonte aberto e de terceiros. Suporte à linguagem R inclui a funcionalidade principal, como **base**, **estatísticas**, **utils**e outros. Uma instalação básica do R também inclui vários conjuntos de dados de exemplo e ferramentas padrão do R, como **RGui** (um editor interativo simples) e **RTerm** (um prompt de comando do R). 

A distribuição de software livre R incluída em sua instalação é [abrir o MRO (Microsoft R)](https://mran.microsoft.com/open). MRO agrega valor à base R, incluindo pacotes de código-fonte aberto adicionais, como o [Intel Math Kernel Library](https://en.wikipedia.org/wiki/Math_Kernel_Library).

A tabela a seguir resume as versões do R fornecidas pelo MRO usando a instalação do SQL Server.

|Versão             | Versão do R       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [Serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

Nunca manualmente, você deve substituir a versão do R instalado pela instalação do SQL Server com as versões mais recentes na web. Pacotes de R da Microsoft se baseiam em versões específicas de R. modificar sua instalação pode desestabilizar.

## <a name="open-source-python-in-your-installation"></a>Python de código-fonte aberto em sua instalação

SQL Server 2017 adiciona componentes do Python. Quando você seleciona a opção de linguagem Python, distribuição do Anaconda 4.2 está instalada. Além das bibliotecas de código do Python, a instalação padrão inclui dados de exemplo, testes de unidade e scripts de exemplo. 

Aprendizado de máquina do SQL Server 2017 é a primeira versão ter R e Python dão suporte.

|Versão             | O anaconda versão| Pacotes da Microsoft    |
|--------------------|-----------------|-----------------------|
| Serviços de Machine Learning do SQL Server 2017  | 4.2 em Python 3.5 | revoscalepy, microsoftml |

Nunca manualmente, você deve substituir a versão do Python instalado pelo programa de instalação do SQL Server com as versões mais recentes na web. Pacotes do Python de Microsoft se baseiam em versões específicas do Anaconda. Modificar a instalação pode desestabilizá-lo.

## <a name="component-upgrades"></a>Atualizações de componentes

Após uma instalação inicial, os pacotes R e Python são atualizados por meio de service packs e atualizações cumulativas, mas as atualizações de versão completo somente são possíveis por *associação* à política de suporte do ciclo de vida moderno. Associação altera o modelo de manutenção. Por padrão, após uma instalação inicial, pacotes R são atualizados por meio de service packs e atualizações cumulativas. Atualizações de versão completa dos componentes principal do R e pacotes adicionais são possíveis somente por meio de atualizações de produto (do SQL Server 2016 ao SQL Server 2017) ou pela vinculação de R dão suporte ao Microsoft Machine Learning Server. Para obter mais informações, consulte [componentes atualizar R e Python no SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="package-library-location"></a>Local da biblioteca de pacote

Quando você instala o aprendizado de máquina com o SQL Server, uma biblioteca de pacote único é criada no nível de instância para cada idioma que deseja instalar. No Windows, a biblioteca de instância é uma pasta protegida registrada com o SQL Server.

Todos os script ou código que é executado no banco de dados no SQL Server deve carregar as funções da biblioteca de instância. SQL Server não pode acessar os pacotes instalados em outras bibliotecas. Aplica-se para os clientes remotos. Ao se conectar ao servidor de um cliente remoto, qualquer código R ou Python que você deseja executar no contexto de computação do servidor só pode usar pacotes instalados na biblioteca de instância.

Para proteger os ativos do servidor, a biblioteca de instância padrão pode ser modificada somente por um administrador do computador. Se você não for o proprietário do computador, você precisa obter permissão do administrador para instalar os pacotes para essa biblioteca. 

#### <a name="file-path-for-in-database-engine-instances"></a>Caminho de arquivo para instâncias do mecanismo de no banco de dados

A tabela a seguir mostra o local do arquivo de R e Python para o banco de dados e a versão combinações de instância do mecanismo. MSSQL13 indica o SQL Server 2016 e é somente para R. MSSQL14 indica que o SQL Server 2017 e tem pastas de R e Python. 

Caminhos de arquivo também incluem os nomes de instância. O SQL Server instala [instâncias do mecanismo de banco de dados](../../database-engine/configure-windows/database-engine-instances-sql-server.md) como a instância padrão (MSSQLSERVER) ou como uma instância nomeada definida pelo usuário. Se o SQL Server é instalado como uma instância nomeada, você verá esse nome anexado da seguinte maneira: `MSSQL13.<instance_name>`.

|Versão e idioma  | Caminho padrão|
|----------------------|------------|
| SQL Server 2016 |Mssql13 SQL do C:\Program Files\Microsoft. MSSQLSERVER\R_SERVICES\library|
| SQL Server 2017 com R|Server\MSSQL14 SQL do C:\Program Files\Microsoft. MSSQLSERVER\R_SERVICES\library |
| SQL Server 2017 com o Python |Server\MSSQL14 SQL do C:\Program Files\Microsoft. Pacotes de MSSQLSERVER\PYTHON_SERVICES\Lib\site |


#### <a name="file-path-for-standalone-server-installations"></a>Caminho de arquivo para instalações autônomas de servidores

A tabela a seguir lista os caminhos padrão de binários quando o SQL Server 2016 R Server (autônomo) ou o servidor do Machine Learning Server (autônomo) do SQL Server 2017 está instalado. 

|Versão| Instalação|Caminho padrão|
|-------|-------------|------------|
| SQL Server 2016|R Server (Autônomo)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Machine Learning Server com R |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Machine Learning Server, com o Python |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> Se você encontrar outras pastas com nomes semelhantes de subpasta e arquivos, você provavelmente tem uma instalação autônoma do Microsoft R Server ou [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/). Esses produtos de servidor têm diferentes instaladores e caminhos (ou seja, C:\Program Files\Microsoft\R Server\R_SERVER ou C:\Program programas\microsoft\ml SERVER\R_SERVER). Para obter mais informações, consulte [instalar o Machine Learning Server para Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) ou [instalar o R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

## <a name="next-steps"></a>Próximas etapas

+ [Obter informações sobre o pacote](determine-which-packages-are-installed-on-sql-server.md)
+ [Instalar os novos pacotes R](install-additional-r-packages-on-sql-server.md)
+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Habilitar o gerenciamento remoto de pacotes R](r-package-how-to-enable-or-disable.md)
+ [Funções de RevoScaleR para o gerenciamento de pacotes R](use-revoscaler-to-manage-r-packages.md)
+ [Sincronização de pacotes R](package-install-uninstall-and-sync.md)
+ [miniCRAN para o repositório local de pacotes R](create-a-local-package-repository-using-minicran.md)
