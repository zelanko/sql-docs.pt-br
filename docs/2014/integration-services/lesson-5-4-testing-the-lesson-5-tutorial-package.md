---
title: 'Etapa 4: testar o pacote de tutoriais da Lição 5 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
caps.latest.revision: 25
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f03073cb5568bf3af867d8cd055bb5bb976ad493
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119569"
---
# <a name="step-4-testing-the-lesson-5-tutorial-package"></a>Etapa 4: Testando o pacote de tutorial da Lição 5
  Em tempo de execução, o pacote irá obter o valor da propriedade `Directory` de uma variável atualizada em tempo de execução, ao invés de utilizar o nome original de diretório que foi especificado quando você criou o pacote. O valor da variável é populado pelo arquivo SSISTutorial.dtsConfig.  
  
 Para verificar se, em tempo de execução, o pacote atualizou corretamente o Diretório com o novo valor, simplesmente execute o pacote. Devido a serem copiados apenas três arquivos de dados de exemplo para o novo diretório, o fluxo de dados irá executar apenas três vezes ao invés de interagir com 14 arquivos da pasta original.  
  
## <a name="checking-the-package-layout"></a>Verificando o layout do pacote  
 Antes de testar o pacote, deve-se verificar se os fluxos de controle e de dados do pacote da Lição 5 contêm os objetos mostrados nos diagramas a seguir. O fluxo de controle deve ser idêntico ao fluxo de controle da Lição 4. O fluxo de dados deve ser idêntico ao fluxo de dados da lição 4.  
  
 **Fluxo de Controle**  
  
 ![Fluxo de controle no pacote](../../2014/tutorials/media/task4lesson2control.gif "Fluxo de controle no pacote")  
  
 **Fluxo de Dados**  
  
 ![Fluxo de dados no pacote](../../2014/tutorials/media/task9lesson1data.gif "Fluxo de dados no pacote")  
  
### <a name="to-test-the-lesson-5-tutorial-package"></a>Para testar o pacote de tutorial da Lição 5  
  
1.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
2.  Terminada a execução do pacote, no menu **Depurar** , clique em **Parar Depuração**.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 6: usar parâmetros com o modelo de implantação de projeto](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  