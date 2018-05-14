---
title: Padrão de R e Python bibliotecas de pacote no SQL Server R e aprendizado de máquina do SQL Server | Microsoft Docs
description: Pacotes de R e Python instalados pelo SQL Server para serviços de aprendizado de máquina do serviços de R, R Server (no banco de dados) e o servidor de aprendizado de máquina (autônomo)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/08/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9df4ec00d1800ebfbe8725d26d4bf220eda49566
ms.sourcegitcommit: feff98b3094a42f345a0dc8a31598b578c312b38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2018
---
# <a name="default-r-and-python-packages-in-sql-server"></a>Pacotes R padrão e Python no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo aborda as bibliotecas do pacote, o local e as versões dos pacotes de R e Python instalados com o SQL Server. 

## <a name="using-the-default-instance-library"></a>Usando a biblioteca de instância padrão

Quando você instala o aprendizado de máquina com o SQL Server, uma biblioteca de pacote único é criada no nível de instância para cada idioma que deseja instalar. 

Todos os script ou código que é executado no banco de dados no SQL Server deve carregar as funções da biblioteca de instância. SQL Server não pode acessar pacotes instalados em outras bibliotecas. Aplica-se os clientes remotos. Ao se conectar ao servidor de um cliente remoto, qualquer código de R ou Python que você deseja executar no contexto de computação do servidor só pode usar pacotes instalados na biblioteca de instância.

Para proteger os ativos do servidor, a biblioteca de instância padrão é instalada em uma pasta protegida que está registrada com o SQL Server e pode ser modificada somente por um administrador do computador. Se você não for o proprietário do computador, você precisará obter permissão do administrador para instalar os pacotes para essa biblioteca. 

Mesmo se você tiver o computador, você deve considerar a utilidade de qualquer pacote de R ou Python específico em um ambiente de servidor antes de adicionar o pacote para a biblioteca de instância. Considere os fatores como o tamanho dos arquivos de pacote e a necessidade de várias versões, bem como a necessidade do pacote de rede ou internet acesso.

### <a name="in-database-engine-instance-file-paths"></a>Caminhos de arquivo de instância do mecanismo de banco de dados

A tabela a seguir mostra o local do arquivo de R e Python para o banco de dados e versão combinações de instância do mecanismo. MSSQL13 indica o SQL Server 2016 e é somente para R. MSSQL14 indica 2017 do SQL Server e tiver pastas de R e Python. 

Caminhos de arquivo também incluem os nomes de instância. O SQL Server instala [instâncias do mecanismo de banco de dados](../../database-engine/configure-windows/database-engine-instances-sql-server.md) como a instância padrão (MSSQLSERVER) ou como uma instância nomeada definida pelo usuário. Se o SQL Server estiver instalado como uma instância nomeada, você verá esse nome adicionada da seguinte maneira: `MSSQL13.<instance_name>`.

|Versão e idioma  | Caminho padrão|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL mssql13. MSSQLSERVER\R_SERVICES\library|
| SQL Server 2017 com R|C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\R_SERVICES\library |
| SQL Server 2017 com Python |C:\Program Files\Microsoft SQL Server\MSSQL14. Pacotes de MSSQLSERVER\PYTHON_SERVICES\Lib\site |


### <a name="standalone-server-file-paths"></a>Caminhos de arquivo de servidor autônomo 

A tabela a seguir lista os caminhos padrão de binários quando o servidor do SQL Server 2016 R (autônomo) ou o servidor do servidor do aprendizado de máquina 2017 SQL Server (autônomo) é instalado. 

|Versão| Instalação|Caminho padrão|
|-------|-------------|------------|
| SQL Server 2016|R Server (Autônomo)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Servidor com R de aprendizado de máquina |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Servidor, com Python de aprendizado de máquina |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> Se você encontrar outras pastas com nomes semelhantes de subpastas e arquivos, você provavelmente tem uma instalação autônoma do Microsoft R Server ou [server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/). Esses produtos de servidor têm instaladores diferentes e caminhos (ou seja, C:\Program Files\Microsoft\R Server\R_SERVER ou C:\Program Files\Microsoft\ML SERVER\R_SERVER). Para obter mais informações, consulte [instalar Machine Learning Server para Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) ou [instalar o R Server 9.1 para Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows).

## <a name="what-is-included-in-a-default-installation"></a>O que é incluído em uma instalação padrão

Esta seção resume os recursos de R e Python incluídos em uma instalação padrão.

### <a name="r-components"></a>Componentes de R

