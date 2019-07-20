---
title: Bibliotecas padrão do pacote R e Python
description: Pacotes r e Python instalados pelo SQL Server para R Services, R Server, Serviços de Machine Learning (no banco de dados) e Machine Learning Server (autônomo)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: f6cf66725ae15b2b738c020258142576ede734ec
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345083"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>Pacotes R e Python padrão no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo lista os pacotes R e Python instalados com SQL Server e onde encontrar a biblioteca de pacotes.  

## <a name="r-package-list-for-sql-server"></a>Lista de pacotes R para SQL Server

Os pacotes do r são instalados com [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) e [SQL Server 2017 serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) quando você seleciona o recurso do R durante a instalação. 

|Packages         | 2016 | 2017 | Descrição |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9,2 | Usado para contextos de computação remota, streaming, execução paralela de funções RX para importação e transformação de dados, modelagem, visualização e análise. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9,2 |Usado para incluir o script R em procedimentos armazenados. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| NA | 9,2 | Adiciona algoritmos de aprendizado de máquina em R. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | NA  | 9,2 | Usado para escrever instruções MDX em R. |

MicrosoftML e olapr estão disponíveis por padrão no Serviços de Machine Learning SQL Server 2017. Em uma instância SQL Server R Services 2016, você pode adicionar esses pacotes por meio de uma [atualização de componente](../install/upgrade-r-and-python.md). Uma atualização de componente também obtém versões mais recentes de pacotes (por exemplo, versões mais recentes do RevoScaleR incluem funções de gerenciamento de pacotes em SQL Server).

## <a name="python-package-list-for-sql-server"></a>Lista de pacotes do Python para SQL Server

Os pacotes do Python estão disponíveis somente no SQL Server 2017 quando você instala [SQL Server 2017 serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) e seleciona o recurso Python.

| Packages         | 2017    |  Descrição |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9,2 | Usado para contextos de computação remota, streaming, execução paralela de funções RX para importação e transformação de dados, modelagem, visualização e análise. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9,2 | Adiciona algoritmos de aprendizado de máquina em Python. |

## <a name="open-source-r-in-your-installation"></a>R de código-fonte aberto em sua instalação

O suporte a r inclui código-fonte aberto para que você possa chamar as funções base do R e instalar pacotes adicionais de software livre e de terceiros. O suporte à linguagem R inclui a funcionalidade básica, como **base**, **estatísticas**, **utils**e outros. Uma instalação básica do R também inclui vários conjuntos de dados de exemplo e ferramentas padrão do R, como **RGui** (um editor interativo leve) e **RTerm** (um prompt de comando do r). 

