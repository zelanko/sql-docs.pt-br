---
title: "Exibir e ler arquivos de log da Instala&#231;&#227;o do SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "exibindo logs"
  - "exibindo arquivos de log"
  - "Configuração [SQL Server], logs"
  - "arquivos de log da instalação [SQL Server]"
  - "instalando o SQL Server, logs"
  - "erros [SQL Server], Configuração"
  - "logs [SQL Server], Configuração"
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
caps.latest.revision: 54
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 54
---
# Exibir e ler arquivos de log da Instala&#231;&#227;o do SQL Server
  Cada execução da Instalação cria arquivos de log com uma nova pasta de log com carimbo de data/hora em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\. O formato de nome da pasta com carimbo de data/hora é AAAAMMDD_hhmmss. Quando a Instalação é executada em um modo autônomo, os logs são criados em % temp%\sqlsetup*.log. Todos os arquivos da pasta de logs são arquivados no arquivo Log\*.cab em sua respectiva pasta de log.  
  
 Uma solicitação de Instalação típica passa por três fases de execução:  
  
1.  Texto de regras globais  
  
2.  Atualização de componente  
  
3.  Ação solicitada pelo usuário  
  
 Em cada fase, a Instalação gera logs de detalhes e de resumo com logs adicionais criados conforme apropriado. A Instalação é chamada ao menos três vezes para cada ação de instalação solicitada pelo usuário.  
  
 Os arquivos de armazenamento de dados contêm um instantâneo do estado de todos os objetos de configuração que estão sendo rastreados pelo processo de instalação e são úteis para solucionar erros de configuração. Despejos de arquivo XML são criados para objetos de armazenamento de dados em cada fase de execução. Eles são salvos em sua própria subpasta de log na pasta de log com carimbo de data/hora, como a seguir:  
  
-   Datastore_GlobalRules  
  
-   Datastore_ComponentUpdated  
  
-   Datastore  
  
 As seções a seguir descrevem arquivos de log da Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Texto resumido  
  
### Visão geral  
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
  
### Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\.  
  
 Para localizar erros no arquivo de texto resumido, pesquise o arquivo usando as palavras-chave "error" ou "failed".  
  
## Summary_engine-base_YYYYMMDD_HHMMss.txt  
  
### Visão geral  
 O arquivo de base summary_engine é semelhante ao arquivo de resumo e é gerado durante o fluxo de trabalho principal.  
  
### Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## Summary_engine-base_YYYYMMDD_HHMMss_ComponentUpdate.txt  
  
### Visão geral  
 O arquivo de log resumido de atualização do componente é semelhante ao arquivo de resumo e é gerado durante o fluxo de trabalho de atualização de componente.  
  
### Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## Summary_engine-base_\<VersionNumber>MMDD_HHMMss_GlobalRules.txt  
  
### Visão geral  
 O arquivo de log resumido de regras globais é semelhante ao arquivo de resumo gerado durante o fluxo de trabalho de regras globais.  
  
### Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## Detail.txt  
  
### Visão geral  
 O arquivo Detail.txt é gerado para o fluxo de trabalho principal, como instalação ou atualização, e fornece os detalhes da execução. Os logs do arquivo são gerados com base na hora em que cada ação para a instalação foi invocada, e mostram a ordem na qual as ações foram executadas e suas dependências.  
  
### Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup  
  
 Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt.  
  
 Se ocorrer um erro durante o processo de Instalação, a exceção ou o erro será registrado no final desse arquivo. Para localizar os erros nesse arquivo, primeiro examine o final do arquivo e depois efetue uma pesquisa do arquivo pelas palavras-chave "error" ou "exception".  
  
## Detail_ComponentUpdate.txt  
  
### Visão geral  
 O arquivo Detail_ComponentUpdate.txt é gerado para o fluxo de trabalho de atualização de componente e é semelhante ao Detail.txt.  
  
### Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## Detail_GlobalRules.txt  
  
### Visão geral  
 O arquivo Detail_GlobalRules.txt é gerado para a execução de regras globais e é semelhante ao Detail.txt.  
  
### Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## Arquivos de log MSI  
  
### Visão geral  
 Os arquivos de log MSI fornecem detalhes do processo de pacote de instalação. Eles são gerados pelo MSIEXEC durante a instalação do pacote especificado.  
  
 Tipos de arquivos de log MSI:  
  
-   \<Feature>_\<Architecture>\_\<Interation>.log  
  
-   \<Feature>_\<Architecture>\_\<Language>\_\<Interation>.log  
  
-   \<Feature>_\<Architecture>\_\<Interation>\_\<workflow>.log  
  
### Local  
 Os arquivos de log MSI estão localizados em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\<Name\>.log.  
  
 No final do arquivo, há um resumo da execução, que inclui o status de êxito ou falha e propriedades. Para localizar o erro no arquivo MSI, pesquise "value 3"; os erros geralmente são encontrados próximos à cadeia de caracteres.  
  
## ConfigurationFile.ini  
  
### Visão geral  
 O arquivo de configuração contém as configurações de entrada que são fornecidas durante instalação. Pode ser usado para reiniciar a instalação sem ser necessário inserir as configurações manualmente. Entretanto, as senhas das contas, o PID e alguns parâmetros não são salvos no arquivo de configuração. As configurações podem ser adicionadas ao arquivo ou fornecidas por meio da linha de comando ou da interface do usuário de Instalação. Para obter mais informações, veja [Instalar o SQL Server 2016 usando um arquivo de configuração](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md).  
  
### Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## SystemConfigurationCheck_Report.htm  
  
### Visão geral  
 O relatório de verificação da configuração do sistema contém uma breve descrição de cada regra executada, bem como o status de execução.  
  
### Local  
 Ele está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## Consulte também  
 [Instalar o SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016.md)  
  
  