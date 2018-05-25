---
title: Instalação dos componentes de aprendizado de máquina do SQL Server do prompt de comando | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7211eda2caaf579267e4c6089be13750022f0ef8
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="install-sql-server-machine-learning-components-from-the-command-line"></a>Instalar componentes de aprendizado de máquina do SQL Server a partir da linha de comando
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece instruções para instalar os componentes de uma linha de comando de aprendizado de máquina de SQL Server:

+ [Instância de novo no banco de dados](#indb)
+ [Adicionar a uma instância de mecanismo de banco de dados existente](#add-existing)
+ [Instalação silenciosa](#silent)
+ [Novo servidor autônomo](#shared-feature)

Você pode especificar interação silenciosa, básica ou completa com a interface de usuário de instalação. Este artigo complementa [instalar o SQL Server a partir do Prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), que abrangem os parâmetros exclusivos para componentes de aprendizado de máquina de R e Python.

## <a name="pre-install-checklist"></a>Lista de verificação de pré-instalação

+ Execute comandos em um prompt de comando com privilégios elevados. 

+ Uma instância do mecanismo de banco de dados é necessária para instalações no banco de dados. Você não pode instalar apenas recursos de R ou Python, embora você possa [adicioná-los incrementalmente para uma instância existente](#add-existing). Se desejar apenas R e Python sem que o mecanismo de banco de dados, instale o [servidor autônomo](#shared-feature).

+ Não instale em um cluster de failover. O mecanismo de segurança usado para isolar processos de R e Python não é compatível com um ambiente de cluster de failover do Windows Server.

+ Não instale em um controlador de domínio. A parte de serviços de aprendizado de máquina do programa de instalação falhará.

+ Evite a instalação autônoma e instâncias no banco de dados no mesmo computador. Um servidor autônomo competirão para os mesmos recursos, prejudicando o desempenho de ambas as instalações.


## <a name="command-line-arguments"></a>Argumentos de linha de comando

O argumento de recursos é necessário, como são os contratos de termos de licença. 

Quando você instala pelo prompt de comando, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao modo silencioso completo usando o parâmetro /Q ou o modo Silencioso Simples usando o parâmetro /QS. A opção /QS mostra apenas o andamento, não aceita nenhuma entrada e não exibe nenhuma mensagem de erro, se encontrado. O parâmetro /QS só tem suporte quando /Action=install é especificado.

| Argumentos | Description |
|-----------|-------------|
| / RECURSOS = AdvancedAnalytics | Instala a versão no banco de dados: SQL Server 2017 Machine Learning Services (no banco de dados) ou SQL Server 2016 R Services (no banco de dados).  |
| /FEATURES = SQL_INST_MR | Aplica-se ao SQL Server 2017 somente. Combinar isso com AdvancedAnalytics. Instala o recurso (no banco de dados) R, incluindo Microsoft R Open e os pacotes de R proprietários. O recurso SQL Server 2016 R Services é R somente, portanto não há nenhum parâmetro para essa versão.|
| /FEATURES = SQL_INST_MPY | Aplica-se ao SQL Server 2017 somente. Combinar isso com AdvancedAnalytics. Instala o recurso de Python (no banco de dados), incluindo Anaconda e os pacotes do Python proprietários. |
| /FEATURES = SQL_SHARED_MR | Instala o recurso de R para a versão autônoma: servidor do aprendizado de máquina 2017 SQL Server (autônomo) ou o servidor do SQL Server 2016 R (autônomo). Um servidor autônomo é um "recurso compartilhado" não está associado a uma instância do mecanismo de banco de dados.|
| /FEATURES = SQL_SHARED_MPY | Aplica-se ao SQL Server 2017 somente. Instala o recurso de Python para a versão autônoma: servidor do aprendizado de máquina 2017 SQL Server (autônomo). Um servidor autônomo é um "recurso compartilhado" não está associado a uma instância do mecanismo de banco de dados.|
| /IACCEPTROPENLICENSETERMS  | Indica que você aceitou os termos de licença para usar os componentes de R de código-fonte aberto. |
| / IACCEPTPYTHONLICENSETERMS | Indica que você aceitou os termos de licença para usar os componentes de Python. |
| /IACCEPTSQLSERVERLICENSETERMS | Indica que você aceitou os termos de licença para usar o SQL Server.|
| / MRCACHEDIRECTORY | Para a instalação offline, define a pasta que contém os arquivos de CAB do componente de R. |
| / MPYCACHEDIRECTORY | Para a instalação offline, define a pasta que contém os arquivos de CAB do componente de Python. |


## <a name="indb"></a> No banco de dados instalações de instâncias

Análise de no banco de dados está disponível para instâncias do mecanismo de banco de dados necessárias para adicionar o **AdvancedAnalytics** recurso à sua instalação. Você pode instalar uma instância do mecanismo de banco de dados com análises avançadas, ou [adicioná-lo a uma instância existente](#add-existing). 

Para exibir informações sobre o andamento sem o interativo na tela prompts, use o argumento /qs.

> [!IMPORTANT]
> Após a instalação, as duas etapas de configuração adicionais permanecem. Integração não é completa até que essas tarefas são executadas. Consulte [tarefas pós-instalação](#post-install) para obter instruções.

### <a name="sql-server-2017-database-engine-advanced-analytics-with-python-and-r"></a>Do SQL Server de 2017: mecanismo de banco de dados advanced analytics com Python e R

Para uma instalação simultânea da instância do mecanismo de banco de dados, forneça o nome da instância e um logon de administrador (Windows). Incluem recursos para a instalação principal e componentes de idioma, bem como aceitação de todos os termos de licenciamento.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Esse mesmo comando, mas com um logon do SQL Server em um mecanismo de banco de dados usando autenticação mista.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Este exemplo é Python, mostrando o que você pode adicionar um idioma, omitindo um recurso.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```

### <a name="sql-server-2016-database-engine-and-advanced-analytics-with-r"></a>SQL Server 2016: mecanismo de banco de dados e análise avançada com R

Esse comando é idêntico ao SQL Server 2017, mas sem os elementos de Python, que não estão disponível na instalação do SQL Server 2016.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```

## <a name="post-install"></a> Configuração de pós-instalação (obrigatória)

Aplica-se no banco de dados somente de instalações.

Quando a instalação for concluída, você tem uma instância do mecanismo de banco de dados com pacotes de R e Python, o Microsoft R e Python, Microsoft R Open, Anaconda, ferramentas, exemplos e scripts que fazem parte da distribuição. 

Duas tarefas mais são necessários para concluir a instalação:

1. Reinicie o serviço de mecanismo de banco de dados.

1. Habilite scripts externos antes de usar o recurso. Siga as instruções em [instalar o SQL Server 2017 Machine Learning Services (no banco de dados)](sql-machine-learning-services-windows-install.md) como a próxima etapa. 

Para o SQL Server 2016, use em vez disso, este artigo [instalar o SQL Server 2016 R Services (no banco de dados)](sql-r-services-windows-install.md).

## <a name="add-existing"></a> Adicionar análise avançada para uma instância de mecanismo de banco de dados existente

Ao adicionar análises avançadas no banco de dados a uma instância de mecanismo de banco de dados existente, forneça o nome da instância. Por exemplo, se você instalou anteriormente um mecanismo de banco de dados do SQL Server 2017 e Python, você pode usar esse comando para adicionar o R.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```



## <a name="silent"></a> Instalação silenciosa

Uma instalação silenciosa suprime a verificação de locais de arquivo. cab. Por esse motivo, você deve especificar o local onde os arquivos. cab devem ser descompactada. Você pode o diretório temp para isso.
 
```  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% /MPYCACHEDIRECTORY=%temp%
```

## <a name="shared-feature"></a> Instalações autônomas de servidores

Um servidor autônomo é um "recurso compartilhado" não está associado a uma instância do mecanismo de banco de dados. Os exemplos a seguir mostram a sintaxe válida para ambas as versões.

2017 do SQL Server dá suporte a Python e R em um servidor autônomo:

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

SQL Server 2016 é somente para R:

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

Quando a instalação for concluída, você deve ter um servidor, pacotes da Microsoft, distribuições de código-fonte aberto do R e Python, ferramentas, exemplos e scripts que fazem parte da distribuição. 

Para abrir uma janela de console de R, vá para \Program files\Microsoft Server\140 SQL (ou 130) \R_SERVER\bin\x64 e clique duas vezes em **RGui.exe**. Você é novo no R? Tente este tutorial: [comandos de R básicos e funções de RevoScaleR: 25 exemplos comuns](https://docs.microsoft.com/en-us/machine-learning-server/r/tutorial-r-to-revoscaler).

Para abrir um comando do Python, vá para \Program Server\140\PYTHON_SERVER\bin\x64 SQL e clique duas vezes em **python.exe**.

## <a name="get-help"></a>Obter ajuda

Precisa de ajuda com a instalação ou atualização? Para obter respostas a perguntas comuns e problemas conhecidos, consulte o seguinte artigo:

* [Atualização e instalação perguntas Frequentes – serviços de aprendizado de máquina](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Para verificar o status da instalação da instância e corrigir problemas comuns, tente esses relatórios personalizados.

* [Relatórios personalizados do SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Próximas etapas

Os desenvolvedores de R podem começar com alguns exemplos simples e conheça os fundamentos de como funciona o R com o SQL Server. Para a próxima etapa, consulte os links a seguir:

+ [Tutorial: Executar R no T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Tutorial: Análise de no banco de dados para os desenvolvedores de R](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Os desenvolvedores de Python podem Saiba como usar o Python com o SQL Server por esses tutoriais a seguir:

+ [Tutorial: Executar Python em T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análise de no banco de dados para desenvolvedores Python](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Para exibir exemplos de aprendizado de máquina com base em cenários do mundo real, consulte [tutoriais de aprendizado de máquina](../tutorials/machine-learning-services-tutorials.md).