---
title: Visão geral do Supervisor de atualização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- SQL Server Upgrade Advisor, components
- tools [Upgrade Advisor]
- Upgrade Advisor [SQL Server], components
- components [Upgrade Advisor]
- Upgrade Advisor Analysis Wizard
- limitations [Upgrade Advisor]
- analyzing system [Upgrade Advisor]
- analyzing system [Upgrade Advisor], about analysis
ms.assetid: f5c56f63-4478-40af-abb9-642f58a0026c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c78630764a26bb8fe281446c1bb997f18d965db7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091603"
---
# <a name="upgrade-advisor-overview"></a>Visão geral do Supervisor de Atualização
  O Supervisor de Atualização fornece um console central para análise de componentes do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] e do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e para exibição de relatórios que contenham informações sobre os resultados da análise.  
  
## <a name="how-upgrade-advisor-works"></a>Como o Supervisor de Atualização funciona  
 Quando você executa o Supervisor de Atualização, a página inicial do Supervisor de Atualização é exibida. Essa página inicial é usada para iniciar o seguinte:  
  
-   Assistente para Análise do Supervisor de Atualização  
  
-   Visualizador de Relatórios do Supervisor de Atualização  
  
-   Tópicos da Ajuda do Supervisor de Atualização  
  
 Ao usar o Supervisor de Atualização pela primeira vez, execute o Assistente para Análise do Supervisor de Atualização para analisar um servidor. Quando o assistente concluir a análise, clique em **Iniciar relatório** no assistente ou retorne à página inicial do Supervisor de atualização. Ali, execute o Visualizador de Relatórios do Supervisor de Atualização para exibir o relatório. O relatório contém links para informações que lhe ajudarão a resolver problemas conhecidos.  
  
## <a name="upgrade-advisor-analysis-wizard"></a>Assistente para Análise do Supervisor de Atualização  
 Para executar uma análise, clique em **iniciar o Assistente para análise Supervisor de atualização** na página inicial do Supervisor de atualização. O Assistente para Análise do Supervisor de Atualização reúne informações sobre o computador, as instâncias e os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os arquivos de rastreamento que você deseja analisar. Depois que todas as informações foram coletadas e confirmadas, o Assistente para Análise do Supervisor de Atualização analisa os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Sempre que você executa o Assistente para Análise do Supervisor de Atualização, é gerado um relatório separado, e os relatórios existentes para componentes selecionadas não são substituídos. Entretanto, o visualizador de relatórios exibe apenas os cinco relatórios mais recentes.  
  
 Quando o Assistente para Análise do Supervisor de Atualização finaliza a análise, ele cria um arquivo XML para cada componente analisado. Os arquivos XML contêm os itens e problemas descobertos em cada componente.  
  
### <a name="what-upgrade-advisor-analyzes"></a>O que o Supervisor de Atualização analisa  
 Um analisador dedicado é executado no contexto do Supervisor de Atualização para cada componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como resultado, é gerado um relatório XML para cada componente analisado.  
  
 O Supervisor de Atualização consulta os seguintes componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Servidor de banco de dados (também chamado de [!INCLUDE[ssDE](../../includes/ssde-md.md)] nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) que inclui a Replicação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, a Pesquisa de Texto Completo e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
> [!NOTE]  
>  Durante a análise, cada analisador cria um arquivo de log. Você pode usar esses arquivos de log para diagnosticar a análise. Por exemplo, se o Supervisor de Atualização está executando lentamente, você pode exibir os arquivos de log para determinar a causa da lentidão.  
  
### <a name="upgrade-advisor-limitations"></a>Limitações do Supervisor de Atualização  
 O Supervisor de Atualização não pode detectar todos os problemas que podem afetar uma atualização. Por exemplo, se você tiver código SQL inserido em um aplicativo cliente que é executado em áreas de trabalho de usuários finais, o Supervisor de Atualização não poderá analisar os aplicativos. No caso desses itens, você ainda terá que considerar os problemas e atualizar, migrar ou modificar as informações conforme necessário em sua instalação.  
  
 O Supervisor de Atualização não analisa procedimentos armazenados criptografados, códigos em procedimentos armazenados estendidos e código fonte em uma linguagem diferente de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="upgrade-advisor-report-viewer"></a>Visualizador de Relatórios do Supervisor de Atualização  
 Para exibir um relatório do Supervisor de atualização, clique em **iniciar o Visualizador de relatórios de Supervisor de atualização** na página inicial do Supervisor de atualização. Quando o Visualizador de Relatórios do Supervisor de Atualização for iniciado, os relatórios no diretório padrão serão carregados. Relatórios não são exibidos se o Visualizador de relatórios do Supervisor de atualização não localizar todos os relatórios no diretório padrão. Se não houver relatórios no diretório padrão, você poderá executar o Assistente para Análise do Supervisor de Atualização para criar um relatório ou carregar um relatório existente de outro servidor ou de um subdiretório.  
  
 O Supervisor de Atualização do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] não substitui relatórios existentes. Entretanto, o visualizador de relatórios exibe apenas os cinco relatórios mais recentes. Para exibir um relatório anterior, selecione o relatório a partir de **relatório** caixa de listagem suspensa. O carimbo de data/hora indica a data e a hora em que o relatório foi gerado.  
  
 Quando arquivos XML do Assistente para Análise do Supervisor de Atualização são localizados no Visualizador de Relatórios do Supervisor de Atualização, é exibido um relatório para cada componente. O relatório contém todos os problemas conhecidos, detectáveis e não, que você precisa solucionar. Para cada problema, há um ícone indicando a importância, um rótulo informando quando o problema deve ser solucionado e uma breve descrição. Quando você expandir um problema, verá uma descrição completa, um link para os detalhes do problema e um link para o arquivo da Ajuda. As informações de cada problema são projetadas para fornecer detalhes suficientes para que você possa solucionar o problema.  
  
 A maioria dos componentes tem problemas que não podem ser detectados. Para exibir esses problemas, expanda o **outros problemas de atualização** para o componente de item e, em seguida, clique no link para exibir informações adicionais sobre os problemas na documentação. Para obter mais informações sobre problemas de compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
