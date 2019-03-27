---
title: Portal de administração de cluster
titleSuffix: SQL Server 2019 big data clusters
description: Saiba como usar o portal de administração de cluster para monitorar clusters do SQL Server 2019 big data (visualização).
author: yualan
ms.author: alayu
manager: craigg
ms.date: 03/27/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 2ed73006850a5174c6df07ed09302ea48decf6d2
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492858"
---
# <a name="how-to-use-the-cluster-administration-portal-to-monitor-a-sql-server-big-data-cluster"></a>Como usar o portal de administração de cluster para monitorar um cluster de big data do SQL Server

Se você quiser monitorar ou solucionar problemas do seu cluster de big data de 2019 do SQL Server (versão prévia), use o portal de administração de cluster.

O portal de administração de cluster permite que você:
- Exibir o número de pods em execução e todos os problemas rapidamente
- Monitorar o status de implantação
- Exibir pontos de extremidade de serviço disponível
- Controlador de exibição e a instância mestre do SQL Server
- Fazer drill down informações sobre pods, incluindo o acesso a logs de Kibana e painéis do Grafana

## <a name="access-the-cluster-administration-portal"></a>Acessar o portal de administração de cluster

Siga as [guia de início rápido para implantar o cluster de big data](quickstart-big-data-cluster-deploy.md) até chegar à **portal de administração de cluster** seção. Depois que o cluster de big data em execução com mssqlctl, siga estas instruções:

Quando o pod de controlador estiver em execução, você pode usar o portal de administração de cluster para monitorar a implantação. Você pode acessar o portal usando o IP endereço e porta número externa para o `endpoint-service-proxy` (por exemplo: **https://\<endereço ip\>: 30777/portal**). As credenciais para acessar o portal de administração é os valores de `CONTROLLER_USERNAME` e `CONTROLLER_PASSWORD` variáveis de ambiente fornecidas acima.

> [!NOTE]
> Para CTP 2.4, há um aviso de segurança ao acessar a página da web, pois ele está usando certificados gerados automaticamente SSL.

## <a name="overview"></a>Visão geral

![visão geral](./media/cluster-admin-portal/portal-overview.png)

Quando você entra pela primeira vez no portal, você pode exibir rapidamente o número de pods em execução em:
- Controlador
- Instância mestre
- Pool de computação
- Pool de armazenamento
- Pool de dados

Se houver algum problema, você pode abrir um link para problemas conhecidos. Você pode usar o painel de navegação esquerdo para ir para o pool específico se houver um problema.

## <a name="deployment"></a>Implantação

![implantação](./media/cluster-admin-portal/portal-deployment.png)

Para monitorar sua implantação, clique na guia de implantação à esquerda. Você pode ver uma exibição de árvore de sua implantação, e se houver algum problema na implantação.

## <a name="service-endpoints"></a>Pontos de extremidade de serviço

![pontos de extremidade](./media/cluster-admin-portal/portal-endpoints.png)

Você pode exibir os pontos de extremidade de serviço disponíveis clicando na guia pontos de extremidade no painel de navegação à esquerda.

Isso inclui links para o ponto de extremidade do Spark, painel do Grafana, e logs do Kibana.

## <a name="controller"></a>Controlador

![Controlador](./media/cluster-admin-portal/portal-controller.png)

O controlador mostra todos os pods relacionados ao controlador. Você pode aprender mais sobre o controlador [aqui.](concept-controller.md)

Para saber mais informações adicionais sobre cada pod, você pode clicar em **métricas** coluna para exibir painéis do Grafana.

Para saber mais sobre os logs para pods com problemas, você pode clicar na **Logs** coluna.

## <a name="master-instance"></a>Instância mestre

![pontos de extremidade](./media/cluster-admin-portal/portal-master.png)

A instância mestre mostra todos os pods relacionados a instância mestre do SQL Server. Você pode aprender mais sobre a instância mestre do SQL Server [aqui.](concept-master-instance.md)

Para saber mais informações adicionais sobre cada pod, você pode clicar em **métricas** coluna para exibir painéis do Grafana.

Para saber mais sobre os logs para pods com problemas, você pode clicar na **Logs** coluna.

## <a name="pool-and-pod-pages"></a>Pool e páginas de Pod

![Pool](./media/cluster-admin-portal/portal-data-pool.png)

Em cada página do pool (computação, armazenamento e dados), é possível Detalhar cada uma das páginas pod clicando no **padrão**

![pod](./media/cluster-admin-portal/portal-data-default-pool.png)

Isso mostra uma navegação de trilha na parte superior de caminho de detalhamento.

Para saber mais informações adicionais sobre cada pod, você pode clicar em **métricas** coluna para exibir painéis do Grafana.

Para saber mais sobre os logs para pods com problemas, você pode clicar na **Logs** coluna.

Para saber mais sobre cada pool:
- [pool de computação](concept-compute-pool.md)
- [pool de armazenamento](concept-storage-pool.md)
- [pool de dados](concept-data-pool.md)

## <a name="about-page"></a>Sobre a página

![sobre](./media/cluster-admin-portal/portal-about.png)

Aqui você pode exibir informações sobre o cluster como os números de versão diferentes, contêineres e um link para a documentação.

## <a name="next-steps"></a>Próximas etapas

Além do portal de administração do cluster, você também pode executar vários comandos úteis do Kubernetes para explorar o status e a integridade do seu cluster. Para obter mais informações, consulte [comandos Kubectl para monitoramento e solução de problemas de clusters de grandes dados do SQL Server](cluster-troubleshooting-commands.md).

Para saber mais sobre clusters de big data de 2019 do SQL Server, consulte [quais são os clusters do SQL Server 2019 big data?](big-data-cluster-overview.md).
