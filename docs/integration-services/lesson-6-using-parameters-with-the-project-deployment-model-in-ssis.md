---
title: 'Lição 6: Usar parâmetros com o modelo de implantação de projetos no SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b9ebfb17a69abbaf8482999d3435bbdea11e0822
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58289892"
---
# <a name="lesson-6-use-parameters-with-the-project-deployment-model-in-ssis"></a>Lição 6: Usar parâmetros com o modelo de implantação de projetos no SSIS

O SQL Server 2012 trouxe um novo modelo de implantação em que você pode implantar seus projetos no servidor do Integration Services. O servidor do Integration Services permite gerenciar e executar pacotes e configurar valores de tempo de execução para pacotes.  
  
Nesta lição, você modificará o pacote criado na [Lição 5: Adicione configurações de pacote do SSIS para o Modelo de Implantação de Pacote](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md) para usar o Modelo de Implantação do Projeto. Você substitui o valor de configuração com um parâmetro para especificar o local de dados de exemplo. Você também pode copiar o pacote concluído da Lição 5 que está incluso no tutorial.  
  
Ao usar o Assistente de Configuração de Projeto do Integration Services, você converte o projeto no Modelo de Implantação do Projeto. Esse modelo usa um parâmetro em vez de um valor de configuração para definir a propriedade Directory. Esta lição abrange parcialmente as etapas que você seguirá para converter os pacotes SSIS existentes no novo Modelo de Implantação do Projeto.  
  
Quando você executa o pacote novamente, o servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usa o parâmetro para preencher o valor da variável. Por sua vez, a variável atualiza a propriedade Directory. O pacote itera pelos arquivos na pasta de dados especificada pelo parâmetro de novo.  
  
> [!NOTE]
> Se você ainda não fez isso, confira os [Pré-requisitos da Lição 1](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).
    
## <a name="lesson-tasks"></a>Tarefas da lição  
Esta lição contém as seguintes tarefas:  
  
1.  [Etapa 1: Copiar o pacote da Lição 5](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [Etapa 2: Converter o projeto no Modelo de Implantação de Projeto](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [Etapa 3: Testar o pacote da Lição 6](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [Etapa 4: Implantar o pacote da Lição 6](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
[Etapa 1: Copiar o pacote da Lição 5](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
