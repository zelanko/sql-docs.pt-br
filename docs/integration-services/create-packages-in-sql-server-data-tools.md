---
title: Criar pacotes no SQL Server Data Tools | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: bb3c085b-1458-49fa-8348-6a76b6e97ea6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 199029eee15d44e3aba5b65c894de58b1ca2129c
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51639703"
---
# <a name="create-packages-in-sql-server-data-tools"></a>Copiar pacotes nas Ferramentas de Dados do SQL Server
  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], você pode criar um novo pacote usando um dos métodos a seguir:  
  
-   Use o modelo de pacote incluído no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
-   Usar um modelo personalizado  
  
     Para usar pacotes personalizados como modelos na criação de novos pacotes, você simplesmente os copia para a pasta DataTransformationItems. Por padrão, esta pasta está em C:\Arquivos de Programas\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject.  
  
-   Copie um pacote existente.  
  
     Se pacotes existentes incluírem a funcionalidade que deseja reutilizar, você pode criar o fluxo de controle e fluxos de dados no novo pacote mais rapidamente copiando e colando os objetos de outros pacotes. Para obter mais informações sobre como usar o copiar e colar em projetos [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , consulte [Reutilizar objetos de pacote](../integration-services/reuse-of-package-objects.md).  
  
     Se você criar um novo pacote copiando e colando um pacote existente, ou usando um pacote personalizado como modelo, o nome e GUID do pacote existente também serão copiados. Você deve atualizar o nome e GUID do novo pacote, para ajudar a diferenciá-lo do pacote originalmente copiado. Por exemplo, caso pacotes tenham o mesmo GUID, é mais difícil identificar o pacote ao quais os dados de log pertencem. Você pode gerar o GUID na propriedade **ID** e atualizar o valor da propriedade **Name** usando a janela Propriedades no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para obter mais informações, consulte [Definir as propriedades do pacote](../integration-services/set-package-properties.md) e [Utilitário dtutil](../integration-services/dtutil-utility.md).  
  
-   Use um pacote personalizado que você designou como um modelo.  
  
-   Executar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
     O Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cria um pacote completo para uma importação ou exportação simples. Este assistente configura as conexões, a origem e o destino e adiciona as transformações de dados necessárias para permitir a execução imediata da importação ou exportação. Se preferir, você pode salvar o pacote para executá-lo novamente depois ou refinar e aprimorar o pacote no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Porém, se o pacote for salvo, você deverá adicioná-lo a um projeto existente do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] antes de alterar o pacote ou executá-lo no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
 Os pacotes criados no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] por meio do [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer são salvos no sistema de arquivos. Para salvar um pacote no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou no repositório de pacotes, salve uma cópia do pacote. Para obter mais informações, consulte [Salvar uma cópia de um pacote](https://msdn.microsoft.com/library/21482a20-e420-4452-b7eb-8f9fa1929f31).  

 Para obter um vídeo que demonstre como criar um pacote básico usando o modelo de pacote padrão, consulte [Criando um pacote básico (vídeo do SQL Server)](https://go.microsoft.com/fwlink/?LinkId=131023).  

## <a name="get-sql-server-data-tools"></a>Obter o SQL Server Data Tools
Para instalar o SSDT (SQL Server Data Tools), consulte [Baixar o SSDT (SQL Server Data Tools)](../ssdt/download-sql-server-data-tools-ssdt.md).

## <a name="create-a-package-in-sql-server-data-tools-using-the-package-template"></a>Criar um pacote no SQL Server Data Tools usando o modelo de pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no qual você deseja criar um pacote.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse na pasta **Pacotes SSIS** e clique em **Novo Pacote SSIS**.  
  
3.  Se desejar, adicione o fluxo de controle, as tarefas do fluxo de dados e os manipuladores de eventos ao pacote. Para obter mais informações, consulte [Fluxo de Controle](../integration-services/control-flow/control-flow.md), [Fluxo de Dados](../integration-services/data-flow/data-flow.md) e [Manipuladores de Eventos do Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-event-handlers.md).  
  
4.  No menu **Arquivo** , clique em **Salvar Itens Selecionados** para salvar o novo pacote.  
  
    > [!NOTE]  
    >  Você pode salvar um pacote vazio.  
  
## <a name="choose-the-target-version-of-a-project-and-its-packages"></a>Escolher a versão de destino de um projeto e seus pacotes  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse em um projeto do Integration Services e selecione **Propriedades** para abrir as páginas de propriedades do projeto.  
  
2.  Na guia **Geral** de **Propriedades de Configuração**, selecione a propriedade **TargetServerVersion** e, em seguida, escolha o SQL Server 2012, SQL Server 2014 ou SQL Server 2016.  
  
     ![Propriedade TargetServerVersion na caixa de diálogo de propriedades do projeto](../integration-services/media/targetserverversion2.png "Propriedade TargetServerVersion na caixa de diálogo de propriedades do projeto")  
  
 Você pode criar, manter e executar pacotes que se destinam ao SQL Server 2016, SQL Server 2014 ou SQL Server 2012.  
  
  
