---
title: Como exibir um relatório do supervisor de atualização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- viewing reports
- Upgrade Advisor [SQL Server], reports
- SQL Server Upgrade Advisor, reports
- reports [Upgrade Advisor], viewing
ms.assetid: d13b38af-0ac3-4030-83cd-e7d7825dd09f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0ae231e380530f11d4c97a917927ed62e99fb47
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094801"
---
# <a name="how-to-view-an-upgrade-advisor-report"></a>Como fazer: Para exibir um relatório do Supervisor de Atualização
  O Supervisor de Atualização cria relatórios para cada componente que você seleciona para analisar. Este tópico descreve como exibir esses relatórios na página inicial do Supervisor de Atualização.  
  
> [!IMPORTANT]  
>  O visualizador de relatórios carrega arquivos com base em nomes de arquivo padrão. Se os arquivos tiverem sido renomeados, o visualizador de relatórios não os carregará.  
  
### <a name="to-view-a-report"></a>Para exibir um relatório  
  
1.  Clique em **Iniciar**, em **todos os programas**, em **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** e em ** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] supervisor de atualização**.  
  
2.  Na página inicial do supervisor de atualização, clique em **Iniciar Visualizador de relatórios do supervisor de atualização**.  
  
3.  Para selecionar um relatório no local padrão em seu computador:  
  
    1.  Na lista **servidor** , selecione um servidor.  
  
    2.  Na lista de **instância ou componente** , selecione uma combinação de componente ou componente/instância.  
  
     Para selecionar um relatório em outro local:  
  
    1.  Clique no link **abrir relatório** .  
  
    2.  Navegue até o local do relatório e clique duas vezes no arquivo XML.  
  
     O Supervisor de Atualização armazena até cinco relatórios da análise anterior como histórico. Para exibir esses relatórios, clique na caixa de listagem suspensa **relatório** e selecione um relatório. Os relatórios são listados pelo carimbo de data/hora de quando foram gerados.  
  
     O relatório contém os seguintes detalhes para todos os problemas detectados:  
  
    -   **Importância**, que indica quão importante é corrigir o problema.  
  
    -   **Quando corrigir**, o que indica se você deve (ou deve) corrigir o problema antes ou depois de atualizar [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]para o, antes ou depois de migrar o aplicativo ou os dados, ou a qualquer momento.  
  
    -   Uma descrição breve do problema.  
  
4.  Se o relatório tiver mais de 20 itens, clique na seta verde para frente, na parte superior ou inferior do relatório, para exibir o próximo conjunto de itens. Clique na seta verde para trás para exibir os 20 itens anteriores.  
  
5.  Para classificar o relatório, clique em um título de coluna.  
  
6.  Para exibir detalhes para um item específico, clique no item. Aparecerá uma descrição do problema, juntamente com opções adicionais:  
  
    -   Para exibir os objetos em que esse problema foi encontrado, clique em **Mostrar objetos afetados**.  
  
    -   Para exibir a ajuda do problema, clique em **mais informações sobre esse problema e como resolvê-lo**.  
  
    -   Para marcar o problema como resolvido, que oculta o problema quando você exibe o relatório novamente, selecione **esse problema foi resolvido**.  
  
> [!NOTE]  
>  O relatório pode conter um item para problemas indetectáveis. Esses são os problemas que não podem ser detectados ou os que gerariam muitos resultados de falso positivo. Clique no link **mais informações sobre esse problema e como resolvê-lo** para ver uma lista de problemas não detectáveis do componente.  
  
## <a name="see-also"></a>Consulte Também  
 [Como: exportar relatórios](../../../2014/sql-server/install/how-to-export-reports.md)   
 [Como executar o assistente de análise do supervisor de atualização](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Resolvendo problemas de atualização](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Tópicos de instruções do supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-how-to-topics.md)   
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
