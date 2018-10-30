---
title: Armazenar um relatório em cache (Gerenciador de Relatórios) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- cache [Reporting Services]
- cached reports [Reporting Services]
- schedules [Reporting Services], report expiration
- expiration [Reporting Services]
ms.assetid: 723d1cb0-c2e7-4763-8690-a6a7a8bbbb90
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9106fffcd2a66254acf5a47799fc8942ef3f0b38
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50030685"
---
# <a name="cache-a-report-report-manager"></a>Armazenar um relatório em cache (Gerenciador de Relatórios)
  Um modo de melhorar o desempenho é configurar propriedades de cache para um relatório. Quando um relatório é armazenado em cache, uma cópia do relatório renderizado é salva por um curto período de tempo. O primeiro usuário que solicita o relatório deve aguardar a conclusão do processamento antes de exibir o relatório. Usuários subsequentes que solicitam o relatório dentro do período de cache podem exibi-lo imediatamente porque o processamento já ocorreu.  
  
 Há restrições quanto aos tipos de relatórios que podem ser armazenados em cache. Por exemplo, um relatório não pode ser armazenado em cache se suas saídas forem diferentes dependendo da identidade do usuário ou se os dados forem recuperados com o token de segurança do usuário que solicita o relatório. Para obter mais informações, consulte [Armazenando relatórios em cache &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md).  
  
### <a name="to-schedule-the-expiration-of-a-cached-report"></a>Para agendar a validade de um relatório armazenado em cache  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** . Navegue até o relatório cujas propriedades de cache você deseja definir, passe o mouse sobre o item e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**.  
  
4.  No quadro esquerdo, clique em **Opções de Processamento**.  
  
5.  Na página, selecione **Sempre executar este relatório com a data mais recente**.  
  
6.  Selecione um das duas opções de cache a seguir e configure a validade do seguinte modo:  
  
    -   Para configurar uma cópia armazenada em cache para expirar depois de um período de tempo específico, clique em **Armazenar uma cópia temporária do relatório em cache. Expirar cópia de relatório após alguns minutos**. Digite o número de minutos para a validade do relatório.  
  
    -   Para configurar uma cópia armazenada em cache para expirar com base em um agendamento, clique em **Armazenar uma cópia temporária do relatório em cache. Expirar cópia de relatório no próximo agendamento.** Clique em **Configurar**ou selecione uma agenda compartilhada para controlar a validade do relatório  
  
7.  Clique em **Aplicar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Definir as propriedades do processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Armazenando relatórios em cache &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)  
  
  
