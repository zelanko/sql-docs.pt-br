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
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- viewing reports
- Upgrade Advisor [SQL Server], reports
- SQL Server Upgrade Advisor, reports
- reports [Upgrade Advisor], viewing
ms.assetid: d13b38af-0ac3-4030-83cd-e7d7825dd09f
caps.latest.revision: 32
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: df6d91d700182c7d3828d9e35ac61cfaa0b3959d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37303576"
---
# <a name="how-to-view-an-upgrade-advisor-report"></a>Como exibir um relatório do Supervisor de Atualização
  O Supervisor de Atualização cria relatórios para cada componente que você seleciona para analisar. Este tópico descreve como exibir esses relatórios na página inicial do Supervisor de Atualização.  
  
> [!IMPORTANT]  
>  O visualizador de relatórios carrega arquivos com base em nomes de arquivo padrão. Se os arquivos tiverem sido renomeados, o visualizador de relatórios não os carregará.  
  
### <a name="to-view-a-report"></a>Para exibir um relatório  
  
1.  Clique em **inicie**, clique em **todos os programas**, clique em **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** e, em seguida, clique em  **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Supervisor de atualização**.  
  
2.  Na página inicial do Supervisor de atualização, clique em **iniciar o Visualizador de relatórios de Supervisor de atualização**.  
  
3.  Para selecionar um relatório no local padrão em seu computador:  
  
    1.  No **Server** , selecione um servidor.  
  
    2.  No **instância ou componente** , selecione uma combinação de componente ou instância do componente.  
  
     Para selecionar um relatório em outro local:  
  
    1.  Clique o **abrir relatório** link.  
  
    2.  Navegue até o local do relatório e clique duas vezes no arquivo XML.  
  
     O Supervisor de Atualização armazena até cinco relatórios da análise anterior como histórico. Para exibir esses relatórios, clique o **relatório** caixa de lista suspensa e selecione um relatório. Os relatórios são listados pelo carimbo de data/hora de quando foram gerados.  
  
     O relatório contém os seguintes detalhes para todos os problemas detectados:  
  
    -   **Importância**, que indica o quanto é importante corrigir o problema.  
  
    -   **Quando corrigir**, que indica se você deve (ou deve) solucionar o problema antes ou após a atualização para [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], antes ou depois de migrar o aplicativo ou dados, ou a qualquer momento.  
  
    -   Uma descrição breve do problema.  
  
4.  Se o relatório tiver mais de 20 itens, clique na seta verde para frente, na parte superior ou inferior do relatório, para exibir o próximo conjunto de itens. Clique na seta verde para trás para exibir os 20 itens anteriores.  
  
5.  Para classificar o relatório, clique em um título de coluna.  
  
6.  Para exibir detalhes para um item específico, clique no item. Aparecerá uma descrição do problema, juntamente com opções adicionais:  
  
    -   Para exibir os objetos em que esse problema foi encontrado, clique em **Mostrar objetos afetados**.  
  
    -   Para exibir a Ajuda para o problema, clique em **mais informações sobre esse problema e como resolvê-lo**.  
  
    -   Para marcar o problema como solucionado, que oculta o problema quando você visualizar o relatório novamente, selecione **esse problema foi resolvido**.  
  
> [!NOTE]  
>  O relatório pode conter um item para problemas indetectáveis. Esses são os problemas que não podem ser detectados ou os que gerariam muitos resultados de falso positivo. Clique o **mais informações sobre esse problema e como resolvê-lo** link para ver uma lista dos problemas indetectáveis do componente.  
  
## <a name="see-also"></a>Consulte também  
 [Como: exportar relatórios](../../../2014/sql-server/install/how-to-export-reports.md)   
 [Como: executar o Assistente para análise do Supervisor de atualização](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Solucionando problemas de atualização](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Tópicos de instruções sobre o Supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-how-to-topics.md)   
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
