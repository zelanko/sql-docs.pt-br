---
title: "Executar um pacote nas Ferramentas de Dados do SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pacotes do Integration Services, executando"
  - "pacotes do SSIS, executando"
  - "pacotes [Integration Services], executando"
  - "pacotes do SQL Server Integration Services, executando"
ms.assetid: 318e6beb-5540-4101-82a5-18c9d47f0570
caps.latest.revision: 58
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# Executar um pacote nas Ferramentas de Dados do SQL Server
  Normalmente, os pacotes são executados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante o desenvolvimento, a depuração e o teste dos pacotes. Quando você executa um pacote no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)], o pacote é sempre executado imediatamente.  
  
 Enquanto um pacote estiver sendo executado, o Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] exibe o andamento da execução do pacote na guia **Progresso**. Você pode exibir a hora de início e do fim do pacote e suas tarefas e contêineres, além de informações sobre quaisquer tarefas ou contêineres no pacote em que houve falha. Depois que o pacote concluir a execução, as informações em tempo de execução continuarão disponíveis na guia **Resultados da Execução**. Para obter mais informações, consulte a seção "Relatório de progresso", no tópico [Depuração do fluxo de controle](../../integration-services/troubleshooting/debugging-control-flow.md).  
  
 **Implantação de tempo de design**. Quando um pacote é executado no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], ele é criado e, em seguida, implantado em uma pasta. Antes de executar o pacote, você pode especificar a pasta na qual ele será implantado. Por padrão, se você não especificar uma pasta, a pasta **bin** será usada. Este tipo de implantação é chamado de implantação de tempo de design.  
  
### Para executar um pacote nas Ferramentas de Dados do SQL Server  
  
1.  No Gerenciador de Soluções, se sua solução contiver vários projetos, clique com o botão direito do mouse no projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote e clique em **Definir como Objeto de Inicialização** para definir o projeto de inicialização.  
  
2.  No Gerenciador de Soluções, se o projeto contiver vários pacotes, clique com o botão direito do mouse em um pacote e clique em **Definir como Objeto de Inicialização** para definir o pacote de inicialização.  
  
3.  Para executar um pacote, use um dos seguintes procedimentos:  
  
    -   Abra o pacote que você deseja executar e clique em **Iniciar Depuração** na barra de menus ou pressione F5. Após a execução do pacote, pressione Shift+F5 para retornar ao modo de design.  
  
    -   No Gerenciador de Soluções, clique com o botão direito do mouse no pacote e, em seguida, clique em **Executar Pacote**.  
  
### Para especificar uma pasta diferente para implantação em tempo de design  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse na pasta de projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote que você deseja executar e clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Página de Propriedades** do \<nome do projeto>, clique em **Compilar**.  
  
3.  Atualize o valor na propriedade OutputPath para especificar a pasta que você deseja usar para a implantação em tempo de design e clique em **OK**.  
  
## Consulte também  
 [Execução de projetos e pacotes](https://msdn.microsoft.com/library/hh213290.aspx)   
 [Pacotes do SSIS (Integration Services)](https://msdn.microsoft.com/library/ms141134.aspx)  
  
  