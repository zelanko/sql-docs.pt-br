---
title: Instalar por meio de um prompt de comando
description: Execute a instalação da linha de comando do SQL Server para adicionar a linguagem R e a integração do Python a uma instância do mecanismo de banco de dados do SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/04/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b3c3d469cb016a562f069473923f470ce750dd5e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883899"
---
# <a name="install-sql-server-machine-learning-r-and-python-components-from-the-command-line"></a>Instale componentes de Python e R do aprendizado de máquina do SQL Server usando a linha de comando
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

Este artigo fornece instruções para instalar componentes de aprendizado de máquina do SQL Server usando uma linha de comando:

+ [Nova instância no banco de dados](#indb)
+ [Adicionar a uma instância de mecanismo de banco de dados existente](#add-existing)
+ [Instalação silenciosa](#silent)
+ [Novo servidor autônomo](#shared-feature)

Você pode especificar a interação silenciosa, básica ou completa com a interface do usuário de Instalação. Este artigo complementa o artigo [Instalar o SQL Server do prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), que aborda parâmetros exclusivos dos componentes de aprendizado de máquina de R e Python.

## <a name="pre-install-checklist"></a>Lista de verificação pré-instalação

+ Execute os comandos de um prompt de comandos com privilégios elevados. 

+ Para instalações no banco de dados, uma instância do mecanismo de banco de dados é necessária. Não é possível instalar apenas os recursos do R ou do Python, embora seja possível [adicioná-los incrementalmente a uma instância existente](#add-existing). Se quiser apenas o R e o Python sem o mecanismo de banco de dados, instale o [servidor autônomo](#shared-feature).

+ Não instale em um cluster de failover. O mecanismo de segurança usado para isolar processos de R e Python não é compatível com um ambiente de cluster de failover do Windows Server.

+ Não instale em um controlador de domínio. A parte dos Serviços de Machine Learning da instalação falhará.

+ Evite instalar instâncias autônomas e no banco de dados no mesmo computador. Um servidor autônomo competirá pelos mesmos recursos, prejudicando o desempenho das duas instalações.


## <a name="command-line-arguments"></a>Argumentos de linha de comando

O argumento FEATURES é obrigatório, assim como os contratos de termo de licenciamento. 

Quando você instala pelo prompt de comando, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao modo silencioso completo usando o parâmetro /Q ou o modo Silencioso Simples usando o parâmetro /QS. A opção /QS mostra apenas o andamento, não aceita nenhuma entrada e não exibe nenhuma mensagem de erro, se encontrado. O parâmetro /QS só tem suporte quando /Action=install é especificado.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
| Argumentos | Descrição |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | Instala a versão no banco de dados: SQL Server R Services (no banco de dados).  |
| /FEATURES = SQL_SHARED_MR | Instala o recurso de R para a versão autônoma: SQL Server R Server (autônomo). Um servidor autônomo é um "recurso compartilhado" não associado a uma instância do mecanismo de banco de dados.|
| /IACCEPTROPENLICENSETERMS  | Indica que você aceitou os termos de licença para usar os componentes de software livre do R. |
| /IACCEPTPYTHONLICENSETERMS | Indica que você aceitou os termos de licença para usar os componentes do Python. |
| /IACCEPTSQLSERVERLICENSETERMS | Indica que você aceitou os termos de licença para usar o SQL Server.|
| MRCACHEDIRECTORY | Para a instalação offline, define a pasta que contém os arquivos CAB do componente de R. |
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
| Argumentos | Descrição |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | Instala a versão no banco de dados: Serviços de Machine Learning do SQL Server (no banco de dados).  |
| /FEATURES = SQL_INST_MR | Use em conjunto com AdvancedAnalytics. Instala o recurso de R (no banco de dados), incluindo o Microsoft R Open e os pacotes de R proprietários. |
| /FEATURES = SQL_INST_MPY | Use em conjunto com AdvancedAnalytics. Instala o recurso de Python (no banco de dados), incluindo o Anaconda e os pacotes de Python proprietários. |
| /FEATURES = SQL_SHARED_MR | Instala o recurso de R para a versão autônoma: SQL Server Machine Learning Server (autônomo). Um servidor autônomo é um "recurso compartilhado" não associado a uma instância do mecanismo de banco de dados.|
| /FEATURES = SQL_SHARED_MPY | Instala o recurso de Python para a versão autônoma: SQL Server Machine Learning Server (autônomo). Um servidor autônomo é um "recurso compartilhado" não associado a uma instância do mecanismo de banco de dados.|
| /IACCEPTROPENLICENSETERMS  | Indica que você aceitou os termos de licença para usar os componentes de software livre do R. |
| /IACCEPTPYTHONLICENSETERMS | Indica que você aceitou os termos de licença para usar os componentes do Python. |
| /IACCEPTSQLSERVERLICENSETERMS | Indica que você aceitou os termos de licença para usar o SQL Server.|
| MRCACHEDIRECTORY | Para a instalação offline, define a pasta que contém os arquivos CAB do componente de R. |
| MPYCACHEDIRECTORY | Reservado para uso futuro. Use %TEMP% para armazenar arquivos CAB do componente de Python para instalação em computadores que não têm uma conexão com a Internet. |
::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
| Argumentos | Descrição |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | Instala a versão no banco de dados: Serviços de Machine Learning do SQL Server (no banco de dados).  |
| /FEATURES = SQL_INST_MR | Use em conjunto com AdvancedAnalytics. Instala o recurso de R (no banco de dados), incluindo o Microsoft R Open e os pacotes de R proprietários. |
| /FEATURES = SQL_INST_MPY | Use em conjunto com AdvancedAnalytics. Instala o recurso de Python (no banco de dados), incluindo o Anaconda e os pacotes de Python proprietários. |
| /FEATURES = SQL_INST_MJAVA | Use em conjunto com AdvancedAnalytics. Instala o recurso Java (no banco de dados), incluindo o Open JRE. |
| /FEATURES = SQL_SHARED_MR | Instala o recurso de R para a versão autônoma: SQL Server Machine Learning Server (autônomo). Um servidor autônomo é um "recurso compartilhado" não associado a uma instância do mecanismo de banco de dados.|
| /FEATURES = SQL_SHARED_MPY | Instala o recurso de Python para a versão autônoma: SQL Server Machine Learning Server (autônomo). Um servidor autônomo é um "recurso compartilhado" não associado a uma instância do mecanismo de banco de dados.|
| /IACCEPTROPENLICENSETERMS  | Indica que você aceitou os termos de licença para usar os componentes de software livre do R. |
| /IACCEPTPYTHONLICENSETERMS | Indica que você aceitou os termos de licença para usar os componentes do Python. |
| /IACCEPTSQLSERVERLICENSETERMS | Indica que você aceitou os termos de licença para usar o SQL Server.|
| MRCACHEDIRECTORY | Para a instalação offline, define a pasta que contém os arquivos CAB do componente de R. |
| MPYCACHEDIRECTORY | Reservado para uso futuro. Use %TEMP% para armazenar arquivos CAB do componente de Python para instalação em computadores que não têm uma conexão com a Internet. |
::: moniker-end

## <a name="in-database-instance-installations"></a><a name="indb"></a> Instalações da instância no banco de dados

A análise no banco de dados está disponível para instâncias do mecanismo de banco de dados, necessárias para adicionar o recurso **AdvancedAnalytics** à sua instalação. Você pode instalar uma instância do mecanismo de banco de dados com análise avançada ou [adicioná-la a uma instância existente](#add-existing). 

Para exibir informações de progresso sem os prompts de tela interativos, use o argumento /qs.

> [!IMPORTANT]
> Após a instalação, restam duas etapas de configuração adicionais. A integração não é concluída até que essas tarefas sejam executadas. Confira [Tarefas pós-instalação](#post-install) para obter instruções.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
### <a name="sql-server-machine-learning-services-database-engine-advanced-analytics-with-python-and-r"></a>Serviços de Machine Learning do SQL Server: mecanismo de banco de dados, análise avançada com Python e R

Para instalação simultânea da instância do mecanismo de banco de dados, forneça o nome da instância e um logon do administrador (Windows). Inclua os recursos para instalar componentes de núcleo e de linguagem, bem como a aceitação de todos os termos de licenciamento.

```cmd
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Este é o mesmo comando, mas com um logon do SQL Server em um mecanismo de banco de dados usando autenticação mista.

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Este exemplo é referente somente ao Python, mostrando que você pode adicionar uma linguagem omitindo um recurso.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
### <a name="sql-server-r-services-database-engine-and-advanced-analytics-with-r"></a>SQL Server R Services: mecanismo de banco de dados e análise avançada com R

Para instalação simultânea da instância do mecanismo de banco de dados, forneça o nome da instância e um logon do administrador (Windows). Inclua os recursos para instalar componentes de núcleo e de linguagem, bem como a aceitação de todos os termos de licenciamento.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```
::: moniker-end

## <a name="post-install-configuration-required"></a><a name="post-install"></a> Configuração pós-instalação (obrigatória)

Aplica-se apenas a instalações no banco de dados.

Quando a instalação é concluída, você tem uma instância do mecanismo de banco de dados com R e Python, os pacotes de R e Python da Microsoft, o Microsoft R Open, o Anaconda, ferramentas, amostras e scripts que fazem parte da distribuição. 

São necessárias mais duas tarefas para concluir a instalação:


::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
1. Reiniciar o serviço do mecanismo de banco de dados.

1. Serviços de Machine Learning do SQL Server: Habilite scripts externos para usar o recurso. Siga as instruções em [Instalar os Serviços de Machine Learning do SQL Server (no Banco de Dados)](sql-machine-learning-services-windows-install.md) como a próxima etapa. 
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. Reiniciar o serviço do mecanismo de banco de dados.

1. SQL Server R Services: Habilite scripts externos para usar o recurso. Siga as instruções em [Instalar o SQL Server R Services (no Banco de Dados)](sql-r-services-windows-install.md) como a próxima etapa. 
::: moniker-end

## <a name="add-advanced-analytics-to-an-existing-database-engine-instance"></a><a name="add-existing"></a> Adicionar análise avançada a uma instância de mecanismo de banco de dados existente

Ao adicionar análise avançada no banco de dados a uma instância do mecanismo de banco de dados existente, forneça o nome da instância. Por exemplo, se tiver instalado um mecanismo de banco de dados do SQL Server 2017 ou posterior e o Python, você poderá usar esse comando para adicionar o R.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```

## <a name="silent-install"></a><a name="silent"></a> Instalação silenciosa

Uma instalação silenciosa suprime a verificação dos locais de arquivos .cab. Por esse motivo, você precisa especificar a localização em que os arquivos .cab devem ser desempacotados. Para Python, os arquivos CAB devem estar em %TEMP*. Para R, você pode definir o caminho da pasta usando o diretório temporário.
 
```cmd  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% 
```

## <a name="standalone-server-installations"></a><a name="shared-feature"></a> Instalações do servidor autônomo

Um servidor autônomo é um "recurso compartilhado" não associado a uma instância do mecanismo de banco de dados. Os exemplos a seguir mostram uma sintaxe válida para a instalação do servidor autônomo.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
O SQL Server Machine Learning Server dá suporte a Python e R em um servidor autônomo:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server R Server é destinado somente ao R:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```
::: moniker-end

Quando a instalação for concluída, você terá um servidor, pacotes da Microsoft, distribuições open-source de R e Python, ferramentas, amostras e scripts que fazem parte da distribuição. 

Para abrir uma janela do console do R, vá para `\Program files\Microsoft SQL Server\150 (or 140/130)\R_SERVER\bin\x64` e clique duas vezes em **RGui.exe**. Você é novo no R? Experimente este tutorial: [Comandos básicos de R e funções RevoScaleR: 25 exemplos comuns](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler).

Para abrir um comando do Python, vá para `\Program files\Microsoft SQL Server\150 (or 140)\PYTHON_SERVER\bin\x64` e clique duas vezes em **Python.exe**.

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do Python podem aprender a usar o Python com o SQL Server seguindo estes tutoriais:

+ [Tutorial do Python: Prever o aluguel de esquis com regressão linear nos Serviços de Machine Learning do SQL Server](../tutorials/python-ski-rental-linear-regression-deploy-model.md)
+ [Tutorial do Python: Categorizar clientes que usam cluster K-means com Serviços de Machine Learning do SQL Server](../tutorials/python-clustering-model.md)

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, confira os links a seguir:

+ [Início Rápido: Executar o R no T-SQL](../tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análise interna no banco de dados para desenvolvedores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)