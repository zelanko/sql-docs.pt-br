---
title: 'Etapa 4: adicionar uma tarefa de fluxo de dados ao pacote | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 96af3073-8f11-4444-b934-fe8613a2d084
caps.latest.revision: 21
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 29c42e491c6d36c20073a801051d8861d03ab0f6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118715"
---
# <a name="step-4-adding-a-data-flow-task-to-the-package"></a>Etapa 4: Adicionando uma tarefa de fluxo de dados ao pacote
  Depois de criar os gerenciadores de conexões para os dados de origem e destino, a próxima tarefa é adicionar a tarefa Fluxo de Dados ao seu pacote. Essa tarefa encapsula o mecanismo de fluxo de dados que move dados entre as origens e os destinos, além de fornecer funcionalidade para transformar, limpar e modificar os dados à medida que são movidos. A tarefa Fluxo de Dados é onde a maioria do trabalho de um processo de extração, transformação e carregamento (ETL) acontece.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] separa o fluxo de dados do fluxo de controle.  
  
### <a name="to-add-a-data-flow-task"></a>Adicionar uma tarefa Fluxo de Dados  
  
1.  Clique na guia **Fluxo de Controle** .  
  
2.  Na **Caixa de Ferramentas do SSIS**, expanda **Favoritos**e arraste uma **Tarefa de Fluxo de Dados** até a superfície de design da guia **Fluxo de Controle** .  
  
    > [!NOTE]  
    >  Se a Caixa de Ferramentas do SSIS não estiver disponível, no menu principal, selecione Caixa de Ferramentas do SSIS para exibir a Caixa de Ferramentas do SSIS.  
  
3.  Sobre o **fluxo de controle** superfície de design, clique no recém-adicionado **a tarefa de fluxo de dados**, clique em **Renomear**e altere o nome para `Extract Sample Currency Data`.  
  
     É uma boa ideia fornecer nomes exclusivos a todos os componentes que você adiciona a uma superfície de design. Para facilitar o uso e a sustentabilidade, os nomes devem descrever a função que cada componente executa. Seguir estas diretrizes de nomeação permite que seus pacotes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sejam documentados automaticamente. Outra forma para documentar seus pacotes é usar anotações. Para obter mais informações sobre como usar anotações, consulte [Usar anotações em pacotes](use-annotations-in-packages.md).  
  
4.  A tarefa de fluxo de dados, clique **propriedades**e na janela Propriedades, verifique se o `LocaleID` está definida como **inglês (Estados Unidos)**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Etapa 5: Adicionando e configurando a fonte de arquivo simples](lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa de Fluxo de Dados](control-flow/data-flow-task.md)  
  
  