---
title: 'Etapa 2: adicionar e configurar o registro em log | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 56105f3f-e500-4669-8c8e-acf434527727
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 23738ca4258bf61ff95087b1b6e2aeaffa97cafa
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440483"
---
# <a name="step-2-adding-and-configuring-logging"></a>Etapa 2: Adicionar e configurar registro em log
  Nesta tarefa, você habilitará o log do fluxo de dados no pacote Lesson 3.dtsx. Então, você configurará um provedor de log de arquivo de texto para armazenar os eventos PipelineExecutionPlan e PipelineExecuteTrees em log. O provedor de log de arquivos de texto cria logs que são fáceis exibir e transportar. A simplicidade destes arquivos de log faz estes arquivos especialmente úteis durante a fase de teste básico de um pacote. É possível também exibir as entradas de log na janela Eventos de Log do Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
### <a name="to-add-logging-to-the-package"></a>Adicionar log ao pacote  
  
1.  No menu **SSIS** , clique em **Registrar em Log**.  
  
2.  Na caixa de diálogo **Configurar SSIS Logs** , no painel **Contêineres** , certifique-se que o objeto mais alto, que representa o pacote Lição 3, está selecionado.  
  
3.  Na guia **Provedores e Logs** , na caixa **Tipo de provedor** , selecione **SSIS provedor de log para Arquivos de Texto**, e clique **Adicionar**.  
  
     Integration Services adiciona um novo provedor de log de arquivo de texto ao pacote com o **provedor de log SSIS de nome padrão para arquivos de texto**. Agora é possível configurar o novo provedor de log.  
  
4.  Na coluna **nome** , digite `Lesson 3 Log File` .  
  
5.  Opcionalmente, modifique a **Descrição**.  
  
6.  Na coluna **Configuração** , clique em **\<New Connection>** para especificar o destino no qual as informações de log serão gravadas.  
  
     Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos** , para **Tipo de uso**, selecione **Criar Arquivo**e clique em **Procurar**. Por padrão, a caixa de diálogo **Selecione Arquivo** abrirá a pasta do projeto, mas você pode salvar o log em qualquer localização.  
  
7.  Na caixa de diálogo **Selecionar arquivo** , na caixa **nome do arquivo** `TutorialLog.log` , digite e clique em **abrir**.  
  
8.  Clique em **OK** para fechar a caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos** .  
  
9. No painel **Contêineres** , expandir todos os nós da hierarquia do contêiner do pacote, e limpe todas as caixas de seleção, inclusive a caixa de seleção **Extrair Dados de Exemplo de Moeda** . Agora marque a caixa de seleção **Extrair Dados de Exemplo de Moeda** para adquirir só os eventos para este nó.  
  
    > [!IMPORTANT]  
    >   Se o estado da caixa de seleção **Extrair Dados de Exemplo de Moeda** estiver esmaecido ao invés de marcada, a tarefa usará as configurações de log do contêiner pai e não será possível ativar os eventos de log específicos para a tarefa.  
  
10. Na guia **Detalhes** , na coluna **Eventos** , selecione os eventos **PipelineExecutionPlan** e **PipelineExecutionTrees** .  
  
11. Clique em **Avançado** para revisar os detalhes que o provedor de log escreverá no log para cada evento. Por padrão, todas as categorias de informações são selecionadas automaticamente para os eventos especificados por você.  
  
12. Clique em **Básico** para ocultar as categorias de informações.  
  
13. Na guia **provedor e logs** , na coluna **nome** , selecione `Lesson 3 Log File` . Assim que tiver criado um provedor de log para seu pacote, poderá, como opção, retirar a seleção para temporariamente desligar o registro em log, sem ter que excluir e recriar o provedor de log.  
  
14. Clique em **OK**.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Etapa 3: Testar o pacote de tutorial da Lição 3](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
  
