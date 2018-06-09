---
title: Padrão de R e Python bibliotecas de pacote no SQL Server R e aprendizado de máquina do SQL Server | Microsoft Docs
description: Pacotes de R e Python instalados pelo SQL Server para serviços de aprendizado de máquina do serviços de R, R Server (no banco de dados) e o servidor de aprendizado de máquina (autônomo)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9362d6e9dc98f80beabc301f43e755b205b40a10
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707284"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>Pacotes R padrão e Python no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo lista os pacotes de R e Python instalados com o SQL Server e onde encontrar a biblioteca de pacote.  

## <a name="r-package-list-for-sql-server"></a>Lista de pacotes de R para o SQL Server

Pacotes R instalados com [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) e [serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) quando você seleciona o recurso R durante a instalação. 

Packages         | 2016 | 2017 | Description |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9.2 | Usado para contextos de computação remota, streaming, execução paralela de funções de rx para importação de dados e transformação, modelagem, visualização e análise. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9.2 |Usado para a inclusão de script R em procedimentos armazenados. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| n.d. | 9.2 | Adiciona os algoritmos de aprendizado de máquina em R. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.d.  | 9.2 | Usado para escrever instruções MDX em R. |

MicrosoftML e olapR estão disponíveis por padrão nos serviços de aprendizado de máquina do SQL Server de 2017. Em uma instância do SQL Server 2016 R Services, você pode adicionar esses pacotes por meio de um [atualização de componente](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md). Uma atualização de componente também obtém as versões mais recentes de pacotes (por exemplo, versões mais recentes do RevoScaleR incluem funções para o gerenciamento de pacotes no SQL Server).

## <a name="python-package-list-for-sql-server"></a>Lista de pacotes do Python para o SQL Server

Pacotes do Python estão disponíveis apenas no SQL Server 2017, quando você instala [serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md) e selecione o recurso de Python.

| Packages         | 2017    |  Description |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | Usado para contextos de computação remota, streaming, execução paralela de funções de rx para importação de dados e transformação, modelagem, visualização e análise. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | Adiciona os algoritmos de aprendizado de máquina em Python. |

## <a name="open-source-r-in-your-installation"></a>R de código-fonte aberto em sua instalação

Suporte a R inclui o código-fonte aberto são para que você possa chamar funções de base R e instalar outros pacotes de código-fonte aberto e de terceiros. Suporte de linguagem R inclui a funcionalidade principal, como **base**, **estatísticas**, **utilitários**e outros. Uma instalação básica do R também inclui vários conjuntos de dados de exemplo e ferramentas padrão de R como **RGui** (um editor leve interativo) e **RTerm** (um prompt de comando de R). 

