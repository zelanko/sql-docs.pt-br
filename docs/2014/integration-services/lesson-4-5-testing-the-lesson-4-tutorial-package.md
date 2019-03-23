---
title: 'Etapa 5: Testando o pacote de Tutorial da lição 4 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fab91a2df7d0401e8301589b1dd0d21027e579c6
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377814"
---
# <a name="step-5-testing-the-lesson-4-tutorial-package"></a>Etapa 5: Testando o pacote de tutorial da Lição 4
  No tempo de execução, o arquivo corrompido, Currency_BAD.txt, não gerará uma correspondência dentro da transformação Pesquisa de Códigos de Moeda. Como a saída de erro de Pesquisa de Códigos de Moeda foi configurada para redirecionar linhas com falhas para o novo destino de linhas com falha, o componente não falha e o pacote é executado com êxito. Todas as linhas com erro são gravadas em ErrorOutput.txt.  
  
 Nesta tarefa, você testará a configuração de saída do erro revisado executando o pacote. Com a execução bem-sucedida do pacote, você verá o conteúdo do arquivo ErrorOutput.txt.  
  
> [!NOTE]  
>  Se você não quiser acumular linhas de erro no arquivo ErrorOutput.txt, exclua manualmente o conteúdo do arquivo entre execuções de pacotes.  
  
## <a name="checking-the-package-layout"></a>Verificando o layout do pacote  
 Antes de você testar o pacote, é recomendável verificar se o fluxo de controle e o fluxo de dados do pacote da lição 4 contêm os objetos mostrados nos diagramas seguintes. O fluxo de controle deve ser idêntico ao fluxo de controle das lições 2 - 4.  
  
 **Fluxo de Controle**  
  
 ![Fluxo de controle no pacote](../../2014/tutorials/media/task4lesson2control.gif "Fluxo de controle no pacote")  
  
 **Fluxo de Dados**  
  
 ![Fluxo de dados no pacote](../../2014/tutorials/media/task5lesson5data.gif "Fluxo de dados no pacote")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>Para executar o pacote de tutorial da lição 4  
  
1.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
2.  Terminada a execução do pacote, no menu **Depurar** , clique em **Parar Depuração**.  
  
### <a name="to-verify-the-contents-of-the-erroroutputtxt-file"></a>Para verificar o conteúdo do arquivo ErrorOutput.txt  
  
-   No Bloco de Notas ou qualquer outro editor de texto, abra o arquivo ErrorOutput.txt. A ordem padrão das colunas é: AverageRate, CurrencyID, CurrencyDate, EndOfDateRate, ErrorCode, ErrorColumn, ErrorDescription.  
  
     Observe que todas as linhas do arquivo contêm o valor CurrencyID de BAD, o valor ErrorCode de -1071607778, o valor ErrorColumn de 0 e o valor ErrorDescription de "Row yielded no match during lookup." O valor de ErrorColumn é definido como 0 porque o erro não é específico da coluna. A operação de pesquisa que falhou. para obter informações sobre a ferramenta de configuração e recursos adicionais.  
  
  
