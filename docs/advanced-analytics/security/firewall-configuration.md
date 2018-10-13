---
title: Configuração do firewall para serviços do SQL Server Machine Learning | Microsoft Docs
description: Como configurar o firewall para serviços do SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: d8a24ca6348054041ca1d8a0f4d0c352dc5bdabd
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48881366"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>Configuração do firewall para serviços do SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo lista as considerações de configuração de firewall que o administrador ou o arquiteto deve ter em mente ao usar serviços de machine learning.

## <a name="default-firewall-rules"></a>Regras de firewall padrão

Por padrão, a instalação do SQL Server desabilita conexões de saída com a criação de regras de firewall. 

No SQL Server 2016 e 2017, essas regras são baseadas nas contas de usuário local, em que a instalação criou uma regra de saída para **SQLRUserGroup** que recebem acesso à rede a seus membros (o cada conta de trabalho foi listada como um princípio local sujeito à a regra.

No SQL Server de 2019, como parte da mudança para AppContainers, há novas regras de firewall com base em SIDs AppContainer: um para cada uma as 20 AppContainers criado pela instalação do SQL Server. Convenções de nomenclatura para o nome da regra de firewall são **bloquear o acesso de rede para AppContainer 00 na instância MSSQLSERVER do SQL Server**, onde 00 é o número de AppContainer (00 – 20 por padrão), e MSSQLSERVER é o nome do SQL Instância do servidor.

> [!Note]
> Se as chamadas de rede são necessárias, você pode desabilitar as regras de saída no Firewall do Windows.

## <a name="restrict-network-access"></a>Restringir o acesso à rede

Em uma instalação padrão, uma regra de firewall do Windows é usada para bloquear todo o acesso de rede de saída de processos de tempo de execução externos. Regras de firewall devem ser criadas para impedir que os processos de tempo de execução externos download de pacotes ou fazer outras chamadas de rede que podem ser potencialmente mal-intencionados.

Se você estiver usando um programa de firewall diferente, você também pode criar regras para bloquear a conexão de rede de saída para tempos de execução externos, definindo regras para as contas de usuário local ou para o grupo representado pelo pool de conta de usuário.

É altamente recomendável que você ative o Firewall do Windows (ou outro firewall de sua escolha) para impedir o acesso irrestrito à rede, os tempos de execução de R ou Python.

## <a name="next-steps"></a>Próximas etapas

[Configurar o firewall do Windows para conexões de entrada](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)