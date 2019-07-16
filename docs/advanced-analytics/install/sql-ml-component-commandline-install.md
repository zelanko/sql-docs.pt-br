---
title: Instalação de componentes de R e Python – Machine Learning do SQL Server do prompt de comando
description: Execute a instalação de linha de comando do SQL Server para adicionar a linguagem R e a integração do Python para uma instância do mecanismo de banco de dados do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6ffd4b13d5ab92187ac998fd983e8fa8416e4401
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962890"
---
# <a name="install-sql-server-machine-learning-r-and-python-components-from-the-command-line"></a>Instalar componentes da linha de comando do R e Python de aprendizado de máquina do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece instruções para instalar componentes de uma linha de comando de aprendizado de máquina de SQL Server:

+ [Instância de novo no banco de dados](#indb)
+ [Adicionar a uma instância de mecanismo de banco de dados existente](#add-existing)
+ [Instalação silenciosa](#silent)
+ [Novo servidor autônomo](#shared-feature)

Você pode especificar interação silenciosa, básica ou completa com a interface do usuário de instalação. Este artigo complementa [instalar o SQL Server do Prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), abordando os parâmetros exclusivos para R e Python componentes de aprendizado de máquina.

## <a name="pre-install-checklist"></a>Lista de verificação de pré-instalação

+ Execute comandos em um prompt de comando elevado. 

+ Uma instância do mecanismo de banco de dados é necessária para instalações no banco de dados. Não é possível instalar apenas recursos de R ou Python, embora você possa [adicioná-los incrementalmente a uma instância existente](#add-existing). Se você quiser apenas R e Python, sem que o mecanismo de banco de dados, instale o [servidor autônomo](#shared-feature).

+ Não instale em um cluster de failover. O mecanismo de segurança usado para isolar processos de R e Python não é compatível com um ambiente de cluster de failover do Windows Server.

+ Não instale em um controlador de domínio. A parte de serviços de Machine Learning da instalação falhará.

+ Evite a instalação autônoma e instâncias no banco de dados no mesmo computador. Um servidor autônomo competirão pelos mesmos recursos, prejudicando o desempenho de ambas as instalações.


## <a name="command-line-arguments"></a>Argumentos de linha de comando

O argumento de recursos é necessário, como são contratos de termo de licença. 

Quando você instala pelo prompt de comando, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao modo silencioso completo usando o parâmetro /Q ou o modo Silencioso Simples usando o parâmetro /QS. A opção /QS mostra apenas o andamento, não aceita nenhuma entrada e não exibe nenhuma mensagem de erro, se encontrado. O parâmetro /QS só tem suporte quando /Action=install é especificado.

| Argumentos | Descrição |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | Instala a versão no banco de dados: Serviços de Machine Learning do SQL Server 2017 (no banco de dados) ou SQL Server 2016 R Services (no banco de dados).  |
| /FEATURES = SQL_INST_MR | Aplica-se ao SQL Server 2017 apenas. Combinar isso com AdvancedAnalytics. Instala o recurso (no banco de dados) R, incluindo Microsoft R Open e pacotes de R proprietários. O recurso do SQL Server 2016 R Services é R somente, portanto, não há nenhum parâmetro para essa versão.|
| /FEATURES = SQL_INST_MPY | Aplica-se ao SQL Server 2017 apenas. Combinar isso com AdvancedAnalytics. Instala o recurso de Python (no banco de dados), incluindo Anaconda e os pacotes do Python proprietários. |
| /FEATURES = SQL_SHARED_MR | Instala o recurso do R para a versão autônoma: SQL Server 2017 Machine Learning Server (autônomo) ou SQL Server 2016 R Server (autônomo). Um servidor autônomo é um "recurso compartilhado" não associado a uma instância do mecanismo de banco de dados.|
| /FEATURES = SQL_SHARED_MPY | Aplica-se ao SQL Server 2017 apenas. Instala o recurso de Python para a versão autônoma: SQL Server 2017 Machine Learning Server (autônomo). Um servidor autônomo é um "recurso compartilhado" não associado a uma instância do mecanismo de banco de dados.|
| /IACCEPTROPENLICENSETERMS  | Indica que você aceitou os termos de licença para usar os componentes de R de software livre. |
| /IACCEPTPYTHONLICENSETERMS | Indica que você aceitou os termos de licença para usar os componentes do Python. |
| /IACCEPTSQLSERVERLICENSETERMS | Indica que você aceitou os termos de licença para usar o SQL Server.|
| /MRCACHEDIRECTORY | Para a instalação offline, define a pasta que contém os arquivos de CAB do componente de R. |
| / MPYCACHEDIRECTORY | Reservado para uso futuro. Use % TEMP % para armazenar arquivos de CAB do componente de Python para instalação em computadores que não têm uma conexão de internet. |


## <a name="indb"></a> No banco de dados instalações de instâncias

Análise no banco de dados está disponível para instâncias do mecanismo de banco de dados, necessárias para adicionar o **AdvancedAnalytics** recurso à sua instalação. Você pode instalar uma instância do mecanismo de banco de dados com análise avançada, ou [adicioná-lo a uma instância existente](#add-existing). 

Para exibir informações sobre o andamento sem a interativa na tela prompts, use o argumento /qs.

> [!IMPORTANT]
> Após a instalação, as duas etapas adicionais de configuração permanecem. Integração não será concluída até que essas tarefas são executadas. Ver [tarefas pós-instalação](#post-install) para obter instruções.

### <a name="sql-server-2017-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server 2017: mecanismo de banco de dados, análises avançadas com Python e R

Para uma instalação simultânea da instância do mecanismo de banco de dados, forneça o nome da instância e um logon de administrador (Windows). Inclua recursos para instalação de núcleo e componentes de linguagem, bem como a aceitação dos termos de licenciamento de todos os.

```cmd
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Esse mesmo comando, mas com um logon do SQL Server em um mecanismo de banco de dados usando autenticação mista.

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Este exemplo é Python, mostrando que você pode adicionar um idioma, omitindo um recurso.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```

### <a name="sql-server-2016-database-engine-and-advanced-analytics-with-r"></a>SQL Server 2016: mecanismo de banco de dados e análises avançadas com R

Esse comando é idêntico ao SQL Server 2017, mas sem os elementos do Python, que não estão disponível na instalação do SQL Server 2016.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```

## <a name="post-install"></a> Configuração de pós-instalação (obrigatória)

Aplica-se no banco de dados somente de instalações.

Quando a instalação for concluída, você tem uma instância do mecanismo de banco de dados com pacotes de R e Python, o Microsoft R e Python, Microsoft R Open, Anaconda, ferramentas, exemplos e scripts que fazem parte da distribuição. 

Duas tarefas mais são necessárias para concluir a instalação:

1. Reinicie o serviço de mecanismo de banco de dados.

1. Habilite scripts externos antes de poder usar o recurso. Siga as instruções em [instalar o SQL Server 2017 serviços Machine Learning (no banco de dados)](sql-machine-learning-services-windows-install.md) como sua próxima etapa. 

Para o SQL Server 2016, use este artigo em vez disso [instalar o SQL Server 2016 R Services (no banco de dados)](sql-r-services-windows-install.md).

## <a name="add-existing"></a> Adicionar análises avançadas para uma instância de mecanismo de banco de dados existente

Ao adicionar a análise avançada no banco de dados a uma instância de mecanismo de banco de dados existente, forneça o nome de instância. Por exemplo, se você instalou anteriormente um mecanismo de banco de dados do SQL Server 2017 e Python, você pode usar esse comando para adicionar o R.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```



## <a name="silent"></a> Instalação silenciosa

Uma instalação silenciosa suprime a verificação de locais de arquivo. cab. Por esse motivo, você deve especificar o local em que os arquivos. cab devem ser descompactada. Para Python, arquivos CAB devem estar localizados em % TEMP *. Para R, você pode definir a pasta de caminho usando, você pode o diretório temporário para isso.
 
```cmd  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% 
```

## <a name="shared-feature"></a> Instalações autônomas de servidores

Um servidor autônomo é um "recurso compartilhado" não associado a uma instância do mecanismo de banco de dados. Os exemplos a seguir mostram a sintaxe válida para ambas as versões.

SQL Server 2017 dá suporte ao Python e R em um servidor autônomo:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

SQL Server 2016 é somente para R:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

Quando a instalação for concluída, você deve ter um servidor, pacotes da Microsoft, as distribuições de software livre de R e Python, ferramentas, exemplos e scripts que fazem parte da distribuição. 

Abra uma janela de console do R, \R_SERVER\bin\x64 go \Program files\Microsoft SQL Server\140 (ou 130) e clique duas vezes **RGui.exe**. Você é novo no R? Experimente esse tutorial: [Comandos básicos de R e funções de RevoScaleR: exemplos comuns de 25](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler).

Para abrir um comando do Python, vá para \Program Server\140\PYTHON_SERVER\bin\x64 SQL e clique duas vezes em **python.exe**.

## <a name="get-help"></a>Obter ajuda

Precisa de ajuda com a instalação ou atualização? Para obter respostas a perguntas comuns e problemas conhecidos, consulte o artigo a seguir:

* [Atualização e instalação perguntas Frequentes - serviços de Machine Learning](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Para verificar o status da instalação da instância e corrigir problemas comuns, experimente estes relatórios personalizados.

* [Relatórios personalizados para o SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores do R podem começar com alguns exemplos simples e aprender os fundamentos de como o R funciona com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Executar R no T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise no banco de dados para os desenvolvedores do R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Os desenvolvedores de Python podem aprender como usar o Python com o SQL Server seguindo estes tutoriais:

+ [Tutorial: Execute o Python no T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análise no banco de dados para desenvolvedores do Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina com base em cenários do mundo real, consulte [tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).