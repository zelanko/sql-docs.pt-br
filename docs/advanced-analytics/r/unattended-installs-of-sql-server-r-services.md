---
title: "Instalação autônoma dos serviços de aprendizado de máquina | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 18
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: babb74aa866404853cfef83e1d30159354f385e7
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="unattended-installation-of-machine-learning-services-in-database"></a>Instalação autônoma dos serviços de aprendizado de máquina (no banco de dados)

Este tópico descreve como usar argumentos de linha de comando com a instalação do SQL Server para instalar o aprendizado de máquina em uma instância do mecanismo de banco de dados, no modo silencioso. Em uma instalação autônoma, não use os recursos interativos do Assistente de instalação e forneça todos os argumentos necessários para concluir a instalação, incluindo licenciamento contratos para o SQL Server e para componentes de aprendizado de máquina.

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 Services (no banco de dados) de aprendizado de máquina

> [!IMPORTANT]
> 
> No SQL Server 2016 e no SQL Server 2017, etapas adicionais serão necessárias após a conclusão da instalação para habilitar o recurso. Esses incluem uma reconfiguração e reiniciar a instância. Certifique-se de examinar todas as etapas.

## <a name="prerequisites"></a>Pré-requisitos

+ Você deve instalar o mecanismo de banco de dados em cada instância onde você usará o aprendizado de máquina.

+ Se o computador não tiver acesso à Internet, certifique-se de instalar os instaladores de aprendizado de máquina componentes com antecedência. Para locais de download, consulte [instalação de componentes de aprendizado de máquina sem acesso à Internet](../../advanced-analytics/r/installing-ml-components-without-internet-access.md).

+ Há novos parâmetros relacionados aos componentes de software livre de R e Python de licenciamento. Você deve aceitar os termos de licença com um argumento separado para cada idioma que deseja instalar. Se você não incluir esse parâmetro na linha de comando, a instalação falhará.

+ Para concluir a instalação sem a necessidade de responder a prompts, certifique-se de que você identificou todos os argumentos necessários, incluindo aqueles para licenciamento e para outros recursos que deseja instalar.

> [!NOTE] 
> O modo de segurança mistas que dá suporte a logons do SQL Server foi necessária nas versões iniciais. No entanto, você pode considerar a habilitação da autenticação de modo misto dar suporte ao desenvolvimento de soluções por cientistas de dados usando um logon SQL.

## <a name="bkmk_NewInstall"></a>Instalação autônoma dos serviços de aprendizado de máquina com R

A exemplo a seguir mostra o **mínimo** instalam recursos necessários a serem especificados na linha de comando ao executar silencioso, autônomo dos serviços de máquina do SQL Server de 2017 (no banco de dados).

1. Abra um prompt de comando com privilégios elevados e execute o seguinte comando:

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
    ```
    
    Observe os sinalizadores necessários para R no SQL Server 2017: `ADVANCEDANALYTICS`, `SQL_INST_MR`, e `IACCEPTROPENLICENSETERMS`.
2. Reinicie o servidor.
3. Execute as etapas de configuração após a instalação, conforme descrito em [nesta seção](#bkmk_PostInstall). Será necessário reiniciar outro dos serviços do SQL Server.

## <a name="OldInstall"></a>Instalação autônoma dos serviços do R (no banco de dados)
 
 A exemplo a seguir mostra o **mínimo** instalam recursos necessários a serem especificados na linha de comando ao executar silencioso, autônomo do SQL Server 2016 R Services.

1. Abra um prompt de comando com privilégios elevados e execute o seguinte comando:

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
    ```
    Observe os sinalizadores necessários para serviços do R 2016: `ADVANCEDANALYTICS` e `IACCEPTROPENLICENSETERMS`.
2. Reinicie o servidor.
3. Execute as etapas de configuração após a instalação, conforme descrito em [nesta seção](#bkmk_PostInstall). Será necessário reiniciar outro dos serviços do SQL Server.

## <a name = "bkmk_PostInstall"></a>Etapas adicionais após a instalação

1.  Após a conclusão da instalação, abra uma nova **consulta** janela no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], e execute o seguinte comando para habilitar o recurso.
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  Você deve habilitar explicitamente o recurso e reconfigure; Caso contrário, não será possível chamar scripts externos, mesmo que o recurso tenha sido instalado.
  
2.  Reinicie o serviço do SQL Server para a instância reconfigurado. Isso reiniciará automaticamente relacionado [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] serviço também.

3. Etapas adicionais poderão ser necessárias se você tiver uma configuração de segurança personalizada ou for usar o SQL Server para dar suporte a contextos de computação remota. Para obter mais informações, consulte [Perguntas frequentes sobre atualização e instalação](../../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md).

