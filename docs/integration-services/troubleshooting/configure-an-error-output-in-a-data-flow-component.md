---
title: "Configurar uma sa&#237;da de erro em um componente de fluxo de dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "erros [Integration Services], componentes de fluxo de dados"
  - "componentes [Integration Services], fluxo de dados"
  - "saídas de erro [Integration Services]"
ms.assetid: 53d7eeea-927d-4b45-8ea9-084e65ad5390
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# Configurar uma sa&#237;da de erro em um componente de fluxo de dados
  Muitos componentes de fluxo de dados dão suporte a saídas de erro e, dependendo do componente, o [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer fornece diferentes modos de configurar uma saída de erro. Além de configurar uma saída de erro, você pode configurar também as colunas de uma saída de erro. Isto inclui a configuração das colunas **ErrorCode** e **ErrorColumn** que são adicionadas pelo componente.  
  
## Configurando uma saída de erro  
 Para configurar uma saída de erro, você tem duas opções:  
  
-   Use a caixa de diálogo **Configurar Saída de Erro** . Você pode usar esta caixa de diálogo para configurar uma saída de erro em qualquer componente de fluxo de dados que ofereça suporte a saídas de erro.  
  
-   Use a caixa de diálogo do editor para o componente. Alguns componentes permitem que você configure saídas de erro diretamente na caixa de diálogo do editor. Entretanto, você não pode configurar saídas de erros da caixa de diálogo do editor para a origem do ADO NET, a transformação de Importar Coluna e do Comando OLE DB ou para o destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 Os procedimentos a seguir descrevem como usar estas caixas de diálogo para configurar saídas de erro.  
  
#### Para configurar uma saída de erro que usa a caixa de diálogo Configurar Saída de Erro  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique na guia **Fluxo de Dados** .  
  
4.  Arraste a saída de erro, representada pela seta vermelha, do componente que é a fonte dos erros para outro componente no fluxo de dados.  
  
5.  Na caixa de diálogo **Configurar Saída de Erro** , selecione uma ação nas colunas **Erro** e **Truncamento** para cada coluna da entrada de componente.  
  
6.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
#### Para adicionar uma saída de erro que usa a caixa de diálogo do editor para o componente  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique na guia **Fluxo de Dados** .  
  
4.  Clique duas vezes nos componentes de fluxo de dados em que você deseja configurar uma saída de erro e, dependendo do componente, siga uma destas etapas:  
  
    -   Clique em **Configurar Saída de Erro**.  
  
    -   Clique em **Saída de Erro**.  
  
5.  Defina a opção **Erro** para cada coluna.  
  
6.  Defina a opção **Truncamento** para cada coluna.  
  
7.  Clique em **OK**.  
  
8.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
## Configurando colunas de saída de erro  
 Para configurar colunas de saída de erro, você deve usar a guia **Propriedades de Entrada e Saída** na caixa de diálogo **Editor Avançado** .  
  
#### Para configurar colunas de saída de erro  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique na guia **Fluxo de Dados** .  
  
4.  Clique com o botão direito do mouse no componente cujas colunas de saída de erro você deseja configurar e clique em **Mostrar Editor Avançado**.  
  
5.  Clique na guia **Propriedades de Entrada e Saída** e expanda **Saída de Erro do \<nome do componente>** e, em seguida, expanda **Colunas de Saída**.  
  
6.  Clique em uma coluna e atualize suas propriedades.  
  
    > [!NOTE]  
    >  A lista de colunas inclui as colunas na entrada do componente, as colunas **ErrorCode** e **ErrorColumn** adicionadas pelas saídas de erros anteriores e as colunas **ErrorCode** e **ErrorColumn** adicionadas por este componente.  
  
7.  Clique em **OK.**  
  
8.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
## Consulte também  
 [Tratamento de erros em dados](../../integration-services/data-flow/error-handling-in-data.md)  
  
  