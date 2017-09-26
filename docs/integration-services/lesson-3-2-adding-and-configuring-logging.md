---
title: 'Etapa 2: Adicionando e Configurando registro em log | Microsoft Docs'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 56105f3f-e500-4669-8c8e-acf434527727
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 37702c62d20217d11785351b69252e08f03c0985
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-3-2---adding-and-configuring-logging"></a>Lição 3-2-adicionando e Configurando registro em log
Nesta tarefa, você habilitará o log do fluxo de dados no pacote Lesson 3.dtsx. Então, você configurará um provedor de log de arquivo de texto para armazenar os eventos PipelineExecutionPlan e PipelineExecuteTrees em log. O provedor de log de arquivos de texto cria logs que são fáceis exibir e transportar. A simplicidade destes arquivos de log faz estes arquivos especialmente úteis durante a fase de teste básico de um pacote. É possível também exibir as entradas de log na janela Eventos de Log do Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
### <a name="to-add-logging-to-the-package"></a>Adicionar log ao pacote  
  
1.  No menu **SSIS** , clique em **Registrar em Log**.  
  
2.  Na caixa de diálogo **Configurar SSIS Logs** , no painel **Contêineres** , certifique-se que o objeto mais alto, que representa o pacote Lição 3, está selecionado.  
  
3.  Na guia **Provedores e Logs** , na caixa **Tipo de provedor** , selecione **SSIS provedor de log para Arquivos de Texto**, e clique **Adicionar**.  
  
    O Integration Services adiciona um novo provedor de log para arquivos de texto para o pacote, com o nome padrão **SSIS provedor de logo para arquivos de texto**. Agora é possível configurar o novo provedor de log.  
  
4.  Na coluna **Nome** , digite **Lesson 3 Log File**.  
  
5.  Opcionalmente, modifique a **Descrição**.  
  
6.  Na coluna **Configuração** , clique em **<New Connection>** para especificar o destino no qual as informações de log serão gravadas.  
  
    Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos** , para **Tipo de uso**, selecione **Criar Arquivo**e clique em **Procurar**. Por padrão, a caixa de diálogo **Selecione Arquivo** abrirá a pasta do projeto, mas você pode salvar o log em qualquer localização.  
  
7.  Na caixa de diálogo **Selecionar Arquivo** , em **Nome do Arquivo** digite **TutorialLog.log**, e clique em **Abrir**.  
  
8.  Clique em **OK** para fechar a caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos** .  
  
9. No painel **Contêineres** , expandir todos os nós da hierarquia do contêiner do pacote, e limpe todas as caixas de seleção, inclusive a caixa de seleção **Extrair Dados de Exemplo de Moeda** . Agora marque a caixa de seleção **Extrair Dados de Exemplo de Moeda** para adquirir só os eventos para este nó.  
  
    > [!IMPORTANT]  
    > Se o estado da caixa de seleção **Extrair Dados de Exemplo de Moeda** estiver esmaecido em vez de marcado, a tarefa usará as configurações de log do contêiner pai e não será possível habilitar os eventos de log específicos da tarefa.  
  
10. Na guia **Detalhes** , na coluna **Eventos** , selecione os eventos **PipelineExecutionPlan** e **PipelineExecutionTrees** .  
  
11. Clique em **Avançado** para revisar os detalhes que o provedor de log escreverá no log para cada evento. Por padrão, todas as categorias de informações são selecionadas automaticamente para os eventos especificados por você.  
  
12. Clique em **Básico** para ocultar as categorias de informações.  
  
13. Na guia **Provedor e Logs** , na coluna **Nome** , selecione **Arquivo de Log da Lição 3**. Assim que tiver criado um provedor de log para seu pacote, poderá, como opção, retirar a seleção para temporariamente desligar o registro em log, sem ter que excluir e recriar o provedor de log.  
  
14. Clique em **OK**.  
  
## <a name="next-steps"></a>Próximas etapas  
[Etapa 3: Testando o pacote de tutorial da Lição 3](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  

