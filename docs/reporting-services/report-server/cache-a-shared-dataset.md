---
title: Armazenar em cache um conjunto de dados compartilhado | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: c2d8c81a-da1e-4a8a-9845-fff9a0903d24
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 73d33f2ca15bda09b29cda5fe9e6c350f05dc10c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47699551"
---
# <a name="cache-a-shared-dataset"></a>Armazenar em cache um conjunto de dados compartilhado
  Um modo de melhorar o desempenho é configurar propriedades de cache para um conjunto de dados compartilhado. Quando um conjunto de dados compartilhado é armazenado em cache, uma cópia dos resultados da consulta é salva por um período de tempo específico. O primeiro usuário que solicita um relatório que usa o conjunto de dados compartilhado deve aguardar os resultados da consulta e a conclusão de todo o processamento antes de exibir o relatório. Os usuários subsequentes que solicitarem o relatório dentro do período de cache terão um desempenho melhor porque a consulta e o processamento já ocorreram. Também é possível especificar um plano de atualização de cache para executar a consulta e armazenar os resultados em cache até a expiração de cache especificada.  
  
 Os usuários que estiverem executando relatórios com base em um conjunto de dados compartilhado ou em planos de atualização de cache criam o cache de consultas e, em ambos os casos, o cache permanece disponível com base nas opções de expiração de cache.  
  
 Há restrições quanto aos tipos de conjuntos de dados compartilhados que podem ser armazenados em cache. Por exemplo, os resultados da consulta não podem ser armazenados em cache se os dados variam de acordo com a identidade do usuário ou se os dados forem recuperados com o token de segurança do usuário que solicita o relatório. Para obter mais informações, consulte [Armazenar conjuntos de dados compartilhados em cache &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md) e [Armazenando relatórios em cache &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md).  
  
### <a name="to-schedule-the-expiration-of-a-cached-report"></a>Para agendar a validade de um relatório armazenado em cache  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  No Gerenciador de Relatórios, navegue até o conjunto de dados compartilhado para o qual deseja definir propriedades de armazenamento em cache, passe o mouse sobre o item e clique na seta suspensa.  
  
3.  No menu suspenso, clique em **Gerenciar**.  
  
4.  No quadro esquerdo, clique em **Cache**.  
  
    > [!NOTE]  
    >  Caso veja o erro **As credenciais usadas para executar o conjunto de dados compartilhado não estão armazenadas**, a opção de conjunto de dados compartilhado em cache será desabilitada. É preciso modificar a fonte de dados para armazenar as credenciais ou modificar o conjunto de dados compartilhado para usar uma fonte de dados diferente que não armazena credenciais.  
  
5.  Selecione **Conjunto de dados de compartilhamento em cache**.  
  
6.  Selecione a opção para expirar o cache depois de 30 minutos. Você também pode optar pela expiração do cache em uma agenda especificada.  
  
7.  Clique em **Aplicar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar conjuntos de dados compartilhados](../../reporting-services/report-data/manage-shared-datasets.md)  
  
  
