---
title: Configuração do firewall
description: Como configurar o firewall para conexões de saída dos Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/17/2018
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f8cf14b294c85f90b0e44375f751a84a50b30e04
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180413"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>Configuração de firewall para os Serviços de Machine Learning do SQL Server
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este artigo lista as considerações de configuração do firewall que o administrador ou o arquiteto deve ter em mente ao usar os Serviços de Machine Learning.

## <a name="default-firewall-rules"></a>Regras de firewall padrão

Por padrão, a instalação do SQL Server desabilita as conexões de saída criando regras de firewall.

No SQL Server 2016 e 2017, essas regras se baseiam em contas de usuário local, em que a instalação criou uma regra de saída para **SQLRUserGroup** que negou acesso à rede para seus membros (cada conta de trabalho foi listada como uma entidade de princípio local para a regra). Para obter mais informações sobre SQLRUserGroup, confira [Visão geral de segurança para a estrutura de extensibilidade nos Serviços de Machine Learning do SQL Server](../../machine-learning/concepts/security.md#sqlrusergroup).

No SQL Server 2019, como parte da mudança para os AppContainers, há novas regras de firewall baseadas em SIDs de AppContainer: uma para cada um dos 20 AppContainers criados pela instalação do SQL Server. As convenções de nomenclatura para o nome da regra de firewall são **Bloquear o acesso à rede para o AppContainer-00 na instância MSSQLSERVER do SQL Server**, em que 00 é o número do AppContainer (00-20 por padrão) e MSSQLSERVER é o nome da instância do SQL Server.

> [!Note]
> Se forem necessárias chamadas de rede, você poderá desabilitar as regras de saída no Firewall do Windows.

## <a name="restrict-network-access"></a>Restringir acesso à rede

Na instalação padrão, uma regra de Firewall do Windows é usada para bloquear todo o acesso à rede de saída dos processos de runtime externos. As regras de firewall devem ser criadas para impedir que o processo de runtime de externo baixe pacotes ou faça outras chamadas de rede que possam ser potencialmente mal-intencionadas.

Se você estiver usando um programa de firewall diferente, também poderá criar regras para bloquear conexões de rede de saída para runtimes externos, definindo regras para as contas de usuário local ou para o grupo representado pelo pool de contas de usuário.

É altamente recomendável que você ative o Firewall do Windows (ou outro firewall de sua escolha) para evitar o acesso irrestrito à rede pelos runtimes de R ou Python.

## <a name="next-steps"></a>Próximas etapas

[Configurar o Firewall do Windows para conexões em associação](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)