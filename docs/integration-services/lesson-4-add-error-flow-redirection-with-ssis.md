---
title: "Lição 4: Adicionar o redirecionamento de fluxo de erro com o SSIS | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 0c8dbda2-75e3-4278-9b4e-dcd220c92522
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cfe3634566a7ede28e3c1f5640cfe6e4caa1c351
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="lesson-4-add-error-flow-redirection-with-ssis"></a>Lição 4: Adicionar o redirecionamento de fluxo de erro com o SSIS
Para tratar erros que podem ocorrer no processo de transformação, o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece a capacidade de decidir, em termos de componente e coluna, como tratar dados que não podem ser transformados. Você pode escolher ignorar uma falha em determinadas colunas, redirecionar toda a linha com falha ou apenas causar falha no componente. Por padrão, todos os componentes no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] são configurados para falhar quando ocorrerem erros. Causar falha em um componente, por sua vez, faz com que o pacote falhe e todo o processamento subsequente pare.  
  
Em vez de permitir que as falhas interrompam a execução do pacote, é bom configurar e tratar erros de processamento em potencial conforme ocorrem dentro da transformação. Como você pode escolher ignorar as falhas para garantir que seu pacote seja executado com êxito, frequentemente é melhor redirecionar a linha com falhas para outro caminho de processamento, em que os dados e o erro podem ser persistentes, examinados e reprocessados posteriormente.  
  
Nesta lição, você aprenderá a criar uma cópia do pacote desenvolvido em [Lição 3: Adicionar o log com o SSIS](../integration-services/lesson-3-add-logging-with-ssis.md). Ao trabalhar com este pacote novo, você criará uma versão corrompida de um dos arquivos de dados de exemplo. O arquivo corrompido forçará a ocorrência de um erro de processamento quando você executar o pacote.  
  
Para tratar os dados de erro, você adicionará e configurará um destino de Arquivo Simples que gravará qualquer linha que não localize um valor de pesquisa na transformação Pesquisa de Códigos de Moeda em um arquivo.  
  
Antes que os dados de erro sejam gravados em um arquivo, você incluirá um componente Script que utiliza script para obter as descrições de erro. Você reconfigurará, então, a transformação Pesquisa de Códigos de Moeda para redirecionar qualquer dado que não possa ser processado para a transformação Script.  
  
> [!IMPORTANT]  
> Este tutorial requer o banco de dados de exemplo **AdventureWorksDW2012** . Para obter mais informações sobre como instalar e implantar o **AdventureWorksDW2012**, [Reporting Services Product Samples on CodePlex](http://go.microsoft.com/fwlink/p/?LinkID=526910)(Amostras de produto do Reporting Services no CodePlex)  
  
## <a name="tasks-in-lesson"></a>Tarefas da lição  
Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiando o pacote da lição 3](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
-   [Etapa 2: Criando um arquivo corrompido](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
-   [Etapa 3: Adicionando redirecionamento de fluxo de erro](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
-   [Etapa 4: Adicionando um destino de arquivo simples](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
-   [Etapa 5: Testando o pacote de Tutorial da lição 4](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
[Etapa 1: Copiando o pacote da lição 3](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
  
  