R de código-fonte aberto é a distribuição do Microsoft [Microsoft R Open (MRO)](https://mran.microsoft.com/open). Suporte de linguagem R inclui a funcionalidade principal, como **base**, **estatísticas**, **utilitários**e outros. Uma instalação básica do R também inclui vários conjuntos de dados de exemplo e ferramentas padrão de R como **RGui** (um editor leve interativo) e **RTerm** (um prompt de comando de R). MRO adiciona o valor de base R, incluindo pacotes de código-fonte aberto adicionais, como o [biblioteca de Kernel de matemática Intel](https://en.wikipedia.org/wiki/Math_Kernel_Library).

Pacotes de proprietários R na instalação do incluem:

+ [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) para contextos de computação remota, streaming, execução paralela de funções de rx para importação de dados e de transformação, modelagem, visualização e análise. 
+ [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package) adiciona o aprendizado de máquina de modelagem em R.
+ [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) para escrever instruções MDX em R.
+ [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) para a inclusão de script R em procedimentos armazenados.

A tabela a seguir resume a versão de R fornecido pela MRO e os pacotes da Microsoft instalados com mecanismos de análise de no banco de dados específico.

|Versão             | Versão de R       | Pacotes da Microsoft    |
|--------------------|-----------------|-----------------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | RevoScaleR, sqlrutil  |
| [Serviços de aprendizado de máquina do SQL Server de 2017](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 | RevoScaleR, MicrosoftML, olapR, sqlrutil|

Você pode atualizar pacotes de componentes de R, adicionar novos pacotes de R e modelos pré-instalado por *associação* para a política de suporte do ciclo de vida modernos. Associação altera o modelo de manutenção. Por padrão, após uma instalação inicial, pacotes R são atualizados por meio de service packs e atualizações cumulativas. Outros pacotes e atualizações de versão completa dos componentes principais R só são possíveis por meio de atualizações de produto (a partir do SQL Server 2016 para 2017 do SQL Server) ou por associação R oferecer suporte ao servidor de aprendizado de máquina do Microsoft. Para obter mais informações, consulte [atualização R e Python componentes do SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="python-components"></a>Componentes do Python

SQL Server 2017 adiciona componentes de Python. Quando você seleciona a opção de linguagem Python, uma distribuição Anaconda está instalada. Além das bibliotecas de código Python, a instalação padrão inclui dados de exemplo, testes de unidade e scripts de exemplo. 

Incluem pacotes do Microsoft [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) como equivalentes Python RevoScaleR, com o streaming, execução paralela de funções de rx para importação de dados e transformação, modelagem, visualização e análise. Outro pacote do Python é [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) para treinamento e transformações, análise de pontuação, texto e imagem e extração de um recurso para derivar valores de dados existentes.

Aprendizado de máquina do SQL Server de 2017 é a primeira versão R e suporte de Python.

|Versão             | Versão anaconda| Pacotes da Microsoft    |
|--------------------|-----------------|-----------------------|
| Serviços de Machine Learning do SQL Server 2017  | 4.2 em Python 3.5 | revoscalepy, microsoftml |

Após uma instalação inicial, Python pacotes são atualizados por meio de service packs e atualizações cumulativas, mas as atualizações de versão completo somente são possíveis associando o suporte do Python para o servidor de aprendizado de máquina do Microsoft. Para obter mais informações, consulte [atualização R e Python componentes do SQL Server](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="administrative-permissions-for-package-installation"></a>Permissões administrativas para a instalação do pacote

A biblioteca de pacote usada por uma instância no banco de dados está fisicamente localizada na pasta arquivos de programas da instância do SQL Server. A gravação nesse local requer permissões de administrador. No entanto, o SQL Server 2017 oferece algumas metodologias adicionais para a instalação do pacote que fornece a capacidade de adicionar pacotes de não-administradores.

+ No SQL Server 2016, o acesso administrativo é necessário para nova instalação do pacote.
+ No SQL Server de 2017, você pode continuar a instalar pacotes como administrador para R e Python, e isso provavelmente é o método mais fácil. 

    A instrução DDL, criar biblioteca externa, permite que o administrador de banco de dados instalar os pacotes sem usar as ferramentas de R. 

    Se você usar o recurso de gerenciamento de pacote para o servidor de aprendizado de máquina, você pode usar o RevoScaleR para instalar os pacotes de R no nível do banco de dados. O administrador de banco de dados deve habilitar o recurso e, em seguida, conceder aos usuários a capacidade de instalar seus próprios pacotes em uma base por banco de dados. Para obter mais informações, consulte [habilitar o gerenciamento de pacote usando DDLs](r-package-how-to-enable-or-disable.md).

### <a name="user-libraries-are-not-supported"></a>Não há suporte para bibliotecas do usuário

Os usuários que não é possível instalar um pacote em um local seguro, geralmente recorrem a instalação de um pacote em uma biblioteca do usuário. No entanto, isso não é possível no ambiente do SQL Server. Acesso de sistema de arquivos normalmente é restrito no servidor e, mesmo se você tiver direitos de administrador e o acesso a uma pasta de documentos do usuário no servidor, o tempo de execução do script externo que é executado no SQL Server não pode acessar todos os pacotes instalados fora da instância padrão biblioteca. No entanto, as soluções alternativas são possíveis. Para obter dicas sobre como resolver problemas relacionados às bibliotecas de usuário, consulte [soluções alternativas para bibliotecas de usuário de R](packages-installed-in-user-libraries.md).

## <a name="next-steps"></a>Próximas etapas

+ [Obter informações de pacote](determine-which-packages-are-installed-on-sql-server.md)
+ [Instalar novos pacotes de R](install-additional-r-packages-on-sql-server.md)
+ [Instalar novos pacotes do Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Habilitar o gerenciamento remoto de pacote de R](r-package-how-to-enable-or-disable.md)
+ [Funções de RevoScaleR para gerenciamento de pacotes de R](use-revoscaler-to-manage-r-packages.md)
+ [Sincronização de pacotes de R](package-install-uninstall-and-sync.md)
+ [miniCRAN para o repositório local de pacote de R](create-a-local-package-repository-using-minicran.md)
