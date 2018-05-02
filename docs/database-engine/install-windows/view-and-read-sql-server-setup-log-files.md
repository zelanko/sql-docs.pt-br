---
title: Exibir e ler arquivos de log da Instalação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: install-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- viewing logs
- displaying log files
- Setup [SQL Server], logs
- installation log files [SQL Server]
- installing SQL Server, logs
- errors [SQL Server], Setup
- logs [SQL Server], Setup
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
caps.latest.revision: 54
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: de8c06e452f096799deab83d1cbe22353de75cba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="view-and-read-sql-server-setup-log-files"></a>Exibir e ler arquivos de log da Instalação do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Cada execução da Instalação cria arquivos de log com uma nova pasta de log com carimbo de data/hora em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\. O formato de nome da pasta com carimbo de data/hora é AAAAMMDD_hhmmss. Quando a Instalação é executada em um modo autônomo, os logs são criados em % temp%\sqlsetup*.log. Todos os arquivos da pasta de logs são arquivados no arquivo Log\*.cab em sua respectiva pasta de log.  
  
 Uma solicitação de Instalação típica passa por três fases de execução:  
  
1.  Texto de regras globais  
  
2.  Atualização de componente  
  
3.  Ação solicitada pelo usuário  
  
 Em cada fase, a Instalação gera logs de detalhes e de resumo com logs adicionais criados conforme apropriado. A Instalação é chamada ao menos três vezes para cada ação de instalação solicitada pelo usuário.  
  
 Os arquivos de armazenamento de dados contêm um instantâneo do estado de todos os objetos de configuração que estão sendo rastreados pelo processo de instalação e são úteis para solucionar erros de configuração. Despejos de arquivo XML são criados para objetos de armazenamento de dados em cada fase de execução. Eles são salvos em sua própria subpasta de log na pasta de log com carimbo de data/hora, como a seguir:  
  
-   Datastore_GlobalRules  
  
-   Datastore_ComponentUpdated  
  
-   Datastore  
  
 As seções a seguir descrevem arquivos de log da Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="summary-text"></a>Texto resumido  
  
### <a name="overview"></a>Visão geral  
 Esse arquivo mostra os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detectados durante Instalação, o ambiente de sistema operacional, valores de parâmetros de linha de comando, caso sejam especificados, e o status global de cada MSI/MSP que foi executado.  
  
 O log é organizado nas seguintes seções:  
  
-   Um resumo global da execução  
  
-   As propriedades e a configuração do computador em que a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi executada  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Recursos do produto instalados anteriormente no computador  
  
-   Descrição da versão de instalação e propriedades do pacote de instalação  
  
-   Configurações de entrada em tempo de execução que são fornecidas durante instalação  
  
-   Local do arquivo de configuração  
  
-   Detalhes dos resultados de execução  
  
-   Regras globais  
  
-   Regras específicas ao cenário de instalação  
  
-   Regras com falha  
  
-   Local do arquivo de relatório de regras  
  
### <a name="location"></a>Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\.  
  
 Para localizar erros no arquivo de texto resumido, pesquise o arquivo usando as palavras-chave "error" ou "failed".  
  
## <a name="summaryengine-baseyyyymmddhhmmsstxt"></a>Summary_engine-base_YYYYMMDD_HHMMss.txt  
  
### <a name="overview"></a>Visão geral  
 O arquivo de base summary_engine é semelhante ao arquivo de resumo e é gerado durante o fluxo de trabalho principal.  
  
### <a name="location"></a>Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## <a name="summaryengine-baseyyyymmddhhmmsscomponentupdatetxt"></a>Summary_engine-base_YYYYMMDD_HHMMss_ComponentUpdate.txt  
  
### <a name="overview"></a>Visão geral  
 O arquivo de log resumido de atualização do componente é semelhante ao arquivo de resumo e é gerado durante o fluxo de trabalho de atualização de componente.  
  
