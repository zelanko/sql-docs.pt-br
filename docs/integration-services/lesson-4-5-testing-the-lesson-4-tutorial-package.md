---
title: 'Etapa 5: Testar o pacote de tutoriais da Lição 4 | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ba5766483def3dc357bc8f1bf65dd1048fa94b48
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295915"
---
# <a name="lesson-4-5-test-the-lesson-4-package"></a>Lição 4-5: Testar o pacote da Lição 4

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



No tempo de execução, o arquivo corrompido, **Currency_BAD.txt**, não gera uma correspondência dentro da transformação Pesquisa de Códigos de Moeda. Como você configurou a saída de erro de Pesquisa de Códigos de Moeda para redirecionar linhas com falhas para o novo destino de linhas com falha, o componente não falha e o pacote é executado com êxito. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] grava todas as linhas de erro com falha em **ErrorOutput.txt**.  
  
Nesta tarefa, você testa a configuração de saída do erro revisado executando o pacote. Após a execução bem-sucedida do pacote, você exibe o conteúdo do arquivo **ErrorOutput.txt**.  
  
> [!NOTE]  
> Se você não quiser acumular linhas de erro no arquivo **ErrorOutput.txt**, exclua manualmente o conteúdo do arquivo entre execuções de pacotes.  
  
## <a name="check-the-package-layout"></a>Verificar o layout do pacote  
Antes de testar o pacote, verifique se que o fluxo de controle e o fluxo de dados no pacote da lição 4 são semelhantes aos diagramas a seguir: 
  
**Fluxo de Controle**  
  
![Fluxo de controle no pacote](../integration-services/media/task4lesson2control.gif "Fluxo de controle no pacote")  
  
**Fluxo de Dados**  
  
![Fluxo de dados no pacote](../integration-services/media/task5lesson5data.gif "Fluxo de dados no pacote")  
  
## <a name="run-the-lesson-4-tutorial-package"></a>Executar o pacote de tutorial da Lição 4  
  
1.  No menu **Depurar**, selecione **Iniciar Depuração**.  
  
2.  Terminada a execução do pacote, no menu **Depurar**, selecione **Parar Depuração**.  
  
## <a name="view-the-contents-of-the-erroroutputtxt-file"></a>Exibir o conteúdo do arquivo ErrorOutput.txt  
  
No Bloco de Notas ou qualquer outro editor de texto, abra o arquivo **ErrorOutput.txt**. A ordem padrão das colunas é: AverageRate, CurrencyID, CurrencyDate, EndOfDateRate, ErrorCode, ErrorColumn, ErrorDescription.  
 
Todas as linhas no arquivo contêm o valor sem correspondência CurrencyID "BAD", o valor ErrorCode -1071607778, o valor ErrorColumn 0 e o valor ErrorDescription "A linha não gerou correspondência durante a pesquisa". O valor de ErrorColumn é 0 porque o erro não é específico de coluna, em vez disso, a operação de pesquisa falhou.
  
  
## <a name="next-lesson"></a>Próxima lição
[Lição 5: Adicionar configurações do pacote SSIS ao modelo de implantação de pacotes](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
