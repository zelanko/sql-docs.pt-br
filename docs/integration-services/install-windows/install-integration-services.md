---
title: Instalar o Integration Services | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Integration Services, installing
- SSIS, installing
- installing Integration Services, about installing Integration Services
- SQL Server Integration Services, installing
- Setup [Integration Services], about installing Integration Services
- installing Integration Services
- Setup [Integration Services]
ms.assetid: bd20fd3a-414b-4581-959d-ebba4ddf5a55
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 8233e11171d5adc7656fd2b2ce75c86fca2c07fa
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="install-integration-services"></a>Instalar o Integration Services
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um único programa de Instalação para instalar qualquer ou todos os seus componentes, incluindo o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Com a Instalação, você pode instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com ou sem outros componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um único computador.    
    
 Este tópico destaca considerações importantes que você deve saber antes de instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. As informações neste tópico o ajudarão a avaliar as opções de instalação, para que seja possível fazer seleções que resultem em uma instalação com êxito.    
    
## <a name="preparing-to-install-integration-services"></a>Preparando para instalar o Integration Services    
 Antes de instalar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], revise os seguintes requisitos:    
    
-   [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)    
    
-   [Verificar parâmetros do Verificador de Configuração do Sistema](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)    
    
-   [Considerações sobre segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)    
    
## <a name="selecting-an-integration-services-configuration"></a>Selecionando uma configuração do Integration Services    
 Você pode instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nas seguintes configurações:    
    
-   Você pode instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um computador que não tenha nenhuma instância anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
    
-   Você pode instalar o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] lado a lado com uma instância existente do [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] e do [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)].    
    
     Quando você atualiza para o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] em um computador que tem uma dessas versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] já instalada, o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] é instalado lado a lado com a versão anterior.    
    
     Para obter mais informações sobre como atualizar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], veja [Atualizar o Integration Services](../../integration-services/install-windows/upgrade-integration-services.md). Para obter informações sobre a compatibilidade com versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], veja [Compatibilidade com versões anteriores do Integration Services](../../integration-services/integration-services-backward-compatibility.md).    
    
## <a name="installing-integration-services"></a>instalando o Integration Services    
 Depois de analisar os requisitos de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e garantir que seu computador atende esses requisitos, você estará pronto para instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].    
    