### <a name="location"></a>Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## <a name="summaryengine-baseversionnumbermmddhhmmssglobalrulestxt"></a>Summary_engine-base_\<VersionNumber>MMDD_HHMMss_GlobalRules.txt  
  
### <a name="overview"></a>Visão geral  
 O arquivo de log resumido de regras globais é semelhante ao arquivo de resumo gerado durante o fluxo de trabalho de regras globais.  
  
### <a name="location"></a>Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## <a name="detailtxt"></a>Detail.txt  
  
### <a name="overview"></a>Visão geral  
 O arquivo Detail.txt é gerado para o fluxo de trabalho principal, como instalação ou atualização, e fornece os detalhes da execução. Os logs do arquivo são gerados com base na hora em que cada ação para a instalação foi invocada, e mostram a ordem na qual as ações foram executadas e suas dependências.  
  
### <a name="location"></a>Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup  
  
 Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt.  
  
 Se ocorrer um erro durante o processo de Instalação, a exceção ou o erro será registrado no final desse arquivo. Para localizar os erros nesse arquivo, primeiro examine o final do arquivo e depois efetue uma pesquisa do arquivo pelas palavras-chave "error" ou "exception".  
  
## <a name="detailcomponentupdatetxt"></a>Detail_ComponentUpdate.txt  
  
### <a name="overview"></a>Visão geral  
 O arquivo Detail_ComponentUpdate.txt é gerado para o fluxo de trabalho de atualização de componente e é semelhante ao Detail.txt.  
  
### <a name="location"></a>Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## <a name="detailglobalrulestxt"></a>Detail_GlobalRules.txt  
  
### <a name="overview"></a>Visão geral  
 O arquivo Detail_GlobalRules.txt é gerado para a execução de regras globais e é semelhante ao Detail.txt.  
  
### <a name="location"></a>Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## <a name="msi-log-files"></a>Arquivos de log MSI  
  
### <a name="overview"></a>Visão geral  
 Os arquivos de log MSI fornecem detalhes do processo de pacote de instalação. Eles são gerados pelo MSIEXEC durante a instalação do pacote especificado.  
  
 Tipos de arquivos de log MSI:  
  
-   \<Recurso>_\<Arquitetura>\_\<Interação>.log  
  
-   \<Recurso>_\<Arquitetura>\_\<Idioma>\_\<Interação>.log  
  
-   \<Recurso>_\<Arquitetura>\_\<Interação>\_\<Fluxo de trabalho>.log  
  
### <a name="location"></a>Local  
 Os arquivos de log MSI estão localizados em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\<Name\>.log.  
  
 No final do arquivo, há um resumo da execução, que inclui o status de êxito ou falha e propriedades. Para localizar o erro no arquivo MSI, pesquise "value 3"; os erros geralmente são encontrados próximos à cadeia de caracteres.  
  
## <a name="configurationfileini"></a>ConfigurationFile.ini  
  
### <a name="overview"></a>Visão geral  
 O arquivo de configuração contém as configurações de entrada que são fornecidas durante instalação. Pode ser usado para reiniciar a instalação sem ser necessário inserir as configurações manualmente. Entretanto, as senhas das contas, o PID e alguns parâmetros não são salvos no arquivo de configuração. As configurações podem ser adicionadas ao arquivo ou fornecidas por meio da linha de comando ou da interface do usuário de Instalação. Para obter mais informações, veja [Instalar o SQL Server 2016 usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
### <a name="location"></a>Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## <a name="systemconfigurationcheckreporthtm"></a>SystemConfigurationCheck_Report.htm  
  
### <a name="overview"></a>Visão geral  
 O relatório de verificação da configuração do sistema contém uma breve descrição de cada regra executada, bem como o status de execução.  
  
### <a name="location"></a>Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## <a name="see-also"></a>Confira também  
 [Instalar o SQL Server 2016](../../database-engine/install-windows/install-sql-server.md)  
  
  
