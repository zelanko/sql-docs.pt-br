---
title: Transformação Distribuidor de Dados Equilibrado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.balanceddatadistributor.f1
ms.assetid: ae0b33dd-f44b-42df-b6f6-69861770ce10
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ec61ee62bf952e64e746ae132ce6ee35c89d468a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62770584"
---
# <a name="balanced-data-distributor-transformation"></a>Transformação de BDD (Balanced Data Distributor)
  A transformação de BDD (Balanced Data Distributor) aproveita o recurso de processamento simultâneo de CPUs modernas. Ela distribui buffers de linhas de entrada uniformemente em saídas em threads separados. Usando threads separados para cada caminho de saída, o componente de BDD melhora o desempenho de um pacote SSIS em computadores de vários núcleos ou de vários processadores. O componente de BDD faz parte do Feature Pack do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Baixe-o e instale-o de [aqui](https://go.microsoft.com/fwlink/p/?LinkId=391999).  
  
 O diagrama a seguir mostra um exemplo simples de como usar a transformação de BDD. Neste exemplo, a transformação de BDD escolhe um buffer de pipeline de cada vez a partir dos dados de entrada de uma fonte de arquivo simples, e envia-o a um dos três caminhos de saída em uma forma round robin. No SQL Server Data Tools, você pode verificar os valores de um <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.DefaultBufferSize%2A>(tamanho padrão do buffer de pipeline) e <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.DefaultBufferMaxRows%2A>(número máximo de linhas padrão em um buffer de pipeline) na janela **Propriedades** que exibe as propriedades de uma tarefa de fluxo de dados.  
  
 ![Distribuidor de Dados Equilibrado](../../media/balanceddatadistributor.JPG "Distribuidor de Dados Equilibrado")  
  
 A transformação de BDD ajuda a melhorar o desempenho de um pacote em um cenário que satisfaça as seguintes condições:  
  
1.  Há uma grande quantidade de dados que entram na transformação de BDD. Se o tamanho dos dados é pequeno e somente um buffer pode manter os dados, não faz sentido usar a transformação de BDD. Se o tamanho dos dados for grande e vários buffers forem necessários para manter os dados, o BDD poderá processar com eficácia buffers de dados em paralelo usando threads separados.  
  
2.  Os dados podem ser lidos mais rápido do que o restante do fluxo de dados pode processá-los. Nesse cenário, as transformações que são executadas nos dados ocorrem lentamente comparado à taxa de entrada dos dados. Se o gargalo está no destino, o destino deve ser paralelizável.  
  
3.  Os dados não precisam ser ordenados. Por exemplo, se os dados precisam ser classificados, você não deve dividi-los usando a transformação de BDD.  
  
 Observe que, se o gargalo em um pacote SSIS for devido à taxa na qual os dados podem ser lidos da origem, o componente de BDD não ajudará a melhorar o desempenho. Se a causa do gargalo em um pacote SSIS for a falta de suporte do destino ao paralelismo, o BDD não ajudará; porém, você pode executar todas as transformações em paralelo e usar a transformação Union All para combinar os dados de saída provenientes de diferentes caminhos da saída da transformação de BDD antes de enviar os dados para o destino.  
  
> [!IMPORTANT]  
>  Consulte o vídeo [Balanced Data Distributor](https://go.microsoft.com/fwlink/?LinkID=226278) na biblioteca do TechNet para obter uma apresentação com uma demonstração sobre o uso da transformação.  
  
  
