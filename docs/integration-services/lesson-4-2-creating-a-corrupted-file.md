---
title: 'Etapa 2: Criar um arquivo corrompido | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cd9266512675c4127a99903e6de0d1da5ccaec70
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295956"
---
# <a name="lesson-4-2-create-a-corrupted-file"></a>Lição 4-2: Criar um arquivo corrompido

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Para demonstrar a configuração e o tratamento de erros de transformação, você precisa criar um arquivo simples de amostra que no processamento causa a falha de um componente.  
  
Nesta tarefa, você cria uma cópia de um arquivo simples de amostra existente. Em seguida, abra o arquivo no bloco de notas e edite a coluna **CurrencyID** para conter um valor errado, que falha na pesquisa. Quando o arquivo corrompido for processado, a falha na pesquisa causará a falha da transformação Pesquisa de Códigos de Moeda e criará, portanto, uma falha no resto do pacote. Depois de criar o arquivo de amostra corrompido, você executa o pacote para exibir a falha do pacote.  
  
## <a name="create-a-corrupted-sample-flat-file"></a>Criar um arquivo simples de amostra corrompido  
  
1.  No Bloco de Notas ou em qualquer outro editor de texto, abra o arquivo **Currency_VEB.txt**.  
  
2.  Use o recurso de localizar e substituir do editor de texto para encontrar todas as instâncias de **VEB** e substituí-los por **BAD**.  
  
3.  Na mesma pasta dos outros arquivos de dados de exemplo, salve o arquivo modificado como **Currency_BAD.txt**.  
  
    > [!NOTE]  
    > Lembre-se de salvar **Currency_BAD.txt** na mesma pasta que os outros arquivos de dados de exemplo.  
  
4.  Feche seu editor de texto.  
  
## <a name="verify-that-an-error-occurs-during-run-time"></a>Verificar se ocorre um erro durante o tempo de execução  
  
1.  No menu **Depurar**, selecione **Iniciar Depuração**.  
  
    Na terceira repetição do fluxo de dados, uma transformação Pesquisa de Códigos de Moeda tenta processar o arquivo **Currency_BAD.txt** e a transformação falha. A falha da transformação faz todo o pacote falhar.  
  
2.  No menu **Depurar**, selecione **Interromper Depuração**.  
  
3.  Na superfície de design, selecione a guia **Resultados da Execução**.  
  
4.  Procure no log e verifique se o seguinte erro sem-tratamento ocorreu:  
  
    ```
    [Lookup Currency Key[27]] Error: Row yielded no match during lookup.
    ```
  
    > [!NOTE]  
    > O número 27 é a ID do componente. Esse valor é atribuído quando você cria o fluxo de dados, ou seja, o valor do seu pacote pode ser diferente.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa  
[Etapa 3: Adicionar redirecionamento de fluxo de erro](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
  
  
