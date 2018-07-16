---
title: Configurar uma saída de erro em um componente de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [Integration Services], data flow components
- components [Integration Services], data flow
- error outputs [Integration Services]
ms.assetid: 53d7eeea-927d-4b45-8ea9-084e65ad5390
caps.latest.revision: 31
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4e61c6583a58ffb2ae84af9a4050ca077fb11b80
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37329866"
---
# <a name="configure-an-error-output-in-a-data-flow-component"></a>Configurar uma saída de erro em um componente de fluxo de dados
  Muitos componentes de fluxo de dados dão suporte a saídas de erro e, dependendo do componente, o [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer fornece diferentes modos de configurar uma saída de erro. Além de configurar uma saída de erro, você pode configurar também as colunas de uma saída de erro. Isto inclui a configuração das colunas **ErrorCode** e **ErrorColumn** que são adicionadas pelo componente.  
  
## <a name="configuring-an-error-output"></a>Configurando uma saída de erro  
 Para configurar uma saída de erro, você tem duas opções:  
  
-   Use a caixa de diálogo **Configurar Saída de Erro** . Você pode usar esta caixa de diálogo para configurar uma saída de erro em qualquer componente de fluxo de dados que ofereça suporte a saídas de erro.  
  
-   Use a caixa de diálogo do editor para o componente. Alguns componentes permitem que você configure saídas de erro diretamente na caixa de diálogo do editor. Entretanto, você não pode configurar saídas de erros da caixa de diálogo do editor para a origem do ADO NET, a transformação de Importar Coluna e do Comando OLE DB ou para o destino do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 Os procedimentos a seguir descrevem como usar estas caixas de diálogo para configurar saídas de erro.  
  
#### <a name="to-configure-an-error-output-using-the-configure-error-output-dialog-box"></a>Para configurar uma saída de erro que usa a caixa de diálogo Configurar Saída de Erro  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer, clique na guia **Fluxo de Dados** .  
  
4.  Arraste a saída de erro, representada pela seta vermelha, do componente que é a fonte dos erros para outro componente no fluxo de dados.  
  
5.  Na caixa de diálogo **Configurar Saída de Erro** , selecione uma ação nas colunas **Erro** e **Truncamento** para cada coluna da entrada de componente.  
  
6.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
#### <a name="to-add-an-error-output-using-the-editor-dialog-box-for-the-component"></a>Para adicionar uma saída de erro que usa a caixa de diálogo do editor para o componente  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer, clique na guia **Fluxo de Dados** .  
  
4.  Clique duas vezes nos componentes de fluxo de dados em que você deseja configurar uma saída de erro e, dependendo do componente, siga uma destas etapas:  
  
    -   Clique em **Configurar Saída de Erro**.  
  
    -   Clique em **Saída de Erro**.  
  
5.  Defina a opção **Erro** para cada coluna.  
  
6.  Defina a opção **Truncamento** para cada coluna.  
  
7.  Clique em **OK**.  
  
8.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
## <a name="configuring-error-output-columns"></a>Configurando colunas de saída de erro  
 Para configurar colunas de saída de erro, você deve usar a guia **Propriedades de Entrada e Saída** na caixa de diálogo **Editor Avançado** .  
  
#### <a name="to-configure-error-output-columns"></a>Para configurar colunas de saída de erro  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer, clique na guia **Fluxo de Dados** .  
  
4.  Clique com o botão direito do mouse no componente cujas colunas de saída de erro você deseja configurar e clique em **Mostrar Editor Avançado**.  
  
5.  Clique na guia **Propriedades de Entrada e Saída** e expanda **Saída de Erro do \<component name>** e, em seguida, expanda **Colunas de Saída**.  
  
6.  Clique em uma coluna e atualize suas propriedades.  
  
    > [!NOTE]  
    >  A lista de colunas inclui as colunas na entrada do componente, as colunas **ErrorCode** e **ErrorColumn** adicionadas pelas saídas de erros anteriores e as colunas **ErrorCode** e **ErrorColumn** adicionadas por este componente.  
  
7.  Clique em **OK.**  
  
8.  Para salvar o pacote atualizado, no menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
## <a name="see-also"></a>Consulte também  
 [Tratamento de erro em dados](data-flow/error-handling-in-data.md)  
  
  
