---
title: Instalar o SSIS (SQL Server Integration Services) | Microsoft Docs
description: Saiba como instalar o Microsoft SQL Server Integration Services (SSIS) e como obter outros downloads para SSIS
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, installing
- SSIS, installing
- installing Integration Services, about installing Integration Services
- SQL Server Integration Services, installing
- Setup [Integration Services], about installing Integration Services
- installing Integration Services
- Setup [Integration Services]
ms.assetid: bd20fd3a-414b-4581-959d-ebba4ddf5a55
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0c0439c5230d39ae9dc856c9e1c5c5553e250c42
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65723667"
---
# <a name="install-integration-services"></a>Instalar o Integration Services

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um único programa de Instalação para instalar qualquer ou todos os seus componentes, incluindo o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Use a Instalação para instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com ou sem outros componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um único computador.    
    
 Este artigo destaca considerações importantes que você deve saber antes de instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. As informações neste artigo lhe ajudam a avaliar as opções de instalação, para que seja possível fazer seleções que resultem em uma instalação bem-sucedida.    
    
## <a name="get-ready-to-install-integration-services"></a>Preparar-se para instalar o Integration Services    
 Antes de instalar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], examine as seguintes informações:    
    
-   [Requisitos de Hardware e Software para a Instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)    
    
-   [Considerações sobre segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)    
    
## <a name="install-standalone-or-side-by-side"></a>Instalação autônoma ou lado a lado    
Você pode instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nas seguintes configurações:    
    
-   Você pode instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um computador que não tenha nenhuma instância anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
    
-   Você pode instalar o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] lado a lado com uma instância existente do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].    
    
Quando você atualiza para a versão mais recente do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um computador que tem uma versão anterior do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] já instalada, a versão atual é instalada lado a lado com a versão anterior.    
    
Para obter mais informações sobre como atualizar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], veja [Atualizar o Integration Services](../../integration-services/install-windows/upgrade-integration-services.md).

## <a name="get-sql-server-with-integration-services"></a>Obter o SQL Server com o Integration Services

Se você ainda não tiver o Microsoft SQL Server, baixe uma Edição de Avaliação gratuita ou a Edição de Desenvolvedor gratuita de [Downloads do SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads). O SSIS não está incluído na edição Express do SQL Server.

## <a name="install-integration-services"></a>Instalar o Integration Services    
 Depois de analisar os requisitos de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e garantir que seu computador atende esses requisitos, você estará pronto para instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].    
     
Se você está usando o Assistente de Instalação para instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você usa uma série de páginas para especificar componentes e opções.

-   Na página **Seleção de Recursos**, em **Recursos Compartilhados**, selecione **Integration Services**.

-   Em **Recursos de Instância**, selecione opcionalmente **Serviços de Mecanismo de Banco de Dados** para hospedar o banco de dados do Catálogo do SSIS, `SSISDB`, para armazenar, gerenciar, executar e monitorar pacotes do SSIS.

-   Para instalar assemblies gerenciados para programação de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], também em **Recursos Compartilhados**, selecione **SDK de Ferramentas de Cliente**.

> [!NOTE]
> Alguns componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que podem ser selecionados para instalação na página **Seleção de Recursos** do Assistente de Instalação instalam um subconjunto parcial dos componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Esses componentes são úteis para tarefas específicas, mas a funcionalidade do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é limitada. Por exemplo, a opção **Serviços de Mecanismo de Banco de Dados** instala os componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] necessários para o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para assegurar uma instalação completa do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você deve selecionar **Integration Services** na página **Seleção de Recursos** .

### <a name="installing-a-dedicated-server-for-etl-processes"></a>Como instalar um servidor dedicado para processos ETL

Para usar um servidor dedicado para processos ETL (extração, transformação e carregamento), instale uma instância local do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] quando você instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] geralmente armazena pacotes em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e depende do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para agendar esses pacotes. Se o servidor ETL não tiver uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], será necessário agendar ou executar pacotes de um servidor que tenha uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Como resultado, os pacotes não estão em execução no servidor ETL, mas sim no servidor do qual são iniciados. Assim, os recursos do servidor ETL dedicado não estarão sendo usados como pretendido. Além disso, os recursos de outros servidores podem ser obtidos pela execução de processos ETL

