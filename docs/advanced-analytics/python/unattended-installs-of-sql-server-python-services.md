---
title: "Instalação autônoma dos serviços de aprendizado de máquina do Python (no banco de dados) | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: r-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 810adfeca86bc12bf05561eb50d555261579a1a5
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="unattended-installation-of-python-machine-learning-services-in-database"></a>Instalação autônoma dos serviços de aprendizado de máquina do Python (no banco de dados)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tópico descreve como usar os argumentos de linha de comando na instalação do SQL Server 2017 para instalar o mecanismo de banco de dados do SQL Server com serviços de aprendizado de máquina e Python, usando o modo silencioso.

> [!NOTE]
> Não se esqueça de incluir os argumentos de linha de comando para os contratos de licença, uma para Python e outra para o SQL Server.

## <a name="prerequisites"></a>Prerequisites

Antes de iniciar o processo de instalação, observe estes requisitos:

+ Não é possível instalar o serviço de Python independentemente do mecanismo de banco de dados do SQL Server 2017. Você deve incluir o recurso de mecanismo de banco de dados SQL.
+ Se você estiver executando uma instalação offline, você deve baixar os componentes necessários do Python com antecedência e copiá-los para uma pasta local. Para locais de download, consulte [instalando os componentes de aprendizado de máquina sem acesso à Internet](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md).
+ Há um novo parâmetro, */IACCEPTPYTHONLICENSETERMS*, que indica que você aceitou os termos de licença para usar os componentes de Python fornecidos pela análise de continuidade. Se você não incluir esse parâmetro na linha de comando, a instalação falhará.
+ Para concluir a instalação sem a necessidade de responder a prompts, certifique-se de que você identificou todos os argumentos necessários, incluindo aqueles para Python e licenciamento do SQL Server e para outros recursos que deseja instalar.
+  Autenticação de modo misto foi necessária em algumas versões de pré-lançamento do SQL Server 2016. Ele não é mais necessário, que pode ser útil em cenários onde os cientistas de dados estiver desenvolvendo e testando soluções remotamente usando logons do SQL Server.

## <a name="perform-an-unattended-installation-of-python-machine-learning-services-in-database"></a>Executar uma instalação autônoma dos serviços de aprendizado de máquina do Python (no banco de dados)

A exemplo a seguir mostra o **mínimo** necessários recursos a serem especificados na linha de comando ao executar uma instalação silenciosa e autônoma do Python e o mecanismo de banco de dados na instância padrão.

> [!NOTE]
> Este recurso requer o SQL Server 2017. Não há suporte para o Python em versões anteriores do SQL Server.

1. Abra um prompt de comando com privilégios elevados e execute o seguinte comando:

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONLICENSETERMS
    ```

    > [!NOTE]
    > 
    > Há novos sinalizadores de instalação da Python: `SQL_INST_MPY` e`IACCEPTPYTHONLICENSETERMS`

2. Reinicie o servidor conforme indicado.
3. Execute as etapas de configuração após a instalação, conforme descrito em [nesta seção](#bkmk_PostInstall). Será necessário reiniciar outro dos serviços do SQL Server.

## <a name = "bkmk_PostInstall"></a>Etapas de pós-instalação

1.  Após a conclusão da instalação, abra uma nova **consulta** janela no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], e execute o seguinte comando para habilitar o recurso.

    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  Você deve habilitar explicitamente o recurso e reconfigure; Caso contrário, não será possível chamar scripts externos, mesmo que o recurso tenha sido instalado.
  
3.  Reinicie o serviço do SQL Server para a instância reconfigurado. Isso reiniciará automaticamente relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] serviço também.

3. Etapas adicionais poderão ser necessárias se você tiver uma configuração de segurança personalizada ou for usar o SQL Server para dar suporte a contextos de computação remota. Para obter mais informações, consulte [Solucionando problemas de instalação de aprendizado de máquina](../machine-learning-troubleshooting-faq.md).
