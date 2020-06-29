---
title: 'Etapa 3: testar o pacote de tutoriais da Lição 3 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6ffa1849e099e670b5fa13db399af67883e8806c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440463"
---
# <a name="step-3-testing-the-lesson-3-tutorial-package"></a>Etapa 3: Testar o pacote de tutorial da Lição 3
  Nesta tarefa, você executará o pacote Lesson 3.dtsx. Quando o pacote for executado, a janela Eventos de Log listará as entradas de log gravadas no arquivo de log. Após a execução do pacote ser concluída, você verificará o conteúdo do arquivo de log gerado pelo provedor do log.  
  
## <a name="checking-the-package-layout"></a>Verificando o layout do pacote  
 Antes de testar o pacote, é recomendável verificar se os fluxos de controle e de dados do pacote da Lição 3 contêm os objetos mostrados nos diagramas a seguir. O fluxo de controle deve ser idêntico ao fluxo de controle da Lição 2. O fluxo de dados deve ser idêntico ao fluxo de dados das lições 1 e 2.  
  
 **Fluxo de controle**  
  
 ![Fluxo de controle no pacote](../../2014/tutorials/media/task4lesson2control.gif "Fluxo de controle no pacote")  
  
 **Fluxo de Dados**  
  
 ![Fluxo de dados no pacote](../../2014/tutorials/media/task9lesson1data.gif "Fluxo de dados no pacote")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>Para executar o pacote de tutorial da lição 4  
  
1.  No menu SSIS, clique em Eventos de Log.  
  
2.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
3.  Terminada a execução do pacote, no menu **Depurar** , clique em **Parar Depuração**.  
  
### <a name="to-examine-the-generated-log-file"></a>Para examinar o arquivo de log gerado  
  
-   Com o bloco de notas ou qualquer outro editor de texto, abra o arquivo TutorialLog.log.  
  
-   Embora a semântica das informações geradas para os `PipelineExecutionPlan` eventos e `PipelineExecutionTrees` esteja além do escopo deste tutorial, você pode ver que a primeira linha lista os campos de informações especificados na guia **detalhes** da caixa de diálogo **Configurar Logs do SSIS** . Além disso, é possível verificar se os dois eventos selecionados, PipelineExecutionPlan e PipelineExecutionTrees, foram conectados para cada iteração do Loop Foreach.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 4: Adicionar redirecionamento de fluxo de erro](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
