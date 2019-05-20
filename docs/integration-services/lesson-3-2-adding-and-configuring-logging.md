---
title: 'Etapa 2: Adicionar e configurar registro em log | Microsoft Docs'
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 56105f3f-e500-4669-8c8e-acf434527727
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 80d2eb1ec30b4729deb4891c451fc5967bec9d54
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65722075"
---
# <a name="lesson-3-2-add-and-configure-logging"></a>Lição 3-2: Adicionar e configurar o registro em log

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Nesta tarefa, você habilita o log do fluxo de dados no pacote Lesson 3.dtsx. Então, você configura um provedor de log de arquivo de texto para armazenar os eventos PipelineExecutionPlan e PipelineExecuteTrees em log. O provedor de log de arquivos de texto cria logs que são fáceis exibir e de transportar. A simplicidade destes arquivos de log faz estes arquivos úteis durante a fase de teste básico de um pacote. É possível também exibir as entradas de log na janela **Eventos de Log** do Designer [!INCLUDE[ssIS](../includes/ssis-md.md)].  
  
## <a name="add-logging-to-the-package"></a>Adicionar registro em log ao pacote  
  
1.  No menu **SSIS**, selecione **Registro em Log**.  
  
2.  Na caixa de diálogo **Configurar Logs de SSIS**, no painel **Contêineres**, verifique se o objeto mais alto está selecionado. Esse objeto representa o pacote da Lição 3.
  
3.  Na guia **Provedores e Logs**, na caixa **Tipo de provedor**, selecione **SSIS provedor de log para Arquivos de Texto** e selecione **Adicionar**.  
  
    O Integration Services adiciona um novo provedor de log para Arquivo de Texto para o pacote, com o nome padrão **SSIS provedor de logo para arquivos de texto**. Agora é possível configurar o novo provedor de log.  
  
4.  Na coluna **Nome**, digite **Lição 3 Arquivo de Log**.  
  
5.  Opcionalmente, modifique a **Descrição**.  
  
6.  Na coluna **Configuração**, selecione **\<Nova Conexão>** para especificar em que local o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] grava informações de log.  
  
    Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos**, para **Tipo de uso**, selecione **Criar Arquivo** e selecione **Procurar**. Por padrão, a caixa de diálogo **Selecione Arquivo** abrirá a pasta do projeto, mas você pode salvar o log em qualquer localização.  
  
7.  Na caixa de diálogo **Selecionar Arquivo**, na caixa **Nome do arquivo**, insira **TutorialLog.log** e selecione **Abrir**.
  
8.  Selecione **OK** para fechar a caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos**.  
  
9. No painel **Contêineres** , expandir todos os nós da hierarquia do contêiner do pacote, e limpe todas as caixas de seleção, inclusive a caixa de seleção **Extrair Dados de Exemplo de Moeda** . Agora marque a caixa de seleção **Extrair Dados de Exemplo de Moeda** para adquirir só os eventos para este nó.  
  
    > [!NOTE]  
    > Se o estado da caixa de seleção **Extrair Dados de Exemplo de Moeda** estiver esmaecido, em vez de selecionado, a tarefa usará as configurações de log do contêiner pai e não será possível habilitar os eventos de log específicos da tarefa. Para resolver essa instância, desmarque a caixa de seleção pai.
  
10. Na guia **Detalhes** , na coluna **Eventos** , selecione os eventos **PipelineExecutionPlan** e **PipelineExecutionTrees** .  
  
11. Selecione **Avançado** para examinar os detalhes que o provedor de log gravará no log para cada evento. Por padrão, todas as categorias de informações são selecionadas automaticamente para os eventos especificados por você.  
  
12. Selecione **Básico** para ocultar as categorias de informações.  
  
13. Na guia **Provedor e Logs** , na coluna **Nome** , selecione **Arquivo de Log da Lição 3**. Depois de ter criado um provedor de log para seu pacote, você poderá, como opção, retirar a seleção para desligar o registro em log, sem ter que excluir e recriar o provedor de log.  
  
14. Escolha **OK**.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa  
[Etapa 3: Testar o pacote da Lição 3](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
