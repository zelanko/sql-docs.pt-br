---
title: O que é o controlador?
titleSuffix: SQL Server big data clusters
description: Este artigo descreve o controlador de um cluster de big data do SQL Server 2019 (visualização).
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 076cc40c09d4b086ae7a416ac1cc5ccbcc16a20a
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67729177"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>O que é o controlador em um cluster de big data do SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O controlador hospeda a lógica básica para implantar e gerenciar um cluster de big data. Ele cuida de todas as interações com o Kubernetes, instâncias do SQL Server que fazem parte do cluster e outros componentes, como HDFS e Spark.

O serviço do controlador fornece as seguintes funcionalidades principais:

- Gerenciar o ciclo de vida do cluster: a inicialização do cluster & exclusão, atualize as configurações
- Gerenciar instâncias do mestres do SQL Server
- Gerenciar pools de computação, dados e armazenamento
- Expor as ferramentas de monitoramento para observar o estado do cluster
- Ferramentas de solução de problemas para detectar e reparar problemas inesperados de expor
- Gerencie segurança de cluster:
  - Certifique-se de pontos de extremidade do cluster seguro
  - Gerenciar usuários e funções
  - Configurar credenciais para a comunicação dentro do cluster

## <a name="deploying-the-controller-service"></a>Implantando o serviço do controlador

O controlador é implantado e hospedado no mesmo namespace do Kubernetes em que o cliente deseja criar um cluster de big data. Esse serviço é instalado por um administrador de Kubernetes durante cluster bootstrap, usando o **mssqlctl** utilitário de linha de comando. Para obter mais informações, consulte [Introdução aos clusters de grandes dados do SQL Server](deploy-get-started.md).

O fluxo de trabalho buildout definirá o layout na parte superior do Kubernetes um cluster de big data totalmente funcional do SQL Server que inclui todos os componentes descritos os [visão geral](big-data-cluster-overview.md) artigo. O fluxo de trabalho de inicialização primeiro cria o serviço do controlador, e quando isso for implantado, o serviço do controlador coordena a instalação e configuração do rest da parte dos serviços de pools de armazenamento, computação, dados e mestre.

## <a name="managing-the-cluster-through-the-controller-service"></a>Gerenciando o cluster por meio do serviço de controlador

Você pode gerenciar o cluster por meio do serviço de controlador usando um **mssqlctl** comandos. Se você implantar objetos Kubernetes adicionais, como os pods no mesmo namespace, eles não são gerenciados ou monitorados pelo serviço do controlador. Você também pode usar **kubectl** comandos para gerenciar o cluster no nível do Kubernetes. Para obter mais informações, consulte [monitoramento e solução de problemas de clusters de grandes dados do SQL Server](cluster-troubleshooting-commands.md).

O controlador e os objetos de Kubernetes (conjuntos com monitoração de estado, pods, segredos, etc.) criados para um cluster de big data residem em um namespace dedicado do Kubernetes. O serviço do controlador será concedido permissão pelo administrador de cluster do Kubernetes para gerenciar todos os recursos dentro desse namespace.  A política RBAC para esse cenário é configurada automaticamente como parte da implantação de cluster inicial usando **mssqlctl**.

### <a name="mssqlctl"></a>mssqlctl

**mssqlctl** é um utilitário de linha de comando escrito em Python que permite que os administradores inicializar e gerenciar clusters de big data por meio das APIs REST expostas pelo serviço de controlador de cluster.

## <a name="controller-service-security"></a>Segurança do controlador de serviço

Toda a comunicação com o serviço do controlador é realizada por meio da API REST sobre HTTPS. Um certificado autoassinado será automaticamente gerado para você em tempo de inicialização. 

Autenticação para o ponto de extremidade de serviço do controlador se baseia no nome de usuário e senha. Essas credenciais são provisionadas no momento de inicialização do cluster usando a entrada para as variáveis de ambiente `CONTROLLER_USERNAME` e `CONTROLLER_PASSWORD`.

> [!NOTE]
> Você deve fornecer uma senha que está em conformidade com [requisitos de complexidade de senha do SQL Server](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de grandes dados do SQL Server, consulte os seguintes recursos:

- [Quais são os clusters do SQL Server 2019 grandes dados?](big-data-cluster-overview.md)
- [Workshop: Arquitetura de clusters de grandes dados do Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
