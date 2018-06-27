---
title: 'Lição 4: Adicionar o redirecionamento de fluxo de erro com o SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
ms.assetid: 0c8dbda2-75e3-4278-9b4e-dcd220c92522
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 381d7b5d80281832081a7a08defbd0b3cb76dda5
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35408858"
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
  
-   [Etapa 1: Copiando o pacote da Lição 3](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
-   [Etapa 2: Criando um arquivo corrompido](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
-   [Etapa 3: Adicionando redirecionamento de fluxo de erro](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
-   [Etapa 4: Adicionando um destino de arquivo simples](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
-   [Etapa 5: Testando o pacote de tutorial da Lição 4](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
[Etapa 1: Copiando o pacote da Lição 3](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
  
  
