---
description: Gerar tabelas de espelho e instâncias de captura CDC
title: Gerar tabelas de espelho e instâncias de captura CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- mirTab
ms.assetid: 260c1617-eecc-4007-a84d-3c5778ce46b6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9f8340ef153f815d3073edaf4f9a13e99e1e9f67
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88394802"
---
# <a name="generate-mirror-tables-and-cdc-capture-instances"></a>Gerar tabelas de espelho e instâncias de captura CDC

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use a página Gerar Tabelas de Espelho para gerar as tabelas de espelho para as tabelas incluídas na instância CDC  
  
 Clique em **Executar** para criar as tabelas de espelho. O progresso para a criação de cada tabela é exibido e uma mensagem é exibida para você saber se cada tabela de espelho foi concluída com êxito ou com erros. Se qualquer erro ocorrer, clique em **Detalhes** para ver uma caixa de diálogo com uma explicação do erro.  
  
 Se alguma tabela não puder ser criada, você poderá escolher continuar ou excluir as tabelas com falha antes de continuar. Depois de terminar de executar o assistente, você pode decidir se corrige a tabela no banco de dados de origem Oracle ou não usá-la na instância CDC. Se você corrigir a tabela, poderá adicioná-la quando você [Edit Tables](../../integration-services/change-data-capture/edit-tables.md).  
  
 Clique em **Avançar** para abrir a página [Finish](../../integration-services/change-data-capture/finish.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Como criar a instância de banco de dados de alteração do SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)  
  
  
