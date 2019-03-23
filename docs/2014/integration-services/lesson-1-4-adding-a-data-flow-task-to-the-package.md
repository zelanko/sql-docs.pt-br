---
title: 'Etapa 4: Adicionando uma tarefa de fluxo de dados ao pacote | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 542b7e3ffcc4a1db5b2053c840b785f775384fe1
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381184"
---
# <a name="step-4-adding-a-data-flow-task-to-the-package"></a>Etapa 4: Adicionando uma tarefa de fluxo de dados ao pacote
  Depois de criar os gerenciadores de conexões para os dados de origem e destino, a próxima tarefa é adicionar a tarefa Fluxo de Dados ao seu pacote. Essa tarefa encapsula o mecanismo de fluxo de dados que move dados entre as origens e os destinos, além de fornecer funcionalidade para transformar, limpar e modificar os dados à medida que são movidos. A tarefa Fluxo de Dados é onde a maioria do trabalho de um processo de extração, transformação e carregamento (ETL) acontece.  
  
> [!NOTE]  
>  O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] separa o fluxo de dados do fluxo de controle.  
  
### <a name="to-add-a-data-flow-task"></a>Adicionar uma tarefa Fluxo de Dados  
  
1.  Clique na guia **Fluxo de Controle** .  
  
2.  Na **Caixa de Ferramentas do SSIS**, expanda **Favoritos**e arraste uma **Tarefa de Fluxo de Dados** até a superfície de design da guia **Fluxo de Controle** .  
  
    > [!NOTE]  
    >  Se a Caixa de Ferramentas do SSIS não estiver disponível, no menu principal, selecione Caixa de Ferramentas do SSIS para exibir a Caixa de Ferramentas do SSIS.  
  
3.  Sobre o **fluxo de controle** superfície de design, clique com botão direito recém-adicionada **tarefa de fluxo de dados**, clique em **Renomear**e altere o nome para `Extract Sample Currency Data`.  
  
     É uma boa ideia fornecer nomes exclusivos a todos os componentes que você adiciona a uma superfície de design. Para facilitar o uso e a sustentabilidade, os nomes devem descrever a função que cada componente executa. Seguir estas diretrizes de nomeação permite que seus pacotes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sejam documentados automaticamente. Outra forma para documentar seus pacotes é usar anotações. Para obter mais informações sobre como usar anotações, consulte [Usar anotações em pacotes](use-annotations-in-packages.md).  
  
4.  A tarefa de fluxo de dados com o botão direito, clique em **propriedades**e na janela Propriedades, verifique se o `LocaleID` estiver definida como **inglês (Estados Unidos)**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 5: Adicionando e configurando a fonte de arquivo simples](lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa de Fluxo de Dados](control-flow/data-flow-task.md)  
  
  
