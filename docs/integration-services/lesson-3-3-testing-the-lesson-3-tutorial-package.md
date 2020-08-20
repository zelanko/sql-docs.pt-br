---
description: 'Lição 3-3: Testar o pacote de tutorial da Lição 3'
title: 'Etapa 3: Testar o pacote de tutoriais da Lição 3 | Microsoft Docs'
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 25536606b345093c0723c9b547713d9223dadbb3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471958"
---
# <a name="lesson-3-3-test-the-lesson-3-tutorial-package"></a>Lição 3-3: Testar o pacote de tutorial da Lição 3

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Nesta tarefa, você executa o pacote **Lesson 3.dtsx**. Conforme o pacote é executado, a janela **Registrar Eventos em Log** relaciona as entradas de log que o SSIS grava no arquivo de log pelo provedor de logs. Depois que o pacote concluir a execução, você poderá exibir o conteúdo do arquivo de log.  
  
## <a name="check-the-package-layout"></a>Verificar o layout do pacote  
Antes de testar o pacote, verifique se os fluxos de controle e de dados do pacote da Lição 3 lembram os objetos mostrados nos diagramas a seguir. O fluxo de controle deve ser igual ao da lição 2 e o fluxo de dados deve ser igual ao das lições 1 e 2.  
  
**Fluxo de Controle**  
  
![Fluxo de controle no pacote](../integration-services/media/task4lesson2control.gif "Fluxo de controle no pacote")  
  
**Fluxo de Dados**  
  
![Fluxo de dados no pacote](../integration-services/media/task9lesson1data.gif "Fluxo de dados no pacote")  
  
## <a name="run-the-lesson-3-tutorial-package"></a>Executar o pacote de tutorial da Lição 3  
  
1.  No menu SSIS, selecione **Eventos de Log**.  
  
2.  No menu **Depurar**, selecione **Iniciar Depuração**.  
  
3.  Terminada a execução do pacote, no menu **Depurar**, selecione **Parar Depuração**.  
  
## <a name="examine-the-generated-log-file"></a>Examinar o arquivo de log gerado  
  
-   Com o bloco de notas ou qualquer outro editor de texto, abra o arquivo TutorialLog.log.  
  
-   Uma descrição completa das informações geradas para os eventos **PipelineExecutionPlan** e **PipelineExecutionTrees** está além do escopo deste tutorial.  No arquivo de log, você pode ver que a primeira linha lista os campos de informações especificados na guia **Detalhes** da caixa de diálogo **Configurar Logs de SSIS**. Você também pode ver que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] registrou em log os dois eventos que você selecionou, **PipelineExecutionPlan** e **PipelineExecutionTrees**, para cada iteração do Foreach Loop.  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 4: Adicionar o redirecionamento de fluxo de erro com o SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
  
