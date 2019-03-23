---
title: Depurando o fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- progress reporting [Integration Services]
- data viewers [Integration Services]
- data flow [Integration Services], debugging
- debugging [Integration Services], data flow
- counting rows
ms.assetid: 1c574f1b-54f7-4c05-8e42-8620e2c1df0f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fdfaeeb9e8dafe82a1312593df2dd128635b8365
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58391074"
---
# <a name="debugging-data-flow"></a>Depurando fluxo de dados
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e o Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] incluem recursos e ferramentas que você pode usar para solucionar problemas de fluxos de dados em um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] O Designer fornece visualizadores de dados.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] O Designer e as transformações do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornecem contagens de linha.  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] fornece relatórios de progresso em tempo de execução.  
  
## <a name="data-viewers"></a>Visualizadores de dados  
 Os visualizadores de dados exibem dados entre dois componentes em um fluxo de dados. Os visualizadores de dados podem exibir dados quando os dados são extraídos de uma fonte de dados e entram primeiro um fluxo de dados, antes e depois de uma transformação atualizar os dados, e antes dos dados serem carregados em seu destino.  
  
 Para visualizar os dados, você anexa os visualizadores de dados ao caminho que conecta dois componentes de fluxo de dados. A habilidade de visualizar os dados entre componentes de fluxo de dados, facilita a identificação de valores de dados inesperados, a visualização de como uma transformação altera os valores das colunas, e a descoberta da razão pela qual uma transformação falha. Por exemplo, você pode descobrir uma falha na pesquisa em uma tabela de referência e, para corrigir isso, você pode desejar adicionar uma transformação que forneça dados padrão para colunas em branco.  
  
 Um visualizador de dados pode exibir dados em uma grade. Ao usar uma grade, você seleciona as colunas a serem exibidas. Os valores das colunas selecionadas são exibidos em um formato tabular.  
  
 Você também pode incluir vários visualizadores de dados em um caminho. Você pode exibir os mesmos dados em diferentes formatos, por exemplo, criar uma exibição de gráfico e uma exibição de grade dos dados, ou criar visualizadores de dados para diferentes colunas de dados.  
  
 Quando você adiciona um visualizador de dados a um caminho, o Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] adiciona um ícone de visualização de dados à superfície de design da guia **Fluxo de Dados** , ao lado do caminho. As transformações que podem tem múltiplas saídas, tais como as transformações Divisão Condicional, podem incluir um visualizador em cada caminho.  
  
 Em tempo de execução, uma janela **Visualizador de Dados** é aberta e exibe as informações especificadas pelo formato do visualizador de dados. Por exemplo, um visualizador de dados que utiliza o formato de grade exibe os dados das colunas selecionadas, o número de linhas de saída transmitidas ao componente de fluxo de dados e o número de linhas exibidas. As informações exibem buffer por buffer e, dependendo da largura das linhas no fluxo de dados, um buffer pode conter mais ou menos linhas.  
  
 Na caixa de diálogo **Visualizador de Dados** , você pode copiar os dados para a Área de Transferência, limpar todos os dados da tabela, configurar novamente o visualizador de dados, retomar o fluxo de dados e desanexar ou anexar o visualizador de dados.  
  
#### <a name="to-add-a-data-viewer"></a>Para adicionar um visualizador de dados  
  
-   [Adicionar um visualizador de dados a um fluxo de dados](../add-a-data-viewer-to-a-data-flow.md)  
  
## <a name="row-counts"></a>Contagens de linhas  
 O número de linhas que passaram por um caminho é exibido na superfície de design da guia **Fluxo de Dados** no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , ao lado do caminho. O número é atualizado periodicamente enquanto os dados se movimentam pelo caminho.  
  
 Você também pode adicionar uma transformação Contagem de Linhas ao fluxo de dados para capturar a contagem final de linhas em uma variável. Para obter mais informações, consulte [Row Count Transformation](../data-flow/transformations/row-count-transformation.md).  
  
## <a name="progress-reporting"></a>Relatório de progresso  
 Quando você executa um pacote, o Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] descreve o progresso na superfície de design da guia **Fluxo de Dados** , exibindo cada componente de fluxo de dados em uma cor que indica seu status. Quando cada componente começa a executar sua função, ele muda para a cor amarelo, e quando ele termina com sucesso, sua cor muda para verde. A cor vermelha indica que o componente falhou.  
  
 A tabela a seguir descreve a codificação de cores.  
  
|Cor|Descrição|  
|-----------|-----------------|  
|Nenhuma cor|Esperando ser chamado pelo mecanismo de fluxo de dados.|  
|Amarelo|Executando uma transformação, extraindo dados ou carregando dados.|  
|Verde|Executado com êxito.|  
|vermelha|Executado com erros.|  
  
## <a name="see-also"></a>Consulte também  
 [Solucionando problemas de ferramentas para desenvolvimento de pacotes](troubleshooting-tools-for-package-development.md)  
  
  
