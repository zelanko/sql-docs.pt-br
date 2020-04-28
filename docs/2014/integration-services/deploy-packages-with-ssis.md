---
title: 'Tutorial do SSIS: implantando pacotes | Microsoft Docs'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e47c9640c314ad28ae64ef105d723b77695e644d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176446"
---
# <a name="ssis-tutorial-deploying-packages"></a>Tutorial do SSIS: Como implantar pacotes
  O [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece ferramentas que facilitam a implantação de pacotes em outro computador. As ferramentas de implantação também gerenciam qualquer dependência, como configurações e arquivos que o pacote precisa. Neste tutorial, você aprenderá a usar essas ferramentas para instalar pacotes e suas dependências em um computador de destino.

 Primeiro, você executará as tarefas para preparar a implantação. Você criará um novo projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e adicionará pacotes e arquivos de dados existentes ao projeto. Você não criará nenhum pacote a partir do zero; em vez disso, apenas trabalhará com pacotes concluídos criados apenas para este tutorial. Você não modificará a funcionalidade dos pacotes neste tutorial; porém, após adicionar os pacotes ao projeto, poderá achar útil abrir os pacotes no Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] e revisar o conteúdo de cada pacote. Ao examinar os pacotes, aprenderá sobre as dependências dos pacotes, como arquivos de log, e sobre outros recursos interessantes dos pacotes.

 Na preparação para a implantação, você também atualizará os pacotes para usar as configurações. As configurações tornam as propriedades dos pacotes e dos objetos de pacote atualizáveis em tempo de execução. Neste tutorial, você usará configurações para atualizar as cadeias de caracteres de conexão de arquivos log e de texto e os locais dos arquivos XML e XSD utilizados pelo pacote. Para obter mais informações, consulte [Configurações de pacote](../../2014/integration-services/package-configurations.md) e [Criar configurações de pacote](../../2014/integration-services/create-package-configurations.md).

 Depois de verificar se os pacotes estão sendo executados com êxito no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], você criará o grupo de desenvolvimento para usar na instalação dos pacotes. O grupo de desenvolvimento consistirá nos arquivos de pacote e outros itens adicionados ao projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , as dependências de pacote que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui automaticamente e o utilitário de implantação que você compilou. Para obter mais informações, consulte [Criar um utilitário de implantação](../../2014/integration-services/create-a-deployment-utility.md).

 Você copiará o pacote de implantação no computador de destino e executará o Assistente de Instalação de Pacotes para instalar os pacotes e as dependências de pacotes. Os pacotes serão instalados no banco de dados msdb do SQL Server e os arquivos auxiliares e de suporte serão instalados no sistema de arquivos. Como os pacotes implantados usam configurações, você atualizará a configuração para usar novos valores que habilitam os pacotes para serem executados com êxito no novo ambiente.

 Por fim, você executará os pacotes no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] usando o Utilitário do Pacote de Execução.

 O objetivo deste tutorial é simular a complexidade dos problemas reais de implantação que você poderá encontrar. Porém, se não for possível implantar os pacotes em um computador diferente, você ainda poderá executar este tutorial instalando os pacotes no banco de dados msdb em uma instância local do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]e depois executar os pacotes do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] na mesma instância.

## <a name="what-you-will-learn"></a>O que você aprenderá
 A melhor maneira de se familiarizar com as novas ferramentas, controles e recursos disponíveis no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é usá-las. Este tutorial guia você através das etapas para criar um projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e adicionar pacotes e outros arquivos necessários ao projeto. Após a conclusão do projeto, você criará um grupo de implantação, copiará o grupo para o computador de destino e instalará os pacotes no computador de destino.

## <a name="requirements"></a>Requisitos
 Este tutorial destina-se a usuários que já estão familiarizados com operações fundamentais do sistema de arquivos, mas que têm exposição limitada aos novos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]recursos disponíveis no. Para entender melhor os [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] conceitos básicos que você colocará para usar neste tutorial, talvez seja útil primeiro concluir os seguintes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] tutoriais: [Execute o assistente de SQL Server importação e exportação](import-export-data/start-the-sql-server-import-and-export-wizard.md) e o tutorial do [SSIS: Criando um pacote ETL simples](../integration-services/ssis-how-to-create-an-etl-package.md).

 **Computador de origem** O computador no qual você criará o pacote de implantação deve ter os seguintes componentes instalados:

-   O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com o banco de dados AdventureWorks. Para reforçar a segurança, os bancos de dados de exemplo não são instalados por padrão. Você pode baixar o banco de dados de exemplo do [codeplex](https://msftdbprodsamples.codeplex.com/releases/view/125550).

-   Você deve ter permissão para criar e cancelar tabelas no AdventureWorks.

-   Este tutorial também precisa de dados de amostra, pacotes concluídos, configurações e um Leiame. Os arquivos para esses itens estão instalados junto com as amostras. Se você não puder localizar os dados de amostra, retorne ao procedimento anterior e complete a instalação conforme descrito.

-   O ambiente de desenvolvimento de business intelligence, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].

 **Computador de destino.** O computador no qual você implanta os pacotes deve ter os seguintes componentes instalados:

-   O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com o banco de dados AdventureWorks.

-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].

-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].

-   Você deve ter permissão para criar e remover tabelas do AdventureWorks e executar pacotes no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].

-   Você deve ter permissão de leitura e gravação na tabela sysssispackages no banco de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dados do sistema msdb.

 Se você planeja implantar pacotes no mesmo computador em que criará o grupo de implantação, esse computador deverá atender aos requisitos dos computadores de origem e de destino.

 **Tempo estimado para concluir este tutorial:** 2 horas

## <a name="lessons-in-this-tutorial"></a>Lições neste tutorial
 [Lição 1: preparando-se para criar o pacote de implantação](../integration-services/lesson-1-preparing-to-create-the-deployment-bundle.md) Nesta lição, você se preparará para implantar uma solução de ETL criando um novo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] projeto e adicionando os pacotes e outros arquivos necessários ao projeto.

 [Lição 2: criando o pacote de implantação](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md) Nesta lição, você criará um utilitário de implantação e verificará se o pacote de implantação inclui os arquivos necessários.

 [Lição 3: Instalando pacotes](../integration-services/lesson-3-install-ssis-package.md) Nesta lição, você copiará o pacote de implantação para o computador de destino, instalará os pacotes e, em seguida, executará os pacotes.

![Ícone de Integration Services (pequeno)](media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.

