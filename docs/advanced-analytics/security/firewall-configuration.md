---
title: Configuração do firewall
description: Como configurar o firewall para conexões de saída de SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 58a10c36eff06cd4e36f3e326407564b2657fec1
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345597"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>Configuração de firewall para SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo lista as considerações de configuração do firewall que o administrador ou o arquiteto deve ter em mente ao usar os serviços do Machine Learning.

## <a name="default-firewall-rules"></a>Regras de firewall padrão

Por padrão, a instalação do SQL Server desabilita as conexões de saída criando regras de firewall.

No SQL Server 2016 e 2017, essas regras são baseadas em contas de usuário local, em que a instalação criou uma regra de saída para **SQLRUserGroup** que negou acesso à rede para seus membros (cada conta de trabalho foi listada como um princípio local sujeito à regra. Para obter mais informações sobre SQLRUserGroup, consulte [visão geral de segurança para a estrutura de extensibilidade no SQL Server serviços de Machine Learning](../../advanced-analytics/concepts/security.md#sqlrusergroup).

No SQL Server 2019, como parte da mudança para AppContainers, há novas regras de firewall baseadas em SIDs de AppContainer: uma para cada um dos 20 AppContainers criados pela instalação do SQL Server. As convenções de nomenclatura para o nome da regra de firewall são **bloquear o acesso à rede para o appcontainer-00 na instância SQL Server MSSQLSERVER**, em que 00 é o número do appcontainer (00-20 por padrão) e MSSQLSERVER é o nome da instância de SQL Server.

> [!Note]
> Se forem necessárias chamadas de rede, você poderá desabilitar as regras de saída no firewall do Windows.

## <a name="restrict-network-access"></a>Restringir o acesso à rede

Em uma instalação padrão, uma regra de firewall do Windows é usada para bloquear todo o acesso de rede de saída de processos de tempo de execução externos. As regras de firewall devem ser criadas para impedir que os processos de tempo de execução externos baixem pacotes ou façam outras chamadas de rede que possam ser mal-intencionadas.

Se você estiver usando um programa de firewall diferente, também poderá criar regras para bloquear a conexão de rede de saída para tempos de execução externos, definindo regras para as contas de usuário local ou para o grupo representado pelo pool de contas de usuário.

É altamente recomendável que você ative o Firewall do Windows (ou outro firewall de sua escolha) para impedir o acesso irrestrito à rede pelos tempos de execução do R ou do Python.

## <a name="next-steps"></a>Próximas etapas

[Configurar o Firewall do Windows para conexões em associação](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)