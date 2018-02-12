---
title: "Instalação autônoma dos serviços de aprendizado de máquina | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 7d41bd73398c016b920fa67244ffea1af865bde2
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="unattended-installation-of-machine-learning-services-in-database"></a>Instalação autônoma dos serviços de aprendizado de máquina (no banco de dados)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como usar argumentos de linha de comando com a instalação do SQL Server para instalar a componentes de aprendizado de máquina.

Instalação autônoma, queremos dizer que você não usar os recursos interativos do Assistente de instalação e fornecer todos os argumentos necessários para concluir a instalação, incluindo licenciamento contratos para o SQL Server e para componentes de aprendizado de máquina em um linha de comando ou como parte de um script, normalmente no modo silencioso.

+ [SQL Server 2016 R Services](#bkmk_OldInstall)
+ [Serviços de aprendizado de máquina do SQL Server de 2017](#bkmk_NewInstall) com R ou Python
+ [Microsoft R Server ou servidor de aprendizado de máquina](../r/install-microsoft-r-server-from-the-command-line.md)

**Aplica-se a: SQL Server 2017 serviços aprendizado de máquina (no banco de dados), SQL Server 2016 R Services**

## <a name="prerequisites"></a>Prerequisites

+ Você deve instalar o mecanismo de banco de dados em cada instância onde você usará o aprendizado de máquina.

+ Se o computador não tiver acesso à Internet, certifique-se de baixar os instaladores de aprendizado de máquina componentes com antecedência. Consulte [instalação de componentes de aprendizado de máquina sem acesso à Internet](../r/installing-ml-components-without-internet-access.md).

+ Há separadas licenciamento parâmetros para cada um dos componentes de software livre de R e Python. SQL Server 2016 dá suporte a apenas R; 2017 do SQL Server dá suporte a R e Python. Você deve aceitar os termos de licença para cada idioma que deseja instalar. A instalação falha se você não incluir esse parâmetro na linha de comando.

+ Para concluir a instalação sem a necessidade de responder a prompts, certifique-se de que você identificou todos os argumentos necessários, incluindo aqueles para licenciamento e para outros recursos que deseja instalar.

+ O **Mixed** foi necessárias de modo de segurança que dá suporte a logons do SQL Server nas versões iniciais. Embora não seja necessário, considere habilitar a autenticação de modo misto dar suporte ao desenvolvimento de soluções por cientistas de dados que use um logon SQL.

> [!IMPORTANT]
> 
> Após a conclusão da instalação para habilitar o recurso, são necessárias etapas adicionais. Esses incluem uma reconfiguração e reiniciar a instância. Se revisar todos os itens na seção [etapas de pós-instalação] (#bkmk_PostInstall) para determinar as ações necessárias após a conclusão da instalação.

## <a name="bkmk_NewInstall"></a>Instalação de linha de comando do SQL Server 2017

Os exemplos a seguir incluem o **mínimo** recursos necessários.

> [!IMPORTANT]
> Certifique-se de executar todos os comandos em um prompt de comando com privilégios elevados.
> 
> Após a conclusão da instalação, algumas etapas adicionais são necessárias. Consulte [nesta seção](#bkmk_PostInstall). 
> Outra reinicialização dos serviços do SQL Server será necessária após a conclusão da configuração.

### <a name="install-r-only"></a>Instalar somente o R

O exemplo a seguir mostra os argumentos necessários para executar um silencioso, autônomo a instalação de serviços de máquina do SQL Server de 2017 (no banco de dados) com a linguagem R adicionada.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
```

Observe os sinalizadores necessários para R no SQL Server 2017:

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MR`
+ `IACCEPTROPENLICENSETERMS`.

### <a name="install-python-only"></a>Instalar somente o Python

O exemplo a seguir mostra os argumentos necessários para executar um silencioso, autônomo a instalação de serviços de máquina do SQL Server de 2017 (no banco de dados) com a linguagem Python adicionada.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

Observe os sinalizadores necessários para Python no SQL Server 2017:

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MPY`
+ `IACCEPTPYTHONOPENLICENSETERMS`

### <a name="install-both-r-and-python-on-a-named-instance"></a>Instalar o R e Python em uma instância nomeada

O exemplo a seguir mostra os argumentos necessários para executar um silencioso, autônomo a instalação de serviços de máquina do SQL Server de 2017 (no banco de dados) em uma instância nomeada. Idiomas R e Python são adicionados.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER.ServerName /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

## <a name="OldInstall"></a>Instalação de linha de comando para o SQL Server 2016
 
O exemplo a seguir mostra os argumentos necessários para executar um silencioso, autônomo instalação do SQL Server 2016 com a linguagem R adicionada.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
```

Observe os sinalizadores necessários para 2016 R Services:

+ `ADVANCEDANALYTICS`
+ `IACCEPTROPENLICENSETERMS`

## <a name = "bkmk_PostInstall"></a>Etapas adicionais após a instalação

Você deve executar as etapas a seguir após a instalação do SQL Server estiver concluída, independentemente de qual versão você instalou. recursos de aprendizagem de máquina não são habilitados por padrão e devem ser explicitamente habilitados.

1.  Após a conclusão da instalação, abra uma nova **consulta** janela no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], e execute o seguinte comando para habilitar o recurso.
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  Você deve habilitar explicitamente o recurso e reconfigure; Caso contrário, não será possível chamar scripts externos, mesmo que o recurso tenha sido instalado.
  
2.  Reinicie o serviço do SQL Server para a instância reconfigurado. Isso reiniciará automaticamente relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] serviço também.

> [!IMPORTANT]
> 
> Algumas etapas adicionais podem ser necessárias se você tiver uma configuração de segurança personalizada, ou se você estiver usando o SQL Server como um contexto de computação ao executar o código de R ou Python de um cliente remoto. 
> 
> Para obter mais informações, consulte [perguntas frequentes sobre atualização e instalação](../../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md).
