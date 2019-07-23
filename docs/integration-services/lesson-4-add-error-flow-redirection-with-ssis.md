---
title: 'Lição 4: Adicionar o redirecionamento de fluxo de erro com o SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0c8dbda2-75e3-4278-9b4e-dcd220c92522
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3ad643a65eb83b1593b21782ad9784d5062c3899
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055763"
---
# <a name="lesson-4-add-error-flow-redirection-with-ssis"></a>Lição 4: Adicionar o redirecionamento de fluxo de erro com o SSIS

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Para tratar erros que podem ocorrer no processo de transformação, o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] permite que você decida por componente e por coluna como tratar dados que o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] não pode transformar. Você pode escolher ignorar uma falha em determinadas colunas, redirecionar toda a linha com falha ou causar falha no componente. Por padrão, os componentes no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] são configurados para falhar quando ocorrerem erros. O componente com falha, por sua vez, faz com que o pacote falhe o processamento seja interrompido.  
  
Em vez de permitir que as falhas interrompam a execução do pacote, você pode configurar e tratar possíveis erros de processamento potenciais conforme eles ocorrem. Uma opção é ignorar as falhas por completo de modo que seu pacote sempre seja executado com êxito. Você também pode redirecionar a linha com falha para outro caminho de processamento em que os dados e os erros possam ser mantidos, examinados ou reprocessados.  
  
Nesta lição, você cria uma cópia do pacote desenvolvido em [Lição 3: Adicionar o registro em log com o SSIS](../integration-services/lesson-3-add-logging-with-ssis.md). Ao trabalhar com este pacote novo, você cria uma versão corrompida de um dos arquivos de dados de exemplo. O arquivo corrompido levará à ocorrência de um erro de processamento quando você executar o pacote.  
  
Para lidar com os dados de erro, você pode adicionar e configurar um destino de arquivo simples que grava linhas com falha em um arquivo de erro. 
  
Antes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] gravar dados de erros no arquivo, você inclui um componente de Script que obtém as descrições de erro. Você então reconfigura então a transformação Pesquisar Chave de Moeda para redirecionar qualquer dado que não possa ser processado para a transformação Script.  
  
## <a name="prerequisites"></a>Prerequisites

> [!NOTE]
> Se você ainda não fez isso, confira a [Lição 1 Pré-requisitos](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).
 
## <a name="lesson-task"></a>Tarefa da lição
Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiar o pacote da Lição 3](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
-   [Etapa 2: Criar um arquivo corrompido](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
-   [Etapa 3: Adicionar redirecionamento de fluxo de erro](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
-   [Etapa 4: Adicionar um destino de Arquivo Simples](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
-   [Etapa 5: Testar o pacote de tutorial da Lição 4](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
[Etapa 1: Copiar o pacote da Lição 3](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
  
  
