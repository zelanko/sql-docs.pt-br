---
title: Monitor de Atividade do Trabalho (configurações de filtro) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.jobactivitymon.filter.f1
ms.assetid: 89cb0055-5262-447f-8464-7203d4caba78
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 77c42bdf35fce0bb2106e99818e14d5b42992647
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217194"
---
# <a name="job-activity-monitor-filter-settings"></a>Monitor de atividade do trabalho (Configurações de Filtro)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use esta página para reduzir o número de linhas visíveis no Monitor de Atividade do Trabalho. Insira critérios em uma ou em várias das caixas disponíveis, para exibir apenas as linhas correspondentes aos valores especificados. Algumas das caixas, como **Status** ou **Tipo de Bloqueio** , oferecem um número limitado de valores possíveis em uma lista suspensa. Outras, como a caixa **Aplicativo,** permitem inserir qualquer valor e quantos valores você desejar em uma lista separada por vírgula. Ícones da barra de ferramentas permitem ordenar as caixas disponíveis por categoria ou em ordem alfabética. Clique nos critérios para mostrar uma breve descrição de cada um.  
  
 Para filtrar o Monitor de Atividade do Trabalho, forneça quantos critérios de filtragem desejar, clique em **Aplicar filtro**e em **OK**.  
  
## <a name="all-jobs"></a>Todos os trabalhos  
 Este grupo de critérios de filtragem está disponível ao filtrar o Monitor de Atividade do Trabalho.  
  
 **Nome**  
 Filtra trabalhos por nome.  
  
 **Próxima Execução**  
 Filtra pela próxima data agendada para execução.  
  
 **Executável**  
 Exibe os trabalhos que podem ser executados ou trabalhos que não podem ser executados. Selecione **Sim** para exibir apenas os trabalhos que podem ser executados, selecione **Não** para exibir apenas os trabalhos que não podem ser executados ou selecione **Todos** para exibir tanto os trabalhos que podem ser executados quanto os que não podem.  
  
 **Última Execução**  
 Filtra pela data da última execução.  
  
 **Resultado da Última Execução**  
 Filtra trabalhos pelo status da última vez em que os trabalhos foram executados.  
  
 **Enabled**  
 Exibe apenas os trabalhos habilitados ou não habilitados.  
  
 **Categoria**  
 Filtra os trabalhos pela categoria do trabalho.  
  
 **Agendado**  
 Exibe todos os trabalhos com agendas ou sem agendas.  
  
 **Status**  
 Filtra trabalhos pelo status.  
  
## <a name="description-area"></a>Área de Descrição  
 **Caixa Descritiva**  
 Essa caixa sem-nome fornece uma descrição curta dos critérios à medida que eles são selecionados.  
  
 **Aplicar filtro**  
 Para aplicar o filtro, clique em **Aplicar****filtro** e em **OK**. Para manter as configurações de filtro na caixa de diálogo **Configurações de****Filtro** sem aplicá-las, desmarque a opção **Aplicar****filtro**e clique em **OK**para exibir todas as linhas.  
  
 **Liberada**  
 Retorna as configurações de filtro para as configurações padrão.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar Atividade do Trabalho](../../ssms/agent/monitor-job-activity.md)  
  
  
