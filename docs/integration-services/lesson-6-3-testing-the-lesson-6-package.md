---
description: 'Lição 6-3: Testar o pacote da Lição 6'
title: 'Etapa 3: Testar o pacote da Lição 6 | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: c184c92d-948f-4037-a502-5fabd909c84c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6fc7b150f94d0f857244587140fd54b8fe7d38c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487707"
---
# <a name="lesson-6-3-test-the-lesson-6-package"></a>Lição 6-3: Testar o pacote da Lição 6

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


Em tempo de execução, seu pacote obtém o valor para a propriedade **Directory** do parâmetro **VarFolderName**.  
  
Para verificar se o pacote atualiza a propriedade **Directory**, execute o pacote. Uma vez que você copiou os três arquivos de dados de exemplo para o novo diretório, o fluxo de dados é executado três vezes.
  
## <a name="check-the-package-layout"></a>Verificar o layout do pacote  
Antes de testar o pacote, verifique se os fluxos de controle e de dados do pacote da Lição 6 são similares aos objetos mostrados nos diagramas a seguir:   
  
**Fluxo de Controle**  
  
![Fluxo de Controle](../integration-services/media/task4lesson2control.gif "Fluxo de Controle")  
  
**Fluxo de Dados**  
  
![Fluxo de Dados](../integration-services/media/task5lesson5data.gif "Fluxo de Dados")  
  
## <a name="test-the-lesson-6-package"></a>Testar o pacote da Lição 6  
  
1.  No menu **Depurar**, selecione **Iniciar Depuração**.  
  
2.  Terminada a execução do pacote, no menu **Depurar**, selecione **Parar Depuração**.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 4: Implantar o pacote da Lição 6](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
  
  
