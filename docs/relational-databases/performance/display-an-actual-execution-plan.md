---
title: Exibir um plano de execução real | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- displaying execution plans
- actual execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eaa3002837dd19335abcc8383612bcb31642265e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "78256862"
---
# <a name="display-an-actual-execution-plan"></a>Exibir um plano de execução real
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este tópico descreve como gerar planos de execução gráfica reais usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Os planos de execução reais são gerados depois que as consultas ou lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] são executados. Por isso, um plano de execução real contém informações de runtime, como avisos de runtime e métricas de uso real do recurso (se houver). O plano de execução gerado exibe o plano de execução de consulta real que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usou para executar as consultas.  
  
 Para usar esse recurso, os usuários devem ter as permissões apropriadas para executar as consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] para as quais um plano de execução gráfica está sendo gerado e eles devem ter a permissão SHOWPLAN para todos os bancos de dados referenciados pela consulta.  
  
## <a name="to-include-an-execution-plan-for-a-query-during-execution"></a>Para incluir um plano de execução para uma consulta durante a execução  
  
1.  Na barra de ferramentas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , clique em **Consulta do Mecanismo de Banco de Dados**. Você também pode abrir uma consulta existente e exibir o plano de execução estimado clicando no botão de barra de ferramentas **Abrir Arquivo** e localizando a consulta existente. 
  
2.  Insira a consulta para a qual você deseja exibir o plano de execução real.  
  
3.  No menu **Consulta**, clique em **Incluir Plano de Execução Real** ou clique no botão de barra de ferramentas **Incluir Plano de Execução Real**.

    ![Botão Plano de Execução Real na barra de ferramentas](../../relational-databases/performance/media/actualexecplantoolbar.png "Botão Plano de Execução Real na barra de ferramentas")   
  
4.  Execute a consulta clicando no botão de barra de ferramentas **Executar** . O plano usado pelo otimizador de consulta é exibido na guia **Plano de Execução** no painel de resultados. 

    ![Plano de Execução Real](../../relational-databases/performance/media/actualexecplan.png "Plano de Execução Real")   

5.  Coloque o mouse sobre os operadores lógicos e físicos para exibir a descrição e as propriedades dos operadores na Dica de Ferramenta exibida, incluindo propriedades do plano de execução geral, selecionando o operador de nó raiz (o nó SELECT na imagem acima).   
  
    Você também pode exibir propriedades do operador na janela Propriedades. Se a janela Propriedades não estiver visível, clique com o botão direito do mouse em um operador e clique em **Propriedades**. Selecione um operador cujas propriedades exibir.  

    ![Clicar com o botão direito do mouse em Propriedades no operador de plano](../../relational-databases/performance/media/planproperties.png "Clicar com o botão direito do mouse em Propriedades no operador de plano")    
  
6.  Você pode alterar a exibição do plano de execução clicando com o botão direito no plano de execução e selecionando **Ampliar**, **Reduzir**, **Zoom Personalizado**ou **Ajustar Nível de Zoom**. **Ampliar** e **Reduzir** permitem ampliar ou reduzir o plano de execução, enquanto **Zoom Personalizado** permite definir seu próprio zoom, como ampliar em 80 por cento. **Ajustar Nível de Zoom** aumenta o plano de execução para se ajustar ao painel de resultados. Como alternativa, use a tecla CTRL e o botão de rolagem do mouse para ativar o **zoom dinâmico**.  

7.  Para navegar na exibição do plano de execução, use as barras de rolagem vertical e horizontal ou **clique e segure em qualquer área em branco** do plano de execução e **arraste o mouse**. Como alternativa, clique e segure o sinal de adição (+) no canto inferior direito da janela de plano de execução para exibir um mapa em miniatura de todo o plano de execução.

> [!NOTE] 
> Como alternativa, use [SET STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md) para retornar informações do plano de execução para cada instrução depois de executá-las. Se usada em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], a guia *Resultados* terá um link para abrir o plano de execução em formato gráfico.   
> Para obter mais informações, confira [Infraestrutura de Criação de Perfil de Consulta](../../relational-databases/performance/query-profiling-infrastructure.md).
  
## <a name="see-also"></a>Consulte Também  
 [Planos de execução](../../relational-databases/performance/execution-plans.md)    
 [Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md)  
