---
title: Instalar o SQL Server usando um arquivo de configuração | Microsoft Docs
ms.date: 09/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: a832153a-6775-4bed-83f0-55790766d885
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: c5127fd5aec582db4f8e574f29cab5cec3809252
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2019
ms.locfileid: "58072201"
---
# <a name="install-sql-server-using-a-configuration-file"></a>Instalar o SQL Server usando um arquivo de configuração

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A Instalação fornece a capacidade de gerar um arquivo de configuração baseado no padrão do sistema e em entradas de tempo de execução. É possível usar o arquivo de configuração para implantar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em toda a empresa com a mesma configuração. Também é possível padronizar instalações manuais em toda a empresa criando um arquivo em lotes que inicie o Setup.exe. 
 
Este artigo é mantido para versões do SQL Server 2016 e posterior. Para versões anteriores do SQL Server, consulte [Instalar o SQL Server 2014 usando um arquivo de configuração](/../../2014/database-engine/install-windows/install-sql-server-using-a-configuration-file.md).
 
A Instalação dá suporte ao uso do arquivo de configuração apenas através do prompt de comando. A ordem de processamento dos parâmetros ao usar o arquivo de configuração é descrita a seguir:  
  
-  O arquivo de configuração substitui os padrões em um pacote  
  
-   Os valores da linha de comando substituem os valores do arquivo de configuração  
  
 O arquivo de configuração pode ser usado para acompanhar os parâmetros e valores de cada instalação. Isto torna o arquivo de configuração útil para verificar e auditar as instalações. 
  
## <a name="configuration-file-structure"></a>Estrutura do arquivo de configuração  
 O ConfigurationFile.ini é um arquivo de texto com parâmetros (par de nome/valor) e comentários descritivos. 
  
 O seguinte exemplo é de um arquivo ConfigurationFile.ini:  
  
```  
; Microsoft SQL Server Configuration file  
[OPTIONS]  
; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE.  
; This is a required parameter.  
ACTION="Install"  
; Specifies features to install, uninstall, or upgrade.  
; The list of top-level features include SQL, AS, RS, IS, and Tools.  
; The SQL feature will install the database engine, replication, and full-text.  
; The Tools feature will install Management Tools, Books online,   
; SQL Server Data Tools, and other shared components.  
FEATURES=SQL,Tools  
```  
  
#### <a name="how-to-generate-a-configuration-file"></a>Como gerar um arquivo de configuração  
  
1. Insira a mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Na pasta raiz, clique duas vezes em Setup.exe. Para instalar a partir de um compartilhamento de rede, localize a pasta raiz no compartilhamento e clique duas vezes em Setup.exe. 
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express Edition não cria um arquivo de configuração automaticamente. O comando a seguir iniciará a instalação e criará um arquivo de configuração. 
    >   
    >  SETUP.exe /UIMODE=Normal /ACTION=INSTALL  
  
2. Conclua o assistente até a página **Pronto para Instalar** . O caminho para o arquivo de configuração é especificado na página **Pronto para Instalar** na seção do caminho do arquivo de configuração. Para obter mais informações sobre como instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Instalar o SQL Server por meio do Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md). 
  
3. Cancele a instalação sem realmente concluí-la para gerar o arquivo INI. 
  
    > [!NOTE]  
    >  A infraestrutura da instalação gravará todos os parâmetros adequados para as ações que foram executadas, com exceção de informações confidencias, como senhas. O parâmetro /IAcceptSQLServerLicenseTerms também não é gravado no arquivo de configuração e requer uma modificação do arquivo de configuração ou um valor a ser fornecido no prompt de comando. Para obter mais informações, consulte [Instalar o SQL Server por meio do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). Além disso, um valor é incluído para os parâmetros boolianos onde um valor geralmente não é fornecido por meio do prompt de comando. 
  
## <a name="using-the-configuration-file-to-install-includessnoversionincludesssnoversion-mdmd"></a>Usando o arquivo de configuração para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  

É possível usar o arquivo de configuração apenas em instalações de linha de comando. 
  
> [!NOTE]  
> Se você precisar fazer alterações no arquivo de configuração, é recomendável fazer uma cópia e trabalhar com a cópia. 
  
### <a name="how-to-use-a-configuration-file-to-install-a-stand-alone-includessnoversionincludesssnoversion-mdmd-instance"></a>Como usar um arquivo de configuração para instalar uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Execute a instalação por meio do prompt de comando e forneça o ConfigurationFile.ini usando o parâmetro *ConfigurationFile* . 
  
### <a name="how-to-use-a-configuration-file-to-prepare-and-complete-an-image-of-a-stand-alone-includessnoversionincludesssnoversion-mdmd-instance-sysprep"></a>Como usar um arquivo de configuração para preparar e concluir uma imagem de uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SysPrep)  
  