A distribuição de software livre R incluída em sua instalação é [abrir de R com a Microsoft (MRO)](https://mran.microsoft.com/open). MRO adiciona o valor de base R, incluindo pacotes de código-fonte aberto adicionais, como o [biblioteca de Kernel de matemática Intel](https://en.wikipedia.org/wiki/Math_Kernel_Library).

A tabela a seguir resume as versões de R fornecidas pelo MRO usando a instalação do SQL Server.

|Versão             | Versão de R       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [Serviços de aprendizado de máquina do SQL Server de 2017](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

Nunca manualmente, você deve substituir a versão do R instalado pela instalação do SQL Server com as versões mais recentes na web. Pacotes de R da Microsoft se baseiam em versões específicas do R. modificando a instalação pôde desestabilizar.

## <a name="open-source-python-in-your-installation"></a>Código-fonte aberto Python em sua instalação

SQL Server 2017 adiciona componentes de Python. Quando você seleciona a opção de linguagem Python, distribuição Anaconda 4.2 está instalada. Além das bibliotecas de código Python, a instalação padrão inclui dados de exemplo, testes de unidade e scripts de exemplo. 

Aprendizado de máquina do SQL Server de 2017 é a primeira versão R e suporte de Python.

|Versão             | Versão anaconda| Pacotes da Microsoft    |
|--------------------|-----------------|-----------------------|
| Serviços de Machine Learning do SQL Server 2017  | 4.2 em Python 3.5 | revoscalepy, microsoftml |

Nunca manualmente, você deve substituir a versão do Python instalados pela instalação do SQL Server com as versões mais recentes na web. Pacotes do Python Microsoft são baseados em versões específicas do Anaconda. Modificar a instalação pôde desestabilizá-lo.

## <a name="component-upgrades"></a>Atualizações de componentes

Após uma instalação inicial, os pacotes R e Python são atualizados por meio de service packs e atualizações cumulativas, mas as atualizações de versão completa somente são possíveis por *associação* para a política de suporte do ciclo de vida modernos. Associação altera o modelo de manutenção. Por padrão, após uma instalação inicial, pacotes R são atualizados por meio de service packs e atualizações cumulativas. Outros pacotes e atualizações de versão completa dos componentes principais R só são possíveis por meio de atualizações de produto (a partir do SQL Server 2016 para 2017 do SQL Server) ou por associação R oferecer suporte ao servidor de aprendizado de máquina do Microsoft. Para obter mais informações, consulte [atualização R e Python componentes do SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="package-library-location"></a>Local da biblioteca de pacote

Quando você instala o aprendizado de máquina com o SQL Server, uma biblioteca de pacote único é criada no nível de instância para cada idioma que deseja instalar. No Windows, a biblioteca de instância é uma pasta protegida registrada com o SQL Server.

Todos os script ou código que é executado no banco de dados no SQL Server deve carregar as funções da biblioteca de instância. SQL Server não pode acessar pacotes instalados em outras bibliotecas. Aplica-se os clientes remotos. Ao se conectar ao servidor de um cliente remoto, qualquer código de R ou Python que você deseja executar no contexto de computação do servidor só pode usar pacotes instalados na biblioteca de instância.

Para proteger os ativos do servidor, a biblioteca de instância padrão pode ser modificada somente por um administrador do computador. Se você não for o proprietário do computador, você precisará obter permissão do administrador para instalar os pacotes para essa biblioteca. 

#### <a name="file-path-for-in-database-engine-instances"></a>Caminho de arquivo para instâncias do mecanismo no banco de dados

A tabela a seguir mostra o local do arquivo de R e Python para o banco de dados e versão combinações de instância do mecanismo. MSSQL13 indica o SQL Server 2016 e é somente para R. MSSQL14 indica 2017 do SQL Server e tiver pastas de R e Python. 

Caminhos de arquivo também incluem os nomes de instância. O SQL Server instala [instâncias do mecanismo de banco de dados](../../database-engine/configure-windows/database-engine-instances-sql-server.md) como a instância padrão (MSSQLSERVER) ou como uma instância nomeada definida pelo usuário. Se o SQL Server estiver instalado como uma instância nomeada, você verá esse nome adicionada da seguinte maneira: `MSSQL13.<instance_name>`.

|Versão e idioma  | Caminho padrão|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL mssql13. MSSQLSERVER\R_SERVICES\library|
| SQL Server 2017 com R|C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library |
| SQL Server 2017 com Python |C:\Program Files\Microsoft SQL Server\MSSQL14. Pacotes de MSSQLSERVER\PYTHON_SERVICES\Lib\site |


#### <a name="file-path-for-standalone-server-installations"></a>Caminho de arquivo para instalações autônomas de servidores

A tabela a seguir lista os caminhos padrão de binários quando o servidor do SQL Server 2016 R (autônomo) ou o servidor do servidor do aprendizado de máquina 2017 SQL Server (autônomo) é instalado. 

|Versão| Instalação|Caminho padrão|
|-------|-------------|------------|
| SQL Server 2016|R Server (Autônomo)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Servidor com R de aprendizado de máquina |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Servidor, com Python de aprendizado de máquina |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> Se você encontrar outras pastas com nomes semelhantes de subpastas e arquivos, você provavelmente tem uma instalação autônoma do Microsoft R Server ou [server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/). Esses produtos de servidor têm instaladores diferentes e caminhos (ou seja, C:\Program Files\Microsoft\R Server\R_SERVER ou C:\Program Files\Microsoft\ML SERVER\R_SERVER). Para obter mais informações, consulte [instalar Machine Learning Server para Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) ou [instalar o R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

## <a name="next-steps"></a>Próximas etapas

+ [Obter informações sobre o pacote](determine-which-packages-are-installed-on-sql-server.md)
+ [Instalar os novos pacotes R](install-additional-r-packages-on-sql-server.md)
+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Habilitar o gerenciamento remoto de pacotes R](r-package-how-to-enable-or-disable.md)
+ [Funções de RevoScaleR para o gerenciamento de pacotes R](use-revoscaler-to-manage-r-packages.md)
+ [Sincronização de pacotes R](package-install-uninstall-and-sync.md)
+ [miniCRAN para o repositório local de pacotes R](create-a-local-package-repository-using-minicran.md)
