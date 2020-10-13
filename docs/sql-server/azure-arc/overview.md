---
title: SQL Server habilitado para Azure Arc
titleSuffix: ''
description: Gerenciar instâncias do SQL Server com SQL Server habilitado para Azure Arc
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 10/07/2020
ms.topic: conceptual
ms.prod: sql
ms.custom: references_regions
ms.openlocfilehash: 5cf1a67d1eeb36ec4889d75241eba34b515264b0
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834314"
---
# <a name="azure-arc-enabled-sql-server-preview"></a>SQL Server habilitado para Azure Arc (versão prévia)

O SQL Server habilitado para Azure Arc faz parte do Azure Arc para servidores. Ele estende os serviços do Azure para instâncias do SQL Server hospedadas fora do Azure no datacenter do cliente, na borda ou em um ambiente de várias nuvens.

Para habilitar os serviços do Azure, uma instância do SQL Server em execução precisa ser registrada com Azure Arc usando o portal do Azure e um script de registro. Após o registro, a instância será representada no Azure como um recurso do __SQL Server – Azure Arc__. As propriedades desse recurso refletem um subconjunto das definições de configuração do SQL Server.

O SQL Server pode ser instalado em uma máquina virtual ou computador físico que executa o Windows ou o Linux que está conectado ao Azure Arc por meio do Connected Machine Agent. O agente está instalado e o computador é registrado automaticamente como parte do registro da instância do SQL Server. O Connected Machine Agent comunica a saída com segurança ao Azure Arc pela porta TCP 443. Se o computador se conectar por meio de um firewall ou servidor proxy HTTP para se comunicar pela Internet, examine os [requisitos de configuração de rede para o Connected Machine Agent](/azure/azure-arc/servers/agent-overview#prerequisites).

A versão prévia pública do SQL Server habilitado para o Azure Arc dá suporte a um conjunto de soluções que exigem que a extensão de servidor do MMA (Microsoft Monitoring Agent) seja instalada e conectada a um workspace do Azure Log Analytics para relatório e coleta de dados. Essas soluções incluem a Segurança de Dados Avançada usando a Central de Segurança do Azure e o Azure Sentinel, bem como as verificações de integridade do Ambiente SQL usando o recurso de Avaliação do SQL sob demanda.

O diagrama a seguir ilustra a arquitetura do SQL Server habilitado para Azure Arc.

![Arquitetura de versão prévia pública](media/overview/pubic-preview-architecture.png)

## <a name="prerequisites"></a>Pré-requisitos

### <a name="supported-sql-versions-and-operating-systems"></a>Sistemas operacionais e versões do SQL compatíveis

O SQL Server habilitado para Azure Arc dá suporte ao SQL Server 2012 ou posterior em uma das seguintes versões do sistema operacional Windows ou Linux:

- Windows Server 2012 R2 e versões posteriores
- Ubuntu 16.04 e 18.04 (x64)
- RHEL (Red Hat Enterprise Linux) 7 (x64) 
- SLES (SUSE Linux Enterprise Server) 15 (x64)

### <a name="required-permissions"></a>Permissões necessárias

Para conectar as instâncias do SQL Server e a hospedagem ao Azure Arc, você precisa ter uma conta com privilégios para executar as seguintes ações:
   * Microsoft.AzureData/*
   * Microsoft.HybridCompute/machines/read
   * Microsoft.HybridCompute/machines/write
   * Microsoft.GuestConfiguration/guestConfigurationAssignments/read

Para uma segurança ideal, é recomendável criar uma função personalizada no Azure que tenha as permissões mínimas listadas. Para obter informações sobre como criar uma função personalizada no Azure com essas permissões, confira [Visão geral das funções personalizadas](https://docs.microsoft.com/azure/active-directory/users-groups-roles/roles-custom-overview). Para adicionar a atribuição de função, confira [Adicionar ou remover atribuições de função usando o portal do Azure](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) ou [Adicionar ou remover atribuições de função usando o Azure RBAC e a CLI do Azure](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-cli).

### <a name="azure-subscription-and-service-limits"></a>Limites de serviço e assinatura do Azure

Antes de configurar seus computadores e instâncias do SQL Server com o Azure Arc, examine os [limites de assinatura](/azure/azure-resource-manager/management/azure-subscription-service-limits#subscription-limits) e os [limites do grupo de recursos](/azure/azure-resource-manager/management/azure-subscription-service-limits#resource-group-limits) do Azure Resource Manager para planejar o número de computadores a ser conectado.

### <a name="networking-configuration-and-resource-providers"></a>Configuração de rede e provedores de recursos

Examine [a configuração de rede, os provedores de segurança e o protocolo TLS](/azure/azure-arc/servers/agent-overview#prerequisites) necessários para o Connected Machine Agent.

### <a name="supported-azure-regions"></a>Regiões do Azure com suporte

Esta versão prévia pública está disponível nas seguintes regiões:
- Leste dos EUA
- Leste dos EUA 2
- Oeste dos EUA 2
- Leste da Austrália
- Sudeste Asiático
- Norte da Europa
- Europa Ocidental
- Sul do Reino Unido

## <a name="next-steps"></a>Próximas etapas

- [Conectar o SQL Server ao Azure Arc](connect.md)
- [Configurar a instância do SQL Server para verificação periódica de integridade do ambiente usando a avaliação do SQL sob demanda](assess.md)
- [Configurar a Segurança de Dados Avançada para a instância do SQL Server](configure-advanced-data-security.md)
