---
title: Executando o Supervisor de atualização (Interface do usuário) | Microsoft Docs
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
- Upgrade Advisor Report Viewer
- Upgrade Advisor [SQL Server], running
- launching Upgrade Advisor
- Upgrade Advisor Analysis Wizard
- starting Upgrade Advisor
- SQL Server Upgrade Advisor, running
ms.assetid: 7f47c9b3-88d3-43d6-837e-f157b49a55ac
caps.latest.revision: 40
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2bc1151b2df35b7912d03519cdf7f659ba96af16
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37216586"
---
# <a name="running-upgrade-advisor-user-interface"></a>Executando o Supervisor de Atualização (Interface do usuário)
  Você pode executar o Supervisor de Atualização para analisar componentes locais ou remotos durante o planejamento da atualização. O Supervisor de Atualização gera um relatório para cada componente e instância que é analisado.  
  
> [!IMPORTANT]  
>  Ele não analisa instâncias remotas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para analisar uma instância do [!INCLUDE[ssRS](../../includes/ssrs-md.md)], o Supervisor de Atualização deve estar instalado no computador em que o [!INCLUDE[ssRS](../../includes/ssrs-md.md)] está instalado.  
>   
>  Para analisar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services, você deve ter o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] instalado e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instalado no mesmo computador.  
  
## <a name="running-the-upgrade-advisor-analysis-wizard"></a>Executando o Assistente para análise do Supervisor de atualização  
 Executar o Assistente de análise do Supervisor de atualização tem seis etapas:  
  
1.  Iniciar o assistente na página inicial do Supervisor de Atualização.  
  
2.  Identificar o servidor e os componentes que serão analisados.  
  
3.  Reunir informações de autenticação.  
  
4.  Reunir outros parâmetros com base no tipo de parâmetro.  
  
5.  Analisar os componentes selecionados.  
  
6.  Gerar o relatório dos problemas de atualização.  
  
 Para obter mais informações sobre o Assistente de análise do Supervisor de atualização, consulte [como: executar o Assistente de análise do Supervisor de atualização](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md).  
  
 Para obter informações específicas necessárias para cada etapa, consulte [Atualizar referência de Interface de usuário do Orientador de](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md).  
  
## <a name="running-the-upgrade-advisor-report-viewer"></a>Executando o Visualizador de relatórios do Supervisor de atualização  
 Você usa o Visualizador de Relatórios do Supervisor de Atualização para exibir relatórios gerados pelo Assistente para Análise do Supervisor de Atualização. Quando os relatórios são carregados, você pode filtrar seus componentes pelos seguintes fatores:  
  
-   Todos os problemas  
  
-   Todos os problemas de atualização  
  
-   Problemas de pré-atualização  
  
-   Todos os problemas de migração  
  
-   Problemas resolvidos  
  
-   Problemas não resolvidos  
  
 Para verificar as instruções passo a passo de como usar o Visualizador de Relatórios, consulte os seguintes tópicos:  
  
-   [Como exibir um relatório do Supervisor de Atualização](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)  
  
-   [Como filtrar relatórios](../../../2014/sql-server/install/how-to-filter-reports.md)  
  
-   [Como exportar relatórios](../../../2014/sql-server/install/how-to-export-reports.md)  
  
## <a name="see-also"></a>Consulte também  
 [Como: executar o Assistente para análise do Supervisor de atualização](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Referência de Interface de usuário do Supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [Solucionando problemas de atualização](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
