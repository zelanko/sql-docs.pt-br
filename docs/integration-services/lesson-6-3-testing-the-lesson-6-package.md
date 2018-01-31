---
title: "Etapa 3: testar o pacote da Lição 6 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: c184c92d-948f-4037-a502-5fabd909c84c
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d3127ba4edc47aa7ae9b6aab8fc309fe2c854da3
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="lesson-6-3---testing-the-lesson-6-package"></a>Lição 6-3 – testar o pacote da Lição 6
Em tempo de execução, seu pacote irá obter o valor para a propriedade Diretório a partir do parâmetro VarFolderName.  
  
Para verificar se, em tempo de execução, o pacote atualizou corretamente o Diretório com o novo valor, simplesmente execute o pacote. Devido a serem copiados apenas três arquivos de dados de exemplo para o novo diretório, o fluxo de dados irá executar apenas três vezes ao invés de interagir com 14 arquivos da pasta original.  
  
## <a name="checking-the-package-layout"></a>Verificando o layout do pacote  
Antes de testar o pacote deve-se verificar se os fluxos de controle e de dados do pacote da Lição 6 contêm os objetos mostrados nos diagramas a seguir. O fluxo de controle deve ser idêntico ao fluxo de controle da lição 5. O fluxo de dados deve ser idêntico ao fluxo de dados na lição 5.  
  
**Fluxo de Controle**  
  
![Fluxo de Controle](../integration-services/media/task3lesson6control.jpg "Fluxo de Controle")  
  
**Fluxo de Dados**  
  
![Fluxo de Dados](../integration-services/media/task3lesson6data.jpg "Fluxo de Dados")  
  
### <a name="to-test-the-lesson-6-tutorial-package"></a>Para testar o pacote de tutorial da Lição 6  
  
1.  No menu Depurar, clique em Iniciar Depuração.  
  
2.  Terminada a execução do pacote, no menu Depurar, clique em Parar Depuração.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Etapa 4: Implantando o pacote da Lição 6](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
  
  