1. Para preparar uma ou mais instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e configurá-las na mesma máquina. 
  
    - Execute **Preparação de imagem de uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** na página **Avançado** da Central de Instalação e capture o arquivo de configuração da preparação de imagem. 
  
    - Use o mesmo arquivo de configuração de preparação de imagem como um modelo para preparar mais instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
    - Execute **Conclusão de imagem de uma instância autônoma preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** na página **Avançado** da Central de Instalação para configurar instâncias preparadas no computador. 
  
2. Para preparar uma imagem do sistema operacional incluindo uma instância preparada não configurada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usando a ferramenta SysPrep do Windows. 
  
    -   Execute a **Preparação de imagem de uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** na página Avançado da Central de Instalação e capture o arquivo de configuração da preparação de imagem. 
  
    -   Execute a **Conclusão de imagem de uma instância autônoma preparada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** na página **Avançado** da Central de Instalação, mas cancele-a na página **Pronto para Concluir** depois de capturar o arquivo de configuração completo. 
  
    -   O arquivo de configuração de imagem completo pode ser armazenado com a imagem do Windows para automatizar a configuração das instâncias preparadas. 
  
### <a name="how-to-install-a-includessnoversionincludesssnoversion-mdmd-failover-cluster-using-the-configuration-file"></a>Como instalar um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o arquivo de configuração  
  
1. Opção de Instalação Integrada (criar um único cluster de failover de nó em um nó e, para nós adicionais, executar AddNode neles):  
  
    -   Execute a opção "Instalar um Cluster de Failover" e capture o arquivo de configuração que lista todas as configurações de instalação. 
  
    -   Execute a instalação de cluster de failover de linha de comando fornecendo o parâmetro *ConfigurationFile* . 
  
    -   Em um nó adicional a ser adicionado, execute AddNode para capturar o arquivo ConfigurationFile.ini aplicável ao cluster de failover existente. 
  
    -   Execute o AddNode de linha de comando em todos os nós adicionais que serão unidos ao cluster de failover fornecendo o mesmo arquivo de configuração usando o parâmetro ConfigurationFile. 
  
2. Opção de Instalação avançada (preparar cluster de failover em todos os nós de cluster de failover e, após preparar todos os nós, execução completa no nó que possui o disco compartilhado):  
  
    -   Execute **Preparar** em um dos nós e capture o arquivo ConfigurationFile.ini. 
  
    -   Forneça o mesmo arquivo ConfigurationFile.ini para Instalação em todos os nós que serão preparados para o cluster de failover. 
  
    -   Após a preparação de todos os nós, execute uma operação de cluster de failover completa no nó que possui o disco compartilhado e capture o arquivo ConfigurationFile.ini. 
  
    -   Em seguida, você pode fornecer esse arquivo ConfigurationFile.ini para concluir o cluster de failover. 
  
### <a name="how-to-add-or-remove-a-node-to-a-includessnoversionincludesssnoversion-mdmd-failover-cluster-using-the-configuration-file"></a>Como adicionar ou remover um nó de um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o arquivo de configuração  
  
-   Se você tiver um arquivo de configuração que foi usado anteriormente para adicionar um nó ou para remover um nó de um cluster de failover, poderá reutilizar esse mesmo arquivo para adicionar ou remover nós adicionais. 
  
### <a name="how-to-upgrade-a-includessnoversionincludesssnoversion-mdmd-failover-cluster-using-the-configuration-file"></a>Como atualizar um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o arquivo de configuração  
  
1. Execute Atualizar no nó passivo e capture o arquivo ConfigurationFile.ini. Isso pode ser feito executando a atualização real ou saindo no final sem fazer a atualização real. 
  
2. Em todos os nós adicionais a serem atualizados, forneça o arquivo ConfigurationFile.ini para concluir o processo. 
  
## <a name="sample-syntax"></a>Sintaxe de exemplo  
 Os exemplos a seguir mostram como usar o arquivo de configuração:  
  
-   Para especificar o arquivo de configuração no prompt de comando:  
  
```  
Setup.exe /ConfigurationFile=MyConfigurationFile.INI  
```  
  
-   Para especificar senhas no prompt de comando em vez de no arquivo de configuração:  
  
```  
Setup.exe /SQLSVCPASSWORD="************" /AGTSVCPASSWORD="************" /ASSVCPASSWORD="************" /ISSVCPASSWORD="************" /RSSVCPASSWORD="************" /ConfigurationFile=MyConfigurationFile.INI  
```  
  
## <a name="see-also"></a>Confira também  
 [Instalar o SQL Server do prompt de comando](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Instalação do cluster de failover do SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)   
 [Atualizar uma instância de cluster de failover do SQL Server](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)  
  
  
