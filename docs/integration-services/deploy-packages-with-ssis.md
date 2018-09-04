---
title: Implantar pacotes com o SSIS | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: quickstart
helpviewer_keywords:
- deployment tutorial [Integration Services]
- deploying packages [Integration Services]
- SSIS, tutorials
- Integration Services, tutorials
- deploying packages [Integration Services], installing
- SQL Server Integration Services, tutorials
- walkthroughs [Integration Services]
- deployment utility [Integration Services]
- deploying packages [Integration Services], configurations
ms.assetid: de18468c-cff3-48f4-99ec-6863610e5886
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f7f28ae86cab01c86aa7360618b080ec4ff124e2
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43028810"
---
# <a name="deploy-packages-with-ssis"></a>Implantar pacotes com o SSIS
[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece ferramentas que facilitam a implantação de pacotes em outro computador. As ferramentas de implantação também gerenciam qualquer dependência, como configurações e arquivos que o pacote precisa. Neste tutorial, você aprenderá a usar essas ferramentas para instalar pacotes e suas dependências em um computador de destino.    
    
Primeiro, você executará as tarefas para preparar a implantação. Você criará um novo projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e adicionará pacotes e arquivos de dados existentes ao projeto. Você não criará nenhum pacote a partir do zero; em vez disso, apenas trabalhará com pacotes concluídos criados apenas para este tutorial. Você não modificará a funcionalidade dos pacotes neste tutorial; porém, após adicionar os pacotes ao projeto, poderá achar útil abrir os pacotes no Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] e revisar o conteúdo de cada pacote. Ao examinar os pacotes, aprenderá sobre as dependências dos pacotes, como arquivos de log, e sobre outros recursos interessantes dos pacotes.    
    
Na preparação para a implantação, você também atualizará os pacotes para usar as configurações. As configurações tornam as propriedades dos pacotes e dos objetos de pacote atualizáveis em tempo de execução. Neste tutorial, você usará configurações para atualizar as cadeias de caracteres de conexão de arquivos log e de texto e os locais dos arquivos XML e XSD utilizados pelo pacote. Para obter mais informações, consulte [Configurações de pacote](../integration-services/packages/package-configurations.md) e [Criar configurações de pacote](../integration-services/packages/create-package-configurations.md).    
    
Depois de verificar se os pacotes estão sendo executados com êxito no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], você criará o grupo de desenvolvimento para usar na instalação dos pacotes. O grupo de desenvolvimento consistirá nos arquivos de pacote e outros itens adicionados ao projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , as dependências de pacote que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui automaticamente e o utilitário de implantação que você compilou. Para obter mais informações, consulte [Criar um utilitário de implantação](../integration-services/packages/create-a-deployment-utility.md).    
    
Você copiará o pacote de implantação no computador de destino e executará o Assistente de Instalação de Pacotes para instalar os pacotes e as dependências de pacotes. Os pacotes serão instalados no banco de dados msdb do SQL Server e os arquivos auxiliares e de suporte serão instalados no sistema de arquivos. Como os pacotes implantados usam configurações, você atualizará a configuração para usar novos valores que habilitam os pacotes para serem executados com êxito no novo ambiente.    
    
Por fim, você executará os pacotes no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] usando o Utilitário do Pacote de Execução.    
    
O objetivo deste tutorial é simular a complexidade dos problemas reais de implantação que você poderá encontrar. Porém, se não for possível implantar os pacotes em um computador diferente, você ainda poderá executar este tutorial instalando os pacotes no banco de dados msdb em uma instância local do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]e depois executar os pacotes do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] na mesma instância.    

**Tempo estimado para concluir este tutorial:** 2 horas

## <a name="what-you-learn"></a>O que você aprenderá    
O melhor modo de se familiarizar com as novas ferramentas, controles e recursos disponíveis no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é utilizando-os. Este tutorial guia você através das etapas para criar um projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e adicionar pacotes e outros arquivos necessários ao projeto. Após a conclusão do projeto, você criará um grupo de implantação, copiará o grupo para o computador de destino e instalará os pacotes no computador de destino.    
    