A distribuição do R de software livre incluído na sua instalação é o [Microsoft R Open (MRO)](https://mran.microsoft.com/open). O MRO agrega valor ao R base, incluindo pacotes de software livre adicionais, como a [biblioteca de kernel de matemática da Intel](https://en.wikipedia.org/wiki/Math_Kernel_Library).

A tabela a seguir resume as versões do R fornecidas pelo MRO usando a instalação do SQL Server.

|Versão             | Versão do R       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [SQL Server 2017 Serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

Você nunca deve substituir manualmente a versão do R instalada pela instalação do SQL Server com versões mais recentes na Web. Os pacotes do Microsoft R são baseados em versões específicas do R. modificar sua instalação pode desestabilizar.

## <a name="open-source-python-in-your-installation"></a>Python de código aberto em sua instalação

SQL Server 2017 adiciona componentes do Python. Quando você seleciona a opção de linguagem Python, a distribuição do Anaconda 4,2 é instalada. Além das bibliotecas de código do Python, a instalação padrão inclui dados de exemplo, testes de unidade e scripts de exemplo. 

SQL Server 2017 Machine Learning é a primeira versão para ter suporte a R e Python.

|Versão             | Versão do Anaconda| Pacotes da Microsoft    |
|--------------------|-----------------|-----------------------|
| Serviços de Machine Learning do SQL Server 2017  | 4,2 sobre Python 3,5 | revoscalepy, microsoftml |

Você nunca deve substituir manualmente a versão do Python instalada pelo SQL Server instalação com versões mais recentes na Web. Os pacotes python da Microsoft são baseados em versões específicas do Anaconda. Modificar sua instalação pode desestabilizar.

## <a name="component-upgrades"></a>Atualizações de componentes

Após a instalação inicial, os pacotes R e Python são atualizados por meio de Service Packs e atualizações cumulativas, mas atualizações de versão completas só são possíveis pela *Associação* à política de suporte do ciclo de vida moderno. A associação altera o modelo de serviço. Por padrão, após uma instalação inicial, os pacotes do R são atualizados por meio de Service Packs e atualizações cumulativas. Pacotes adicionais e atualizações de versão completa dos principais componentes do R só são possíveis por meio de atualizações de produto (de SQL Server 2016 para SQL Server 2017) ou pela vinculação do suporte a R para Microsoft Machine Learning Server. Para obter mais informações, consulte [upgrade R and Python Components in SQL Server](../install/upgrade-r-and-python.md).

## <a name="package-library-location"></a>Local da biblioteca de pacotes

Quando você instala o Machine Learning com o SQL Server, uma única biblioteca de pacote é criada no nível da instância para cada idioma que você instalar. No Windows, a biblioteca de instâncias é uma pasta segura registrada com SQL Server.

Todo script ou código executado no banco de dados no SQL Server deve carregar funções da biblioteca de instâncias. SQL Server não pode acessar pacotes instalados em outras bibliotecas. Isso também se aplica a clientes remotos. Ao se conectar ao servidor de um cliente remoto, qualquer código de R ou Python que você deseja executar no contexto de computação do servidor só pode usar pacotes instalados na biblioteca de instâncias.

Para proteger ativos de servidor, a biblioteca de instância padrão pode ser modificada somente por um administrador de computador. Se você não for o proprietário do computador, talvez seja necessário obter permissão de um administrador para instalar pacotes nessa biblioteca. 

#### <a name="file-path-for-in-database-engine-instances"></a>Caminho do arquivo para instâncias do mecanismo no banco de dados

A tabela a seguir mostra o local do arquivo de R e Python para combinações de instância de mecanismo de banco de dados e versão. MSSQL13 indica SQL Server 2016 e é somente R. MSSQL14 indica SQL Server 2017 e tem as pastas R e Python. 

Os caminhos de arquivo também incluem nomes de instância. SQL Server instala [instâncias do mecanismo de banco de dados](../../database-engine/configure-windows/database-engine-instances-sql-server.md) como a instância padrão (MSSQLSERVER) ou como uma instância nomeada definida pelo usuário. Se SQL Server for instalado como uma instância nomeada, você verá esse nome anexado da seguinte maneira: `MSSQL13.<instance_name>`.

|Versão e idioma  | Caminho padrão|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library|
| SQL Server 2017 com R|C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |
| SQL Server 2017 com Python |C:\Arquivos de Programas\microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages |


#### <a name="file-path-for-standalone-server-installations"></a>Caminho do arquivo para instalações de servidor autônomo

A tabela a seguir lista os caminhos padrão dos binários quando SQL Server servidor R 2016 (autônomo) ou SQL Server 2017 Machine Learning Server (autônomo) é instalado. 

|Version| Instalação|Caminho padrão|
|-------|-------------|------------|
| SQL Server 2016|R Server (Autônomo)| C:\Arquivos de Programas\microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Machine Learning Server, com R |C:\Arquivos de Programas\microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Machine Learning Server, com Python |C:\Arquivos de Programas\microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> Se você encontrar outras pastas com nomes de subpasta e arquivos semelhantes, provavelmente terá uma instalação autônoma de Microsoft R Server ou [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/). Esses produtos de servidor têm diferentes instaladores e caminhos (ou seja, C:\Program Files\Microsoft\R Server\R_SERVER ou C:\Program Programas\microsoft\ml SERVER\R_SERVER). Para obter mais informações, consulte [instalar o Machine Learning Server para Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) ou [instalar o R Server 9,1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

## <a name="next-steps"></a>Próximas etapas

+ [Obter informações sobre o pacote](installed-package-information.md)
+ [Instalar os novos pacotes R](../r/install-additional-r-packages-on-sql-server.md)
+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Habilitar o gerenciamento remoto de pacotes R](../r/r-package-how-to-enable-or-disable.md)
+ [Funções de RevoScaleR para o gerenciamento de pacotes R](../r/use-revoscaler-to-manage-r-packages.md)
+ [Sincronização de pacotes R](../r/package-install-uninstall-and-sync.md)
+ [miniCRAN para o repositório local de pacotes R](../r/create-a-local-package-repository-using-minicran.md)
