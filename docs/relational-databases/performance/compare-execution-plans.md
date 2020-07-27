---
title: Comparar planos de execução | Microsoft Docs
description: Saiba como comparar as semelhanças e as diferenças entre planos de execução gráficos reais usando o recurso de Comparação de Plano SQL Server Management Studio.
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- comparing execution plans
- compare execution plans
- plan comparison
- execution plans [SQL Server], comparing
- Query Store, comparing plans
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 855d893ddde9c3eba9f9197c510ed0d03bc658ce
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457362"
---
# <a name="compare-execution-plans"></a>Comparar planos de execução
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
Este tópico descreve como comparar as semelhanças e as diferenças entre os planos de execução gráficos reais usando o recurso de Comparação de Plano [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Este recurso está disponível a partir do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v16.
  
> [!NOTE]
> Os planos de execução reais são gerados depois que as consultas ou lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] são executados. Por isso, um plano de execução real contém informações de runtime, como número real de linhas, métricas de uso de recursos e avisos de runtime (se houver). Para obter mais informações, confira [Exibir um plano de execução real](../../relational-databases/performance/display-an-actual-execution-plan.md).
  
A capacidade de comparar os planos é algo que os profissionais de banco de dados podem precisar fazer para solucionar problemas:
-   Saiba por que uma consulta ou lote de repente fica lento.
-   Entenda o impacto de reescrever uma consulta.
-   Observe como uma alteração de aprimoramento de desempenho específica introduzida no design de esquema (como um novo índice) mudou efetivamente o plano de execução.  
 
O menu **Comparação de Plano** permite a comparação lado a lado de dois planos de execução diferentes para facilitar a identificação de semelhanças e alterações que explicam os comportamentos diferentes por todas as razões declaradas acima. Essa opção pode comparar entre:
- Dois arquivos de plano de execução (extensão *sqlplan*) salvos anteriormente.
- Um plano de execução ativo um plano de execução de consulta salvo anteriormente.
- Dois planos de consulta selecionados em [Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).

> [!TIP]
> A Comparação de Plano funciona com qualquer arquivo *sqlplan*, até mesmo de versões mais antigas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Além disso, essa opção permite comparação offline, portanto, não é necessário estar conectado a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

Quando dois planos de execução são comparados, regiões do plano que **fazem essencialmente a mesma ação** são realçadas na mesma cor e padrão. Clicar em uma região colorida em um plano centralizará o outro plano no nó correspondente naquele plano. Você ainda pode comparar operadores não correspondentes e nós dos planos de execução, porém, nesse caso, deverá selecionar manualmente os operadores a serem comparados.

> [!IMPORTANT]
> Somente nós considerados como alterando a forma do plano são usados para verificar se há semelhanças. Portanto, pode haver um nó que não esteja colorido no meio de dois nós que estejam na mesma subseção do plano. Nesse caso, a falta de cor implica que os nós não foram considerados durante a verificação se as seções eram iguais.
  
## <a name="to-compare-execution-plans"></a>Para comparar planos de execução
  
1.  Abra um arquivo de plano de execução de consulta salvo anteriormente (.sqlplan) usando o menu **Arquivo** e clicando em **Abrir Arquivo** ou arraste um arquivo de plano para a janela [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]. Como alternativa, se você tiver acabado de executar uma consulta e optar por exibir seu plano de execução, vá para a guia **Plano de Execução** guia no painel de resultados. 

2.  Clique com o botão direito do mouse em uma área em branco do plano de execução e clique em **Comparar plano de execução**. 

    ![Clique com o botão direito do mouse em Comparar Plano de Execução](../../relational-databases/performance/media/plancomparisonmenuoption.png "Clique com o botão direito do mouse em Comparar Plano de Execução")   

3.  Escolha o segundo arquivo de plano de consulta com o qual você deseja comparar. O segundo arquivo será aberto para que você possa comparar os planos.

4.  Os planos comparados abrirão uma nova janela, por padrão, estando uma na parte superior e outra na parte inferior. A seleção padrão será a primeira ocorrência de um operador ou nó em comum nos planos comparados, mas o mostrando as diferenças entre os planos. Todos os operadores e nós realçados existem em ambos os planos comparados. Selecionar um operador realçado no plano superior ou esquerdo automaticamente seleciona o operador correspondente no plano inferior ou direito. Selecionar operador raiz do nó em qualquer um dos planos comparados (o nó SELECT na imagem abaixo) também seleciona o operador de nó raiz respectivo no outro plano comparado.

    ![Planejar a comparação entre dois arquivos de plano salvos](../../relational-databases/performance/media/plancomparison-plans.png "Planejar a comparação entre dois arquivos de plano salvos")  

     > [!TIP]
     > Você pode alternar a exibição da comparação de plano de execução para lado a lado clicando com o botão direito do mouse em uma área em branco do plano de execução e selecionando **Alternar Orientação do Divisor**.

     > [!TIP]
     > Todas as opções de zoom e navegação disponíveis para planos de execução funcionam no modo de comparação do plano. Para obter mais detalhes, confira [Exibir um plano de execução real](../../relational-databases/performance/display-an-actual-execution-plan.md).

