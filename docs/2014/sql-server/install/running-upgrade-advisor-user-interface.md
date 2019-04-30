---
title: Executando o Supervisor de atualização (Interface do usuário) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- Upgrade Advisor [SQL Server], running
- launching Upgrade Advisor
- Upgrade Advisor Analysis Wizard
- starting Upgrade Advisor
- SQL Server Upgrade Advisor, running
ms.assetid: 7f47c9b3-88d3-43d6-837e-f157b49a55ac
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c402516980f5cf3e1790f8a5fa6d594c93b0e500
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63245955"
---
# <a name="running-upgrade-advisor-user-interface"></a>Executando o Supervisor de Atualização (Interface do usuário)
  Você pode executar o Supervisor de Atualização para analisar componentes locais ou remotos durante o planejamento da atualização. O Supervisor de Atualização gera um relatório para cada componente e instância que é analisado.  
  
> [!IMPORTANT]  
>  Ele não analisa instâncias remotas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para analisar uma instância do [!INCLUDE[ssRS](../../includes/ssrs.md)], o Supervisor de Atualização deve estar instalado no computador em que o [!INCLUDE[ssRS](../../includes/ssrs.md)] está instalado.  
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
  
 Para obter mais informações sobre o Assistente de análise do Supervisor de atualização, consulte [como: Execute o Assistente para análise do Supervisor de atualização](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md).  
  
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
  
-   [Como: Exibir um relatório do Supervisor de atualização](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)  
  
-   [Como: Filtrar relatórios](../../../2014/sql-server/install/how-to-filter-reports.md)  
  
-   [Como: Exportar relatórios](../../../2014/sql-server/install/how-to-export-reports.md)  
  
## <a name="see-also"></a>Consulte também  
 [Como: Execute o Assistente para análise do Supervisor de atualização](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Referência de Interface de usuário do Supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [Solucionando problemas de atualização](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