## <a name="prerequisites"></a>Prerequisites    
Este tutorial destina-se a usuários que já estão familiarizados com as operações básicas do sistema de arquivos, mas que tiveram pouca exposição aos novos recursos disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Para entender melhor os conceitos básicos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que serão usados neste tutorial, talvez seja útil concluir primeiro este tutorial do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] : [SSIS: Como criar um pacote ETL](../integration-services/ssis-how-to-create-an-etl-package.md).    
    
### <a name="on-the-source-computer"></a>No computador de origem

O computador no qual você criará o pacote de implantação **deverá ter os seguintes componentes instalados:**

- SQL Server. (Baixe uma edição do desenvolvedor ou de avaliação gratuita do SQL Server de [Downloads do SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads).)

- Dados de exemplo, pacotes concluídos, configurações e um Leiame. Para baixar os dados de exemplo e os pacotes de lição como um arquivo zip, veja os [Arquivos de Tutorial do SQL Server Integration Services](https://www.microsoft.com/download/details.aspx?id=56827). A maioria dos arquivos no arquivo Zip é somente leitura a fim de impedir alterações acidentais. Para gravar algo em um arquivo ou alterá-lo, talvez você precise desligar o atributo somente leitura nas propriedades do arquivo.

-   O banco de dados de exemplo **AdventureWorks2014**. Para baixar o banco de dados **AdventureWorks2014**, baixe `AdventureWorks2014.bak` em [Bancos de dados de exemplo do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) e restaure o backup.  

-   Você deve ter permissão para criar tabelas no banco de dados do AdventureWorks e para removê-las dele.
    
-   [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md).    
    
### <a name="on-the-destination-computer"></a>No computador de destino

O computador no qual você implanta os pacotes **deve ter os seguintes componentes instalados:**    
    
- SQL Server. (Baixe uma edição do desenvolvedor ou de avaliação gratuita do SQL Server de [Downloads do SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads).)

- Dados de exemplo, pacotes concluídos, configurações e um Leiame. Para baixar os dados de exemplo e os pacotes de lição como um arquivo zip, veja os [Arquivos de Tutorial do SQL Server Integration Services](https://www.microsoft.com/download/details.aspx?id=56827). A maioria dos arquivos no arquivo Zip é somente leitura a fim de impedir alterações acidentais. Para gravar algo em um arquivo ou alterá-lo, talvez você precise desligar o atributo somente leitura nas propriedades do arquivo.

-   O banco de dados de exemplo **AdventureWorks2014**. Para baixar o banco de dados **AdventureWorks2014**, baixe `AdventureWorks2014.bak` em [Bancos de dados de exemplo do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) e restaure o backup.  
    
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md).    
    
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Para instalar o SSIS, veja [Instalar o Integration Services](install-windows/install-integration-services.md).
    
-   Você deve ter permissão para criar tabelas no banco de dados do AdventureWorks e para removê-las dele, bem como para executar pacotes do SSIS no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].    
    
-   Você deve ter permissão de leitura e gravação na tabela `sysssispackages` no banco de dados do sistema `msdb` do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].    
    
Se você planeja implantar pacotes no mesmo computador em que criará o grupo de implantação, esse computador deverá atender aos requisitos dos computadores de origem e de destino.    
        
## <a name="lessons-in-this-tutorial"></a>Lições neste tutorial    
[Lição 1: Preparando-se para criar o pacote de implantação](../integration-services/lesson-1-preparing-to-create-the-deployment-bundle.md)    
Nesta lição, você irá se preparar para implantar uma solução ETL criando um novo projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e adicionando os pacotes e outros arquivos necessários ao projeto.    
    
[Lição 2: Criar o pacote de implantação no SSIS](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)    
Nesta lição, você compilará um utilitário de implantação e verificará se o grupo de implantação inclui os arquivos necessários.    
    
[Lição 3: Instalar os pacotes SSIS](../integration-services/lesson-3-install-ssis-packages.md)    
Nesta lição, você copiará o grupo de implantação para o computador de destino, instalará os pacotes e executará os pacotes.    
    