5.  Também é aberta uma janela Propriedades dupla à direita no escopo da seleção padrão. As propriedades que existem em ambos os operadores comparados, mas que apresentem diferenças, serão precedidas pelo sinal *diferente de* (&ne;) para facilitar a identificação.

    ![Janela de propriedades duplas](../../relational-databases/performance/media/plancomparison-properties.png "Janela de propriedades duplas")  

6.  A janela de navegação de comparação **Análise de Plano de Execução** também abre na parte inferior. Há três guias disponíveis:

    1.  Na guia **Opções da Instrução**, a seleção padrão é *Realçar operações semelhantes* e o mesmo operador ou nó realçado em planos comparados compartilham o mesmo padrão de cor e linha. Navegue entre áreas semelhantes em planos comparados clicando em um padrão verde-limão. Você também pode optar por realçar as diferenças entre os planos, em vez das semelhanças, selecionando *Realçar operações que não correspondem aos segmentos semelhantes*. 
    
       > [!NOTE]
       > Por padrão, os nomes de banco de dados são ignorados durante a comparação de planos para permitir a comparação de planos capturados para bancos de dados que têm nomes diferentes, mas compartilham do mesmo esquema. Por exemplo, ao comparar os planos de bancos de dados *ProdDB* e *TestDB*. Esse comportamento pode ser alterado com a opção *Ignorar nome do banco de dados ao comparar operadores*.

       ![Janela de Análise de Plano de Execução](../../relational-databases/performance/media/plancomparison-analysis.png "Janela de Análise de Plano de Execução") 

    2.  A guia **Várias Instruções** é útil ao comparar planos com várias instruções, permitindo que o par de instruções certo seja comparado.

        ![Várias instruções em plano comparado](../../relational-databases/performance/media/plancomparison-multiple.png "Várias instruções em plano comparado")  

    3.  Na guia **Cenários**, você pode encontrar uma análise automatizada de alguns dos aspectos mais relevantes para analisar no sentido de como se relacionada a diferenças de [Estimativa de Cardinalidade](../../relational-databases/performance/cardinality-estimation-sql-server.md) em planos comparados. Para cada operador listado no painel esquerdo, o painel direito mostra detalhes sobre o cenário no link *Clique aqui para obter mais informações sobre esse cenário* e possíveis razões para explicar esse cenário são listadas. 

        ![Linhas estimadas diferentes](../../relational-databases/performance/media/plancomparison-scenarios.png "Linhas estimadas diferentes")  

    Se esta janela for fechada, clique com o botão direito do mouse em uma área em branco de um plano comparado e selecione **Opções de Comparação de Plano de Execução** para reabrir.

    ![Opções de comparação de plano](../../relational-databases/performance/media/plancomparison-options.png "Opções de comparação de plano")  

## <a name="to-compare-execution-plans-in-query-store"></a>Para comparar os planos de execução no Repositório de Consultas

1.  No Repositório de Consultas, identifique uma consulta que tenha mais de um plano de execução. Para obter mais informações sobre cenários do Repositório de Consultas, confira [Cenários de uso do Repositório de Consultas](../../relational-databases/performance/query-store-usage-scenarios.md#identify-and-tune-top-resource-consuming-queries).

2.  Use uma combinação da tecla SHIFT e do mouse para selecionar dois planos para a mesma consulta. 

    ![Selecione dois planos no Repositório de Consultas](../../relational-databases/performance/media/plancomparison-querystore.png "Selecione dois planos no Repositório de Consultas")   

3.  Use o botão **Comparar planos para a consulta de seleção em uma janela separada** para iniciar a comparação de planos. Em seguida, as etapas 4 a 6 *Para comparar os planos de execução* são aplicáveis. 

    ![Comparar Plano de Execução no Repositório de Consultas](../../relational-databases/performance/media/plancomparison-querystoreoption.png "Comparar Plano de Execução no Repositório de Consultas") 
