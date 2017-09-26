---
title: "Etapa 3: Testando o pacote de Tutorial da lição 3 | Microsoft Docs"
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
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d6477267c95ffd200f70b2c93191dfaf0883a4af
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-3-3---testing-the-lesson-3-tutorial-package"></a>Lição 3 de 3: Testando o pacote de Tutorial da lição 3
Nesta tarefa, você executará o pacote Lesson 3.dtsx. Quando o pacote for executado, a janela Eventos de Log listará as entradas de log gravadas no arquivo de log. Após a execução do pacote ser concluída, você verificará o conteúdo do arquivo de log gerado pelo provedor do log.  
  
## <a name="checking-the-package-layout"></a>Verificando o layout do pacote  
Antes de testar o pacote, é recomendável verificar se os fluxos de controle e de dados do pacote da Lição 3 contêm os objetos mostrados nos diagramas a seguir. O fluxo de controle deve ser idêntico ao fluxo de controle da Lição 2. O fluxo de dados deve ser idêntico ao fluxo de dados das lições 1 e 2.  
  
**Fluxo de Controle**  
  
![Controlar o fluxo do pacote](../integration-services/media/task4lesson2control.gif "controlar o fluxo do pacote")  
  
**Fluxo de Dados**  
  
![Fluxo de dados no pacote](../integration-services/media/task9lesson1data.gif "no pacote de fluxo de dados")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>Para executar o pacote de tutorial da lição 4  
  
1.  No menu SSIS, clique em Eventos de Log.  
  
2.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
3.  Terminada a execução do pacote, no menu **Depurar** , clique em **Parar Depuração**.  
  
### <a name="to-examine-the-generated-log-file"></a>Para examinar o arquivo de log gerado  
  
-   Com o bloco de notas ou qualquer outro editor de texto, abra o arquivo TutorialLog.log.  
  
-   Embora as semânticas das informações geradas para os eventos **PipelineExecutionPlan** e **PipelineExecutionTrees** estejam além do escopo deste tutorial, você pode ver que a primeira linha lista os campos de informações especificados na guia **Detalhes** da caixa de diálogo **Configurar Logs de SSIS** . Além disso, é possível verificar se os dois eventos selecionados, PipelineExecutionPlan e PipelineExecutionTrees, foram conectados para cada iteração do Loop Foreach.  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 4: Adicionar o redirecionamento de fluxo de erro com o SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
  

