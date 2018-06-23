---
title: 'Como: exibir um relatório do Supervisor de atualização | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- displaying reports
- viewing reports
- Upgrade Advisor [SQL Server], reports
- SQL Server Upgrade Advisor, reports
- reports [Upgrade Advisor], viewing
ms.assetid: d13b38af-0ac3-4030-83cd-e7d7825dd09f
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b3617edd1d79e258490c0cc44fc3b21e012c4573
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011724"
---
# <a name="how-to-view-an-upgrade-advisor-report"></a>Como exibir um relatório do Supervisor de Atualização
  O Supervisor de Atualização cria relatórios para cada componente que você seleciona para analisar. Este tópico descreve como exibir esses relatórios na página inicial do Supervisor de Atualização.  
  
> [!IMPORTANT]  
>  O visualizador de relatórios carrega arquivos com base em nomes de arquivo padrão. Se os arquivos tiverem sido renomeados, o visualizador de relatórios não os carregará.  
  
### <a name="to-view-a-report"></a>Para exibir um relatório  
  
1.  Clique em **iniciar**, clique em **todos os programas**, clique em **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** e, em seguida, clique em  **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Supervisor de atualização**.  
  
2.  Na página inicial do Supervisor de atualização, clique em **iniciar o Visualizador de relatórios o Supervisor de atualização**.  
  
3.  Para selecionar um relatório no local padrão em seu computador:  
  
    1.  No **Server** lista, selecione um servidor.  
  
    2.  No **instância ou componente** , selecione uma combinação de componente ou instância do componente.  
  
     Para selecionar um relatório em outro local:  
  
    1.  Clique o **abrir relatório** link.  
  
    2.  Navegue até o local do relatório e clique duas vezes no arquivo XML.  
  
     O Supervisor de Atualização armazena até cinco relatórios da análise anterior como histórico. Para exibir esses relatórios, clique o **relatório** caixa de listagem suspensa e selecione um relatório. Os relatórios são listados pelo carimbo de data/hora de quando foram gerados.  
  
     O relatório contém os seguintes detalhes para todos os problemas detectados:  
  
    -   **Importância**, que indica o quão importante é corrigir o problema.  
  
    -   **Quando corrigir**, que indica se você deve (ou deve) solucionar o problema antes ou depois de atualizar para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], antes ou depois de migrar o aplicativo ou dados, ou a qualquer momento.  
  
    -   Uma descrição breve do problema.  
  
4.  Se o relatório tiver mais de 20 itens, clique na seta verde para frente, na parte superior ou inferior do relatório, para exibir o próximo conjunto de itens. Clique na seta verde para trás para exibir os 20 itens anteriores.  
  
5.  Para classificar o relatório, clique em um título de coluna.  
  
6.  Para exibir detalhes para um item específico, clique no item. Aparecerá uma descrição do problema, juntamente com opções adicionais:  
  
    -   Para exibir os objetos onde esse problema foi encontrado, clique em **Mostrar objetos afetados**.  
  
    -   Para exibir a Ajuda para o problema, clique em **mais informações sobre esse problema e como resolvê-lo**.  
  
    -   Para marcar o problema como solucionado, que oculta o problema quando você visualizar o relatório novamente, selecione **esse problema foi resolvido**.  
  
> [!NOTE]  
>  O relatório pode conter um item para problemas indetectáveis. Esses são os problemas que não podem ser detectados ou os que gerariam muitos resultados de falso positivo. Clique o **mais informações sobre esse problema e como resolvê-lo** link para ver uma lista dos problemas indetectáveis do componente.  
  
## <a name="see-also"></a>Consulte também  
 [Como: exportar relatórios](../../../2014/sql-server/install/how-to-export-reports.md)   
 [Como: executar o Assistente para análise do Supervisor de atualização](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Solucionando problemas de atualização](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Tópicos de instruções do Supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-how-to-topics.md)   
 [Trabalhando com o Supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  