> [!NOTE]    
>  Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por padrão, quando você instalava o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , todos os usuários no grupo Usuários tinham acesso ao serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Quando você instala o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], os usuários não têm acesso ao serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Por padrão, o serviço é protegido. Depois que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for instalado, o administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá executar a ferramenta Configuração de DCOM (Dcomcnfg.exe) para conceder acesso ao **SQL Server Integration Services 13.0**a usuários específicos.    
>     
>  Para obter instruções sobre como conceder permissões, consulte [Serviço SSIS &#40;Serviço Integration Services&#41;](../../integration-services/service/integration-services-service-ssis-service.md).    
    
 Se estiver usando o Assistente de Instalação para instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você usará uma série de páginas para especificar componentes e opções. A tabela a seguir lista somente as páginas do Assistente de Instalação em que as opções selecionadas afetam a instalação do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:    
    
|Página|Recomendações|    
|----------|---------------------|    
|**Seleção de recursos**|Selecione **Integration Services** para instalar o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e executar pacotes fora do ambiente de design.<br /><br /> Para uma instalação completa do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], que tenha as ferramentas e a documentação para o desenvolvimento e o gerenciamento de pacotes, selecione **Integration Services** e **Recursos Compartilhados**:<br /><br /> -<br />                    **Ferramentas de Dados do SQL Server** para instalar as ferramentas para criar pacotes.<br /><br /> -<br />                    **Ferramentas de Gerenciamento – Completas** para instalar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para gerenciar pacotes.<br /><br /> -<br />                    **SDK de Ferramentas de Cliente** para instalar assemblies gerenciados para programação do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .<br /><br /> Muitas soluções de data warehousing também requerem a instalação de componentes adicionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> **Instalando em um computador de 64 bits** Em um computador de 64 bits, a seleção de **Integration Services** instala apenas o tempo de execução e as ferramentas de 64 bits. Se você precisar executar pacotes em modo de 32 bits, deverá selecionar também uma opção adicional para instalar o tempo de execução e as ferramentas de 32 bits:<br /><br /> - Se o computador de 64 bits estiver executando o sistema operacional x86, selecione **SQL Server Data Tools** ou **Management Tools – Completo**.<br /><br /> - Se o computador de 64 bits estiver executando o sistema operacional [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] , selecione **Management Tools – Completo**.<br /><br /> **Instalando em um Servidor Dedicado para ETL** Para usar um servidor dedicado para processos ETL (extração, transformação e carregamento) é recomendável instalar uma instância local do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ao instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] geralmente armazena pacotes em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e depende do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para agendar esses pacotes. Se o servidor ETL não tiver uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], será necessário agendar ou executar pacotes de um servidor que tenha uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Isso significa que os pacotes não serão executados no servidor ETL, mas no servidor do qual foram iniciados. Assim, os recursos do servidor ETL dedicado não estarão sendo usados como pretendido. Além disso, os recursos de outros servidores podem ser obtidos pela execução de processos ETL<br /><br /> <br /><br /> Observação: alguns componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que podem ser selecionados para instalação na página **Seleção de Recursos** do Assistente de Instalação instalam um subconjunto parcial dos componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Esses componentes são úteis para tarefas específicas, mas a funcionalidade do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] será limitada. Por exemplo, a opção **Serviços de Mecanismo de Banco de Dados** instala os componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] necessários para o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A opção **Ferramentas de Dados do SQL Server** instala os componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] necessários para criar um pacote, mas o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não é instalado e você não pode executar pacotes fora do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Para assegurar uma instalação completa do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você deve selecionar **Integration Services** na página **Seleção de Recursos** .|    
|**Configuração da instância**|Qualquer seleção que você faça na página **Configuração da Instância** não afeta o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .<br /><br /> Você pode instalar apenas uma instância do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um computador. Você se conecta ao serviço usando o nome do computador.<br /><br /> Por padrão, o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é configurado para gerenciar pacotes armazenados no banco de dados **msdb** em uma instância do Mecanismo de Banco de Banco de Dados instalada ao mesmo tempo em que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se uma instância do Mecanismo de Banco de Dados não for instalada ao mesmo tempo que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] será configurado para gerenciar pacotes armazenados no banco de dados **msdb** de uma instância local padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para gerenciar pacotes armazenados em uma instância nomeada ou remota do [!INCLUDE[ssDE](../../includes/ssde-md.md)]ou em várias instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)], é preciso modificar o arquivo de configuração. Para obter mais informações sobre como modificar esse arquivo de configuração, consulte [Serviço SSIS &#40;Serviço Integration Services&#41;](../../integration-services/service/integration-services-service-ssis-service.md).|    
|**Configuração do Servidor**|Examine as configurações para o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] na guia **Contas de Serviço** da página **Configuração do Servidor** .<br /><br /> Se o Windows 7 ou Windows Server 2008 R2 estiver instalado, o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] será registrado para ser executado na conta virtual NT Services\MsDtsServer130 e o **Tipo de inicialização** será **Automático**.  Você não tem que inserir uma senha para a conta virtual. Se o Microsoft Vista ou Windows Server 2008 estiver instalado, o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] será registrado para ser executado na conta interna Serviço de Rede e o **Tipo de inicialização** será **Automático**. Você não tem que digitar uma senha para a conta de Serviço de Rede interna.|    
    
 Por padrão, em uma nova instalação, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é configurado para não registrar eventos relacionados à execução de pacotes no log de eventos do Aplicativo. Essa configuração evita de entradas em excesso no log de eventos quando você usa o recurso Coletor de Dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Os eventos registrados são EventID 12288, "Pacote iniciado" e EventID 12289, "Pacote concluído com êxito". Para registrar esses eventos no log de eventos do Aplicativo, abra o Registro para edição. Em seguida, no Registro, localize o nó HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS e altere o valor DWORD da configuração LogPackageExecutionToEventLog de 0 para 1.    
    
## <a name="understanding-the-integration-services-service"></a>Compreendendo o serviço Integration Services    
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instala o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .    
    
 O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é instalado quando você selecionar a opção **Integration Services** na página **Seleção de Recursos** . Quando você aceita as configurações padrão na página **Configuração de Servidor** , o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é habilitado e seu **Tipo de Inicialização** é **Automática**.    
    
 Você pode instalar apenas uma única instância do serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um computador. O serviço não é específico a uma instância específica do Mecanismo de Banco de Dados. Você se conecta ao serviço usando o nome do computador no qual ele está sendo executado.    
    
## <a name="installing-integration-services-on-64-bit-computers"></a>Instalando o Integration Services em computadores de 64 bits    
    
### <a name="integration-services-features-installed-on-64-bit-computers"></a>Recursos do Integration Services instalados em computadores de 64 bits    
 A instalação instala vários recursos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com base nas opções de instalação selecionadas:    
    
-   Quando você instala o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e seleciona o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para instalação, são instalados todos os recursos e ferramentas de 64 bits disponíveis do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .    
    
-   Se você precisar de recursos de tempo de design do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , também deverá instalar o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].    
    
-   Se você precisar das versões de 32 bits das ferramentas e do tempo de execução do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para executar determinados pacotes no modo de 32 bits, deverá instalar também o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].    
    
 Os recursos de 64 bits são instalados no diretório **Arquivos de Programas** e os recursos de 32 bits são instalados separadamente no diretório **Arquivos de Programas (x86)** . (Esse comportamento não é específico do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].)    
    
> [!IMPORTANT]    
>  O [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], ambiente de desenvolvimento de 32 bits para pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], não tem suporte no sistema operacional de 64 bits do [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] e não é instalado em servidores [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)].    
    
  
