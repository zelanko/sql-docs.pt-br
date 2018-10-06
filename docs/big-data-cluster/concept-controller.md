---
title: O que é o controlador de cluster de big data do SQL Server? | Microsoft Docs
description: ''
author: mihaelablendea
ms.author: mihaelab
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 6b3a8f01170fecf21fd85dbb2d85d228430fc100
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48795770"
---
# <a name="what-is-the-sql-server-big-data-clusters-controller"></a>O que é o controlador de clusters de grandes dados do SQL Server?

O controlador hospeda a lógica básica para implantar e gerenciar um cluster de big data. Ele cuida de todas as interações com o Kubernetes, instâncias do SQL Server que fazem parte do cluster e outros componentes, como HDFS e Spark. 

O serviço do controlador fornece as seguintes funcionalidades principais:

- Gerenciar o ciclo de vida do cluster: a inicialização do cluster & exclusão, atualize as configurações
- Gerenciar instâncias do mestres do SQL Server
- Gerenciar pools de armazenamento e computação, dados
- Expor as ferramentas de monitoramento para observar o estado do cluster
- Ferramentas de solução de problemas para detectar e reparar problemas inesperados de expor
- Gerenciar a segurança de cluster: Certifique-se de pontos de extremidade do cluster seguro, gerenciar usuários e funções, configurar as credenciais para a comunicação dentro do cluster
- Gerenciar o fluxo de trabalho de atualizações para que eles são implementados com segurança (não disponível no CTP 2.0)
- Gerenciar a alta disponibilidade e recuperação de desastres para serviços com estado no cluster (não disponível no CTP 2.0)

## <a name="deploying-the-controller-service"></a>Implantando o serviço do controlador

O controlador é implantado e hospedado no mesmo namespace do Kubernetes em que o cliente deseja criar um cluster de big data. Esse serviço é instalado por um administrador do Kubernetes durante a inicialização do cluster, usando o utilitário de linha de comando mssqlctl:

```bash
mssqlctl create cluster <name of your cluster>
```

O fluxo de trabalho buildout definirá o layout na parte superior do Kubernetes um cluster de big data totalmente funcional do SQL Server que inclui todos os componentes descritos os [visão geral](big-data-cluster-overview.md) artigo. O fluxo de trabalho de inicialização primeiro cria o serviço do controlador, e quando isso for implantado, o serviço do controlador coordena a instalação e configuração do rest da parte dos serviços de pools de armazenamento, computação, dados e mestre.

## <a name="managing-the-cluster-through-the-controller-service"></a>Gerenciando o cluster por meio do serviço de controlador
Você pode gerenciar o cluster puramente por meio do serviço de controlador usando `mssqlctl` APIs ou o portal de administração de cluster que está hospedado dentro do cluster. Se você implantar objetos Kubernetes adicionais, como os pods no mesmo namespace, eles não são gerenciados ou monitorados pelo serviço do controlador.

O controlador e os objetos de Kubernetes (conjuntos com monitoração de estado, pods, segredos, etc.) criados para um cluster de big data residem em um namespace dedicado do Kubernetes. O serviço do controlador será concedido permissão pelo administrador de cluster do Kubernetes para gerenciar todos os recursos dentro desse namespace.  A política RBAC para esse cenário é configurada automaticamente como parte da implantação de cluster inicial usando `mssqlctl`. 

### <a name="mssqlctl"></a>mssqlctl

`mssqlctl` um utilitário de linha de comando é escrito em Python que permite aos administradores de cluster inicializar e gerenciar clusters de big data por meio das APIs REST expostas pelo serviço do controlador.

### <a name="cluster-administration-portal"></a>Portal de administração de cluster

Depois que o serviço do controlador está em execução, o administrador de cluster pode usar o Portal de administração de Cluster para monitorar o progresso da implantação, detectar e solucionar problemas com os serviços dentro do cluster. 

## <a name="monitoring-and-troubleshooting-the-controller-service"></a>Monitorando e Solucionando problemas de serviço do controlador

Em breve...

## <a name="controller-service-security"></a>Segurança do controlador de serviço
Toda a comunicação com o serviço do controlador é realizada por meio da API REST sobre HTTPS. Um certificado autoassinado será automaticamente gerado para você em tempo de inicialização. 

Autenticação para o ponto de extremidade de serviço do controlador se baseia no nome de usuário e senha. Essas credenciais são provisionadas no momento de inicialização do cluster usando a entrada para as variáveis de ambiente `CONTROLLER_USERNAME` e `CONTROLLER_PASSWORD`.
```

> [!NOTE]
> You must provide a password that is in compliance with [SQL Server password complexity requirements](https://docs.microsoft.com/en-us/sql/relational-databases/security/password-policy?view=sql-server-2017).

## Next steps

To learn more about the SQL Server big data clusters, see the following overview:

- [What is SQL Server 2019 big data clusters?](big-data-cluster-overview.md)
