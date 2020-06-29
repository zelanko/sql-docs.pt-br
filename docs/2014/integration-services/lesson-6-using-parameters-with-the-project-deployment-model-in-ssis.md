---
title: 'Lição 6: usando parâmetros com o modelo de implantação de projeto | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 357fe65ef7b269d775b5cabbb2a17ec3a075acae
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440303"
---
# <a name="lesson-6-using-parameters-with-the-project-deployment-model"></a>Lição 6: Como usar parâmetros com o modelo de implantação de projeto
  O SQL Server 2012 apresenta um novo modelo de implantação em que você pode implantar seus projetos no servidor do Integration Services. O servidor do Integration Services permite gerenciar e executar pacotes e configurar valores de runtime para pacotes.  
  
 Nesta lição, você modificará o pacote criado no [Lesson 5: Adding Package Configurations for the Package Deployment Model](lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md) para usar o Modelo de Implantação do Projeto. Você substitui o valor de configuração com um parâmetro para especificar o local de dados de exemplo. Você também pode copiar o pacote concluído da Lição 5 que está incluso no tutorial.  
  
 Usando o Assistente de Configuração de Projeto do Integration Services, você converterá o projeto no Modelo de Implantação do Projeto e usará um parâmetro, em vez de um valor de configuração, para definir a propriedade do Diretório. Esta lição abrange parcialmente as etapas que você seguirá para converter os pacotes SSIS existentes no novo Modelo de Implantação do Projeto.  
  
 Quando você executar o pacote novamente, o serviço Integration Services usará o parâmetro para popular o valor da variável e, por sua vez, a variável atualizará a propriedade Diretório. Assim, o pacote itera pelos arquivos na nova pasta de dados especificada pelo valor de parâmetro, em vez da pasta que foi definida no arquivo de configuração do pacote.  
  
> [!IMPORTANT]  
>  Este tutorial requer o banco de dados de exemplo **AdventureWorksDW2012** . Para obter mais informações sobre como instalar e implantar o **AdventureWorksDW2012**, consulte [Considerações sobre a instalação de amostras e bancos de dados de exemplo do SQL Server](https://technet.microsoft.com/library/ms161556%28v=sql.105%29).  
  
## <a name="lesson-tasks"></a>Tarefas da lição  
 Esta lição contém as seguintes tarefas:  
  
1.  [Etapa 1: Copiar o pacote da Lição 5](lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [Etapa 2: Convertendo o projeto para o modelo de implantação de projeto](lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [Etapa 3: Testar o pacote da Lição 6](lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [Etapa 4: Implantar o pacote da Lição 6](lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
 [Etapa 1: Copiar o pacote da Lição 5](lesson-6-1-copying-the-lesson-5-package.md)  
  
  
