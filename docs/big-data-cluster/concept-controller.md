---
title: O que é o controlador?
titleSuffix: SQL Server big data clusters
description: Este artigo descreve o controlador de um cluster de Big Data do SQL Server.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 97df8916b713feae56a7cd5344e7fbdc93038317
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358394"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>O que o controlador em um cluster de Big Data do SQL Server?

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

O controlador hospeda a lógica principal para implantar e gerenciar um cluster de Big Data. Ele cuida de todas as interações com o Kubernetes, instâncias do SQL Server que fazem parte do cluster e outros componentes, como o HDFS e o Spark.

O serviço de controlador fornece a seguinte funcionalidade fundamental:

- Gerenciar ciclo de vida do cluster: inicialização e exclusão do cluster, atualização de configurações
- Gerenciar instâncias do SQL Server mestre
- Gerenciar pools de computação, dados e armazenamento
- Expor ferramentas de monitoramento para observar o estado do cluster
- Expor ferramentas de solução de problemas para detectar e reparar problemas inesperados
- Gerenciar a segurança do cluster:
  - Garantir pontos de extremidade de cluster seguros
  - Gerenciar usuários e funções
  - Configurar credenciais para comunicação dentro do cluster

## <a name="deploying-the-controller-service"></a>Implantação do serviço do controlador

O controlador é implantado e hospedado no mesmo namespace do Kubernetes em que o cliente deseja criar um cluster de Big Data. Esse serviço é instalado por um administrador do Kubernetes durante a inicialização do cluster, usando o utilitário de linha de comando **azdata**. Para obter mais informações, confira [Introdução ao [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deploy-get-started.md).

O fluxo de trabalho de buildout será disposto sobre o Kubernetes um cluster de Big Data do SQL Server totalmente funcional que inclui todos os componentes descritos no artigo [Visão geral](big-data-cluster-overview.md). O fluxo de trabalho de inicialização cria primeiro o serviço do controlador e, após ele ser implantado, o serviço do controlador coordenará a instalação e a configuração do restante da parte dos serviços referentes a mestre, computação, dados e pools de armazenamento.

## <a name="managing-the-cluster-through-the-controller-service"></a>Gerenciando o cluster por meio do serviço de controlador

Você pode gerenciar o cluster por meio do serviço de controlador usando os comandos de **azdata**. Se você implantar objetos de Kubernetes adicionais, como pods, no mesmo namespace, eles não serão gerenciados nem monitorados pelo serviço do controlador. Você também pode usar comandos **kubectl** para gerenciar o cluster no nível de Kubernetes. Para obter mais informações, confira [Monitoramento e solução de problemas dos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](cluster-troubleshooting-commands.md).

O controlador e os objetos de Kubernetes (conjuntos com estado, pods, segredos, etc.) criados para um cluster de Big Data residem em um namespace dedicado do Kubernetes. O serviço de controlador receberá permissão do administrador de cluster do Kubernetes para gerenciar todos os recursos dentro desse namespace.  A política de RBAC para esse cenário é configurada automaticamente como parte da implantação do cluster inicial usando **azdata**.

### <a name="azdata"></a>azdata

**azdata** é um utilitário de linha de comando escrito em Python que permite aos administradores de cluster inicializar e gerenciar clusters de Big Data por meio das APIs REST expostas pelo serviço do controlador.

## <a name="controller-service-security"></a>Segurança do serviço de controlador

Toda a comunicação com o serviço do controlador é conduzida por meio de uma API REST por HTTPS. Um certificado autoassinado será gerado automaticamente para você no momento da inicialização. 

A autenticação no ponto de extremidade de serviço do controlador está usando uma identidade do Active Directory ou baseada em nome de usuário e senha. Essas credenciais são provisionadas no momento da inicialização do cluster usando a entrada para variáveis de ambiente `AZDATA_USERNAME` e `AZDATA_PASSWORD`.

> [!NOTE]
> Você deve fornecer uma senha que esteja em conformidade com os [Requisitos de complexidade de senha do SQL Server](../relational-databases/security/password-policy.md).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira os seguintes recursos:

- [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
- [Workshop: Arquitetura dos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] da Microsoft](https://github.com/microsoft/sqlworkshops-bdc)