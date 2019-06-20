---
title: 'Etapa 3: Testando o pacote de Tutorial da lição 3 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ac1aa0c45e8201d50ead862dd1631bbb3324c8e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62891584"
---
# <a name="step-3-testing-the-lesson-3-tutorial-package"></a>Etapa 3: Testar o pacote de tutorial da Lição 3
  Nesta tarefa, você executará o pacote Lesson 3.dtsx. Quando o pacote for executado, a janela Eventos de Log listará as entradas de log gravadas no arquivo de log. Após a execução do pacote ser concluída, você verificará o conteúdo do arquivo de log gerado pelo provedor do log.  
  
## <a name="checking-the-package-layout"></a>Verificando o layout do pacote  
 Antes de testar o pacote, é recomendável verificar se os fluxos de controle e de dados do pacote da Lição 3 contêm os objetos mostrados nos diagramas a seguir. O fluxo de controle deve ser idêntico ao fluxo de controle da Lição 2. O fluxo de dados deve ser idêntico ao fluxo de dados das lições 1 e 2.  
  
 **Fluxo de Controle**  
  
 ![Fluxo de controle no pacote](../../2014/tutorials/media/task4lesson2control.gif "Fluxo de controle no pacote")  
  
 **Fluxo de Dados**  
  
 ![Fluxo de dados no pacote](../../2014/tutorials/media/task9lesson1data.gif "Fluxo de dados no pacote")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>Para executar o pacote de tutorial da lição 4  
  
1.  No menu SSIS, clique em Eventos de Log.  
  
2.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
3.  Terminada a execução do pacote, no menu **Depurar** , clique em **Parar Depuração**.  
  
### <a name="to-examine-the-generated-log-file"></a>Para examinar o arquivo de log gerado  
  
-   Com o bloco de notas ou qualquer outro editor de texto, abra o arquivo TutorialLog.log.  
  
-   Embora as semânticas das informações geradas para o `PipelineExecutionPlan` e `PipelineExecutionTrees` eventos estão além do escopo deste tutorial, você pode ver que a primeira linha lista os campos de informações especificados na **detalhes** guia de o **configurar Logs de SSIS** caixa de diálogo. Além disso, é possível verificar se os dois eventos selecionados, PipelineExecutionPlan e PipelineExecutionTrees, foram conectados para cada iteração do Loop Foreach.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 4: Adicionando redirecionamento de fluxo de erro](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
