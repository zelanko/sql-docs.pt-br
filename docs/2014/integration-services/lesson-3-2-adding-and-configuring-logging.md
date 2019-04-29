---
title: 'Etapa 2: Adicionando e Configurando registro em log | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 56105f3f-e500-4669-8c8e-acf434527727
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ef4f5d42ae3451d4199e84480a5672e437d7ca5f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62892431"
---
# <a name="step-2-adding-and-configuring-logging"></a>Etapa 2: Adicionar e configurar registro em log
  Nesta tarefa, você habilitará o log do fluxo de dados no pacote Lesson 3.dtsx. Então, você configurará um provedor de log de arquivo de texto para armazenar os eventos PipelineExecutionPlan e PipelineExecuteTrees em log. O provedor de log de arquivos de texto cria logs que são fáceis exibir e transportar. A simplicidade destes arquivos de log faz estes arquivos especialmente úteis durante a fase de teste básico de um pacote. É possível também exibir as entradas de log na janela Eventos de Log do Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
### <a name="to-add-logging-to-the-package"></a>Adicionar log ao pacote  
  
1.  No menu **SSIS** , clique em **Registrar em Log**.  
  
2.  Na caixa de diálogo **Configurar SSIS Logs** , no painel **Contêineres** , certifique-se que o objeto mais alto, que representa o pacote Lição 3, está selecionado.  
  
3.  Na guia **Provedores e Logs** , na caixa **Tipo de provedor** , selecione **SSIS provedor de log para Arquivos de Texto**, e clique **Adicionar**.  
  
     O Integration Services adiciona um novo provedor de log para arquivos de texto para o pacote, com o nome padrão **SSIS provedor de logo para arquivos de texto**. Agora é possível configurar o novo provedor de log.  
  
4.  No **nome** coluna, digite `Lesson 3 Log File`.  
  
5.  Opcionalmente, modifique a **Descrição**.  
  
6.  No **Configuration** coluna, clique em  **\<nova Conexão >** para especificar o destino no qual as informações de log são gravadas.  
  
     Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos** , para **Tipo de uso**, selecione **Criar Arquivo**e clique em **Procurar**. Por padrão, a caixa de diálogo **Selecione Arquivo** abrirá a pasta do projeto, mas você pode salvar o log em qualquer localização.  
  
7.  No **Selecionar arquivo** na caixa a **nome do arquivo** caixa, digite `TutorialLog.log`e clique em **abrir**.  
  
8.  Clique em **OK** para fechar a caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos** .  
  
9. No painel **Contêineres** , expandir todos os nós da hierarquia do contêiner do pacote, e limpe todas as caixas de seleção, inclusive a caixa de seleção **Extrair Dados de Exemplo de Moeda** . Agora marque a caixa de seleção **Extrair Dados de Exemplo de Moeda** para adquirir só os eventos para este nó.  
  
    > [!IMPORTANT]  
    >  Se o estado da caixa de seleção **Extrair Dados de Exemplo de Moeda** estiver esmaecido em vez de marcado, a tarefa usará as configurações de log do contêiner pai e não será possível habilitar os eventos de log específicos da tarefa.  
  
10. Na guia **Detalhes** , na coluna **Eventos** , selecione os eventos **PipelineExecutionPlan** e **PipelineExecutionTrees** .  
  
11. Clique em **Avançado** para revisar os detalhes que o provedor de log escreverá no log para cada evento. Por padrão, todas as categorias de informações são selecionadas automaticamente para os eventos especificados por você.  
  
12. Clique em **Básico** para ocultar as categorias de informações.  
  
13. Sobre o **provedor e Logs** guia da **nome** coluna, selecione `Lesson 3 Log File`. Assim que tiver criado um provedor de log para seu pacote, poderá, como opção, retirar a seleção para temporariamente desligar o registro em log, sem ter que excluir e recriar o provedor de log.  
  
14. Clique em **OK**.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Etapa 3: Testando o pacote de Tutorial da lição 3](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
  
