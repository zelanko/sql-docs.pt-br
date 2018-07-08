---
title: Usando relatórios | Microsoft Docs
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
- overriding reports
- Upgrade Advisor Report Viewer
- reports [Upgrade Advisor], about reports
- formatting reports
- resolved issues [Upgrade Advisor]
- distributing reports [Reporting Services]
- filtering reports [Reporting Services]
- removing report items
- viewing reports
- rerunning analysis
- information issues [Upgrade Advisor]
- deleting report items
- icons [Upgrade Advisor]
- Upgrade Advisor [SQL Server], reports
- sending reports
- blocking issues [Upgrade Advisor]
- sharing reports
- reports [Upgrade Advisor]
- SQL Server Upgrade Advisor, reports
- modifying reports
- distributing reports [Reporting Services], about report distribution
- warnings [Upgrade Advisor]
- analyzing system [Upgrade Advisor], reports
ms.assetid: 4a3cb94a-a7ac-4cec-94c7-db26fcf6d161
caps.latest.revision: 39
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 857f83c12983f7f23fdbedf7f73ce94a2ad91fff
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278357"
---
# <a name="using-reports"></a>Usando relatórios
  Um relatório único é gerado para cada componente e, se necessário, para cada instância analisada pelo Assistente para Análise do Supervisor de Atualização em um servidor. O relatório fornece detalhes sobre problemas conhecidos que podem afetar uma atualização. Ele também fornece links para informações e ações sugeridas para solucionar os problemas identificados.  
  
> [!NOTE]  
>  Se o Visualizador de relatórios do Supervisor de atualização não localizar todos os relatórios no diretório de relatórios padrão, você pode carregar um relatório de um diretório diferente usando o **abrir relatório** link.  
  
## <a name="viewing-reports"></a>Exibindo relatórios  
 O Visualizador de Relatórios do Supervisor de Atualização é usado para exibir relatórios do Supervisor de Atualização. Para exibir relatórios, na página inicial do Supervisor de atualização, clique em **iniciar o Visualizador de relatórios de Supervisor de atualização**.  
  
 Depois de carregar um relatório no servidor, você pode selecionar um componente para o qual deseja verificar os problemas de atualização. Você pode aplicar um filtro a partir de **filtrar por** caixa para ver o seguinte:  
  
-   Todos os problemas  
  
-   Todos os problemas de atualização  
  
-   Problemas de pré-atualização  
  
-   Todos os problemas de migração  
  
-   Problemas resolvidos  
  
-   Problemas não resolvidos  
  
 Se o relatório tiver mais de 20 problemas, você pode mover para o grupo anterior ou seguinte de problemas clicando **próximos 20** ou **20 anteriores** na parte superior ou inferior da lista de problemas.  
  
 Você pode exibir até cinco relatórios salvos selecionando os relatórios a partir de **relatório** caixa de listagem suspensa. Os relatórios são listados pelo carimbo de data/hora de quando foram gerados.  
  
## <a name="report-format"></a>Formato de relatório  
 O visualizador de relatórios exibe os problemas em três colunas. Cada problema pode ser recolhido para que você possa ocultar a descrição ou exibir apenas informações fundamentais.  
  
 A primeira coluna é o **importância** coluna. Os ícones indicam a importância de cada problema. Um círculo vermelho com um X indica problemas importantes ou que podem impedir a atualização; um triângulo amarelo com um ponto de exclamação indica problemas com avisos ou informações. A segunda coluna, **quando corrigir**, indica quando você deve solucionar o problema. Você pode classificar o relatório pela **importância** ou **quando corrigir** coluna. A terceira coluna, **descrição**, lista o título do problema.  
  
 É possível expandir um problema para exibir informações adicionais, um link para informações detalhadas sobre como solucionar o problema e um link para exibir detalhes do problema. Ao clicar no link para acessar informações detalhadas do problema, o tópico da Ajuda com informações sobre o problema e instruções para solucioná-lo é exibido. Depois de corrigir um problema ou para gerenciar seus itens de ação, você pode marcar como concluído, selecionando o **esse problema foi resolvido** caixa de seleção. Se você quiser remover os problemas resolvidos da lista de problemas de atualização, clique em **Refresh**. O problema não seja exibido novamente até que você execute o Assistente de análise do Supervisor de atualização no mesmo componente ou aplica a **problemas resolvidos** filtrar a partir de **filtrar por** opção.  
  
## <a name="report-files"></a>Arquivos de relatório  
 O Assistente de análise do Supervisor de atualização cria relatórios em Meus documentos\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade Advisor\110\Reports diretório e cria um subdiretório para cada servidor que você analisa. Os arquivos de relatório estão no formato XML e seguem uma convenção de nomenclatura específica. Quando você inicia o Visualizador de Relatórios do Supervisor de Atualização, os arquivos de relatório do diretório padrão são exibidos. Se você copiar arquivos de relatório para essa pasta, eles deverão seguir a mesma convenção de nomenclatura ou o visualizador de relatórios não irá exibi-los automaticamente.  
  
 Se você quiser compartilhar a informações com outras pessoas, poderá enviar-lhes o relatório XML. Se preferir usar outro aplicativo, basta exportar o relatório para um arquivo CSV que pode ser usado para criar uma planilha, um arquivo de texto ou uma mensagem de email.  
  
## <a name="see-also"></a>Consulte também  
 [Como: exibir um relatório do Supervisor de atualização](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)   
 [Como: exportar relatórios](../../../2014/sql-server/install/how-to-export-reports.md)   
 [Como: Filtrar relatórios](../../../2014/sql-server/install/how-to-filter-reports.md)   
 [Solucionando problemas de atualização](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
