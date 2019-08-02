---
title: Instalação de prompt de comando de componentes R e Python
description: Execute SQL Server configuração de linha de comando para adicionar a linguagem R e a integração do Python a uma instância do mecanismo de banco de dados SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3e1e74c9d14c93cf44a7da5db4795a1524d238be
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715268"
---
# <a name="install-sql-server-machine-learning-r-and-python-components-from-the-command-line"></a>Instalar SQL Server componentes de R e Python do Machine Learning na linha de comando
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece instruções para instalar SQL Server componentes de Machine Learning de uma linha de comando:

+ [Nova instância no banco de dados](#indb)
+ [Adicionar a uma instância do mecanismo de banco de dados existente](#add-existing)
+ [Instalação silenciosa](#silent)
+ [Novo servidor autônomo](#shared-feature)

Você pode especificar a interação silenciosa, básica ou completa com a interface do usuário de instalação. Este artigo complementa a [instalação SQL Server do prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), cobrindo os parâmetros exclusivos dos componentes de aprendizado de máquina R e Python.

## <a name="pre-install-checklist"></a>Lista de verificação de pré-instalação

+ Execute comandos de um prompt de comandos com privilégios elevados. 

+ Uma instância do mecanismo de banco de dados é necessária para instalações no banco de dados. Você não pode instalar apenas os recursos do R ou do Python, embora possa [adicioná-los incrementalmente a uma instância existente](#add-existing). Se você quiser apenas R e Python sem o mecanismo de banco de dados, instale o [servidor autônomo](#shared-feature).

+ Não instale em um cluster de failover. O mecanismo de segurança usado para isolar os processos de R e Python não é compatível com um ambiente de cluster de failover do Windows Server.

+ Não instale o em um controlador de domínio. A parte Serviços de Machine Learning da instalação falhará.

+ Evite instalar instâncias autônomas e no banco de dados no mesmo computador. Um servidor autônomo competirá pelos mesmos recursos, submineração do desempenho de ambas as instalações.


## <a name="command-line-arguments"></a>Argumentos de linha de comando

O argumento FEATURES é necessário, assim como contratos de termo de licenciamento. 

Quando você instala pelo prompt de comando, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao modo silencioso completo usando o parâmetro /Q ou o modo Silencioso Simples usando o parâmetro /QS. A opção /QS mostra apenas o andamento, não aceita nenhuma entrada e não exibe nenhuma mensagem de erro, se encontrado. O parâmetro /QS só tem suporte quando /Action=install é especificado.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
| Argumentos | Descrição |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | Instala a versão no banco de dados: SQL Server R Services (no banco de dados).  |
| /FEATURES = SQL_SHARED_MR | Instala o recurso R para a versão autônoma: SQL Server R Server (autônomo). Um servidor autônomo é um "recurso compartilhado" não associado a uma instância do mecanismo de banco de dados.|
| /IACCEPTROPENLICENSETERMS  | Indica que você aceitou os termos de licença para usar os componentes de software livre do R. |
| /IACCEPTPYTHONLICENSETERMS | Indica que você aceitou os termos de licença para usar os componentes do Python. |
| /IACCEPTSQLSERVERLICENSETERMS | Indica que você aceitou os termos de licença para usar SQL Server.|
| /MRCACHEDIRECTORY | Para a instalação offline, define a pasta que contém os arquivos CAB do componente do R. |
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
| Argumentos | Descrição |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | Instala a versão no banco de dados: SQL Server Serviços de Machine Learning (no banco de dados).  |
| /FEATURES = SQL_INST_MR | Emparelhe isso com AdvancedAnalytics. Instala o recurso R (no banco de dados), incluindo o Microsoft R Open e os pacotes de R proprietários. |
| /FEATURES = SQL_INST_MPY | Emparelhe isso com AdvancedAnalytics. Instala o recurso Python (no banco de dados), incluindo Anaconda e os pacotes python proprietários. |
| /FEATURES = SQL_SHARED_MR | Instala o recurso R para a versão autônoma: SQL Server Machine Learning Server (autônomo). Um servidor autônomo é um "recurso compartilhado" não associado a uma instância do mecanismo de banco de dados.|
| /FEATURES = SQL_SHARED_MPY | Instala o recurso Python para a versão autônoma: SQL Server Machine Learning Server (autônomo). Um servidor autônomo é um "recurso compartilhado" não associado a uma instância do mecanismo de banco de dados.|
| /IACCEPTROPENLICENSETERMS  | Indica que você aceitou os termos de licença para usar os componentes de software livre do R. |
| /IACCEPTPYTHONLICENSETERMS | Indica que você aceitou os termos de licença para usar os componentes do Python. |
| /IACCEPTSQLSERVERLICENSETERMS | Indica que você aceitou os termos de licença para usar SQL Server.|
| /MRCACHEDIRECTORY | Para a instalação offline, define a pasta que contém os arquivos CAB do componente do R. |
| /MPYCACHEDIRECTORY | Reservado para uso futuro. Use% TEMP% para armazenar arquivos CAB do componente do Python para instalação em computadores que não têm uma conexão com a Internet. |
::: moniker-end

## <a name="indb"></a>Instalações da instância no banco de dados

A análise no banco de dados está disponível para instâncias do mecanismo de banco de dados, necessárias para adicionar o recurso **AdvancedAnalytics** à sua instalação. Você pode instalar uma instância do mecanismo de banco de dados com análise avançada ou [adicioná-la a uma instância existente](#add-existing). 

Para exibir as informações de progresso sem os prompts de tela interativos, use o argumento/QS.

> [!IMPORTANT]
> Após a instalação, duas etapas de configuração adicionais permanecem. A integração não é concluída até que essas tarefas sejam executadas. Consulte [tarefas pós-instalação](#post-install) para obter instruções.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
### <a name="sql-server-machine-learning-services-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server Serviços de Machine Learning: mecanismo de banco de dados, análise avançada com Python e R

Para uma instalação simultânea da instância do mecanismo de banco de dados, forneça o nome da instância e um logon do administrador (Windows). Inclua recursos para instalar componentes de núcleo e idioma, bem como a aceitação de todos os termos de licenciamento.

```cmd
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Este é o mesmo comando, mas com um SQL Server logon em um mecanismo de banco de dados usando autenticação mista.

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Este exemplo é somente Python, mostrando que você pode adicionar um idioma omitindo um recurso.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
### <a name="sql-server-r-services-database-engine-and-advanced-analytics-with-r"></a>SQL Server R Services: mecanismo de banco de dados e análise avançada com R

Para uma instalação simultânea da instância do mecanismo de banco de dados, forneça o nome da instância e um logon do administrador (Windows). Inclua recursos para instalar componentes de núcleo e idioma, bem como a aceitação de todos os termos de licenciamento.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```
::: moniker-end

## <a name="post-install"></a>Configuração pós-instalação (obrigatória)

Aplica-se somente a instalações no banco de dados.

Quando a instalação for concluída, você terá uma instância do mecanismo de banco de dados com R e Python, os pacotes Microsoft R e Python, Microsoft R Open, Anaconda, Tools, samples e scripts que fazem parte da distribuição. 

Mais duas tarefas são necessárias para concluir a instalação:


::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
1. Reinicie o serviço do mecanismo de banco de dados.

1. SQL Server Serviços de Machine Learning: Habilite scripts externos antes de poder usar o recurso. Siga as instruções em [instalar SQL Server serviços de Machine Learning (no banco de dados)](sql-machine-learning-services-windows-install.md) como a próxima etapa. 
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. Reinicie o serviço do mecanismo de banco de dados.

1. SQL Server R Services: Habilite scripts externos antes de poder usar o recurso. Siga as instruções em [instalar SQL Server R Services (no banco de dados)](sql-r-services-windows-install.md) como a próxima etapa. 
::: moniker-end

## <a name="add-existing"></a>Adicionar análise avançada a uma instância do mecanismo de banco de dados existente

Ao adicionar a análise avançada no banco de dados a uma instância do mecanismo de banco de dados existente, forneça o nome da instância. Por exemplo, se você tiver instalado anteriormente um mecanismo de banco de dados SQL Server 2017 e Python, poderá usar esse comando para adicionar R.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```

## <a name="silent"></a>Instalação silenciosa

Uma instalação silenciosa suprime a verificação de locais de arquivo. cab. Por esse motivo, você deve especificar o local onde os arquivos. cab devem ser desempacotados. Para Python, os arquivos CAB devem estar localizados em% TEMP *. Para o R, você pode definir o caminho da pasta usando o diretório Temp para isso.
 
```cmd  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% 
```

## <a name="shared-feature"></a>Instalações de servidor autônomo

Um servidor autônomo é um "recurso compartilhado" não associado a uma instância do mecanismo de banco de dados. Os exemplos a seguir mostram uma sintaxe válida para a instalação do servidor autônomo.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
SQL Server Machine Learning Server dá suporte a Python e R em um servidor autônomo:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server R Server é somente R:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```
::: moniker-end

Quando a instalação for concluída, você terá um servidor, pacotes da Microsoft, distribuições de software livre de R e Python, ferramentas, exemplos e scripts que fazem parte da distribuição. 

Para abrir uma janela do console do R, `\Program files\Microsoft SQL Server\150 (or 140/130)\R_SERVER\bin\x64` vá para e clique duas vezes em **RGui. exe**. Você é novo no R? Experimente este tutorial: [Comandos básicos de R e funções RevoScaleR: 25 exemplos](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)comuns.

Para abrir um comando do Python, vá `\Program files\Microsoft SQL Server\150 (or 140)\PYTHON_SERVER\bin\x64` para e clique duas vezes em **Python. exe**.

## <a name="get-help"></a>Obter ajuda

Precisa de ajuda com a instalação ou atualização? Para obter respostas a perguntas comuns e problemas conhecidos, consulte o seguinte artigo:

* [Perguntas frequentes sobre atualização e instalação-Serviços de Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Para verificar o status da instalação da instância e corrigir problemas comuns, experimente esses relatórios personalizados.

* [Relatórios personalizados para SQL Server](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores de R podem começar com alguns exemplos simples e aprender as noções básicas de como o R funciona com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Executar R no T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise no banco de dados para desenvolvedores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Os desenvolvedores de Python podem aprender a usar o Python com SQL Server seguindo estes tutoriais:

+ [Tutorial: Executar o Python no T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análise no banco de dados para desenvolvedores de Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina que se baseiam em cenários do mundo real, consulte [tutoriais do Machine Learning](../tutorials/machine-learning-services-tutorials.md).