### <a name="configuring-ssis-event-logging"></a>Como configurar o log de eventos do SSIS
    
Por padrão, em uma nova instalação, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é configurado para não registrar eventos relacionados à execução de pacotes no log de eventos do Aplicativo. Essa configuração evita de entradas em excesso no log de eventos quando você usa o recurso Coletor de Dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Os eventos registrados são EventID 12288, "Pacote iniciado" e EventID 12289, "Pacote concluído com êxito". Para registrar esses eventos no log de eventos do Aplicativo, abra o Registro para edição. Em seguida, no Registro, localize o nó HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS e altere o valor DWORD da configuração LogPackageExecutionToEventLog de 0 para 1.    
    
## <a name="install-additional-components-for-integration-services"></a>Instalar componentes adicionais para o Integration Services

Para uma instalação completa do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], selecione os componentes necessários da lista a seguir:

-   **Integration Services (SSIS)**. Instale o SSIS com o Assistente de instalação do SQL Server. Selecionar o SSIS instala os seguintes itens:

    -   Suporte para o Catálogo do SSIS no Mecanismo de Banco de Dados do Microsoft SQL Server.

    -   Opcionalmente, o recurso SSIS Scale Out, que consiste de um mestre e de trabalhos.

    -   Componentes SSIS de 32 bits e de 64 bits.

    -   Instalar o SSIS **não** instala as ferramentas necessárias para projetar e desenvolver pacotes do SSIS.

-   **Mecanismo de banco de dados do SQL Server**. Instale o Mecanismo de Banco de Dados com o Assistente de Instalação do SQL Server. Selecionar o Mecanismo de Banco de Dados permite criar e hospedar o banco de dados do Catálogo do SSIS, `SSISDB`, para armazenar, gerenciar, executar e monitorar pacotes do SSIS.

-   **SQL Server Data Tools (SSDT)**. Para baixar e instalar o SSDT, veja [Baixar o SSDT (SQL Server Data Tools)](../../ssdt/download-sql-server-data-tools-ssdt.md). Instalar o SSDT permite criar e implantar pacotes do SSIS. O SSDT instala os seguintes itens:

    -   As ferramentas de design e desenvolvimento do pacote do SSIS, incluindo o Designer SSIS.

    -   Somente componentes SSIS de 32 bits.

    -   Uma versão limitada do Visual Studio (se não houver uma edição do Visual Studio já instalada).

    -   VSTA (Visual Studio Tools for Applications), o editor de scripts usado pela Tarefa Script e o Componente Script do SSIS.

    -   Assistentes do SSIS, incluindo o Assistente de Implantação e o Assistente de Atualização de Pacote.

    -   Assistente de Importação e Exportação do SQL Server.

-   **Feature Pack do Integration Services para Azure**. Para baixar e instalar o Feature Pack, veja [Feature Pack do Microsoft SQL Server 2017 Integration Services para Azure](https://www.microsoft.com/download/details.aspx?id=54798). Instalar o Feature Pack permite que seus pacotes se conectem aos serviços de armazenamento e análise na nuvem do Azure, incluindo os seguintes serviços:

    -   Armazenamento de Blobs do Azure.

    -   Azure HDInsight.

    -   Azure Data Lake Store.

    -   SQL Data Warehouse do Azure.

-   **Componentes adicionais opcionais**. Opcionalmente, você pode baixar os componentes de terceiros adicionais do SQL Server Feature Package.

    -   Microsoft® Connector para SAP BW para Microsoft SQL Server®. Para obter esses componentes, veja o [Feature Pack do Microsoft® SQL ServerÂ® 2017](https://www.microsoft.com/download/details.aspx?id=55992).

    -   Microsoft Connector versão 5.0 para Oracle da Attunity e Microsoft Connector versão 5.0 para Teradata da Attunity. Para obter esses componentes, veja [Microsoft Connectors v5.0 para Oracle e Teradata](https://www.microsoft.com/download/details.aspx?id=55179).
