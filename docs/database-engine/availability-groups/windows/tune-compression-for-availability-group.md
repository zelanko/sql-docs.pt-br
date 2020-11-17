---
title: Ajustar a compactação do grupo de disponibilidade | Microsoft Docs
description: Saiba como o SQL Server compacta fluxos de dados para grupos de disponibilidade, o que reduz o tráfego de rede, aumenta a carga da CPU e pode induzir à latência.
ms.custom: ''
ms.date: 06/22/2016
ms.prod: sql
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 7632769c-b246-4766-886f-7c60ec540be8
author: cawrites
ms.author: chadam
ms.openlocfilehash: 6b618efb64f5409e16665d772accbbe9434e8ffd
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583679"
---
# <a name="tune-compression-for-availability-group"></a>Ajustar a compactação do grupo de disponibilidade
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
Por padrão, o SQL Server compacta fluxos de dados, quando apropriado, de grupos de disponibilidade. A compactação reduz o tráfego de rede, aumenta a carga da CPU e pode induzir a latência. Você deve ser membro da função de servidor fixa sysadmin para habilitar a compactação. A seguinte tabela mostra os casos em que o SQL Server usa a compactação para os fluxos de log do grupo de disponibilidade:

| Cenário | Configuração da compactação
| ---- | ----
| Réplica de confirmação síncrona | Não compactado
| Réplicas de confirmação assíncrona | Compressed
| Durante a propagação automática | Não compactado
| TDE habilitado no banco de dados  | Não compactado

## <a name="trace-flags-for-availability-group-compression"></a>Sinalizadores de rastreamento para a compactação do grupo de disponibilidade 

Na maioria dos cenários, a Microsoft não recomenda alterar essas configurações. É possível usar sinalizadores de rastreamento global para testar a alteração dessas configurações. O SQL Server aplica os sinalizadores de rastreamento global a toda a instância. Todos os grupos de disponibilidade na instância serão afetados por essas configurações.  

A tabela a seguir mostra os sinalizadores de rastreamento que alterarão o comportamento padrão da compactação do SQL Server. 

Sinalizador de rastreamento | Descrição
------------- | -------------
1462          | Desabilita a compactação do fluxo de logs dos Grupos de Disponibilidade com réplicas síncronas. Esse recurso está habilitado por padrão em réplicas assíncronas para otimizar a largura de banda de rede.
9567          | Habilita a compactação do fluxo de dados em Grupos de Disponibilidade durante a propagação automática. Durante a propagação automática, a compactação pode reduzir de forma significativa o tempo de transferência e aumentará a carga no processador.
9592          | Habilita a compactação do fluxo de logs dos Grupos de Disponibilidade com réplicas síncronas. Esse recurso está desabilitado por padrão em réplicas síncronas, pois a compactação adiciona latência. A compactação do fluxo de log está habilitada por padrão em réplicas assíncronas.


## <a name="resources"></a>Recursos


[Opções de inicialização do Mecanismo de Banco de Dados](../../../database-engine/configure-windows/database-engine-service-startup-options.md)

[Propagação automática](./automatically-initialize-always-on-availability-group.md)

[Pré-requisitos do AlwaysOn](prereqs-restrictions-recommendations-always-on-availability.md)