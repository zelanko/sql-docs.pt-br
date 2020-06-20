---
title: Configuração de rede de cluster | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- cluster network selection, Setup
- cluster network selection
ms.assetid: 579482ef-a023-45b2-9176-b4a4188adf9d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 04b0d412cd577fb0869f2188d99c1ea6a5646d2b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85037166"
---
# <a name="cluster-network-configuration"></a>Configuração de rede do cluster
  Use a página **Seleção de Rede de Cluster** para especificar os recursos de rede para sua instância de cluster de failover.  
  
## <a name="options"></a>Opções  
 ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Nome de rede do cluster de failover** -esse é o nome usado para identificar a instância de cluster de failover na rede.  
  
 **Configurações de Rede** — Especifique o tipo e o endereço IP da instância de cluster de failover.  
  
 Durante as operações Adicionar Nó e Remover Nó, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibe uma lista somente leitura dos endereços IP existentes para o cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Instalação Integrada:  
  
    -   Se você estiver adicionando um nó que tenha suporte para um conjunto idêntico de sub-redes de rede com suporte dos nós existentes do cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , nenhum outro endereço IP poderá ser adicionado. A configuração de dependência permanece inalterada.  
  
    -   Se você estiver adicionando um nó que tenha um subconjunto das sub-redes com suporte dos nós existentes no cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , nenhum outro recurso de endereço IP poderá ser adicionado. A dependência de recurso de endereço IP é definida como OR para refletir que todos os endereços IP especificados não sejam válidos em todos os nós de cluster.  
  
    -   Se você estiver adicionando um nó que tenha suporte para sub-redes, além das sub-redes já com suporte dos nós existentes no cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , terá a opção de adicionar novos endereços IP válidos. Se novos endereços IP forem especificados, a dependência de recurso de endereço IP será definida como OR para refletir que todos os endereços IP especificados não sejam válidos em todos os nós de cluster.  
  
    -   Se você estiver adicionando um nó que tenha suporte para mais sub-redes de rede, mas que não tenha suporte para nenhuma das sub-redes aceitas pelos nós existentes no cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , será necessário adicionar mais endereços IP. A dependência de recurso de endereço IP é definida como OR para refletir que todos os endereços IP especificados não sejam válidos em todos os nós de cluster.  
  
-   Instalação Avançada: Durante a etapa Concluir da instalação, especifique o endereço IP de todos os nós e sub-redes da instância de cluster de failover. Você pode especificar vários endereços IP para um cluster de failover de várias sub-redes, mas há suporte para apenas um endereço IP por sub-rede. Cada nó preparado deve ser um possível proprietário de pelo menos um endereço IP. Se você tiver várias sub-redes em seu cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , será solicitado que defina a dependência de recurso de endereço IP como OR.Remove Node:  
  
    -   Se houver suporte para os endereços IP restantes em todos os outros nós, você deverá definir a dependência de recurso de endereço IP como AND.  
  
    -   Se não houver suporte para os endereços IP restantes em todos os outros nós, a dependência de recurso de endereço IP será deixada como OR.  
  
  
