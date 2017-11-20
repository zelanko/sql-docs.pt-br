---
title: "Etapa 5: Testando o pacote de Tutorial da lição 4 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 68e4545ee2eae96664007a8dc69c9953c0351107
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-4-5---testing-the-lesson-4-tutorial-package"></a>Lição 4-5: Testando o pacote de Tutorial da lição 4
No tempo de execução, o arquivo corrompido, Currency_BAD.txt, não gerará uma correspondência dentro da transformação Pesquisa de Códigos de Moeda. Como a saída de erro de Pesquisa de Códigos de Moeda foi configurada para redirecionar linhas com falhas para o novo destino de linhas com falha, o componente não falha e o pacote é executado com êxito. Todas as linhas com erro são gravadas em ErrorOutput.txt.  
  
Nesta tarefa, você testará a configuração de saída do erro revisado executando o pacote. Com a execução bem-sucedida do pacote, você verá o conteúdo do arquivo ErrorOutput.txt.  
  
> [!NOTE]  
> Se você não quiser acumular linhas de erro no arquivo ErrorOutput.txt, exclua manualmente o conteúdo do arquivo entre execuções de pacotes.  
  
## <a name="checking-the-package-layout"></a>Verificando o layout do pacote  
Antes de você testar o pacote, é recomendável verificar se o fluxo de controle e o fluxo de dados do pacote da lição 4 contêm os objetos mostrados nos diagramas seguintes. O fluxo de controle deve ser idêntico ao fluxo de controle das lições 2 - 4.  
  
**Fluxo de Controle**  
  
![Controlar o fluxo do pacote](../integration-services/media/task4lesson2control.gif "controlar o fluxo do pacote")  
  
**Fluxo de Dados**  
  
![Fluxo de dados no pacote](../integration-services/media/task5lesson5data.gif "no pacote de fluxo de dados")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>Para executar o pacote de tutorial da lição 4  
  
1.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
2.  Terminada a execução do pacote, no menu **Depurar** , clique em **Parar Depuração**.  
  
### <a name="to-verify-the-contents-of-the-erroroutputtxt-file"></a>Para verificar o conteúdo do arquivo ErrorOutput.txt  
  
-   No Bloco de Notas ou qualquer outro editor de texto, abra o arquivo ErrorOutput.txt. A ordem de colunas padrão é: AverageRate, CurrencyID, CurrencyDate, EndOfDateRate, ErrorCode, ErrorColumn, ErrorDescription.  
  
    Observe que todas as linhas do arquivo contêm o valor CurrencyID de BAD, o valor ErrorCode de -1071607778, o valor ErrorColumn de 0 e o valor ErrorDescription de "Row yielded no match during lookup." O valor de ErrorColumn é definido como 0 porque o erro não é específico da coluna. A operação de pesquisa que falhou. .  
  
  
  

