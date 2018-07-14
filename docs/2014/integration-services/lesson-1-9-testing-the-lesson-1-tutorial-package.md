---
title: 'Etapa 9: testar o pacote de tutoriais da Lição 1 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f5dc22149aab9dfd9d458ed8cd4ec958794d973b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37193382"
---
# <a name="step-9-testing-the-lesson-1-tutorial-package"></a>Etapa 9: Testando o pacote de tutorial da Lição 1
  Nesta lição, você executou as seguintes tarefas:  
  
-   Criou um novo projeto do [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
-   Configurou os gerenciadores de conexões que o pacote precisa para estabelecer conexão com os dados de origem e de destino.  
  
-   Adicionou um fluxo de dados que usa os dados de uma origem de arquivo simples, desenvolve as transformações Pesquisa necessárias sobre os dados e configura os dados para o destino.  
  
 Seu pacote está completo agora! Está na hora de testá-lo.  
  
## <a name="checking-the-package-layout"></a>Verificando o layout do pacote  
 Antes de testar o pacote, é recomendável verificar se os fluxos de controle e de dados do pacote da Lição 1 contêm os objetos mostrados nos diagramas a seguir.  
  
 **Fluxo de Controle**  
  
 ![Fluxo de controle no pacote](../../2014/tutorials/media/task9lesson1control.gif "Fluxo de controle no pacote")  
  
 **Fluxo de Dados**  
  
 ![Fluxo de dados no pacote](../../2014/tutorials/media/task9lesson1data.gif "Fluxo de dados no pacote")  
  
### <a name="to-run-the-lesson-1-tutorial-package"></a>Para executar o pacote de tutorial da Lição 1  
  
1.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
     O pacote será executado, resultando em 1097 linhas adicionadas à tabela de fatos **FactCurrency** no **AdventureWorksDW2012**.  
  
2.  Terminada a execução do pacote, no menu **Depurar** , clique em **Parar Depuração**.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Adicionando loop](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>Consulte também  
 [Execução de projetos e pacotes](packages/run-integration-services-ssis-packages.md)  
  
  
