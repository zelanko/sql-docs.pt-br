---
title: O que é o controlador?
titleSuffix: SQL Server big data clusters
description: Este artigo descreve o controlador de um cluster de Big Data do SQL Server 2019 (versão prévia).
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e984c3dced4bde713ac98d67c22481e54491cd68
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68419541"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>O que o controlador em um cluster de Big Data do SQL Server?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

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

O controlador é implantado e hospedado no mesmo namespace do Kubernetes em que o cliente deseja criar um cluster de Big Data. Esse serviço é instalado por um administrador do Kubernetes durante a inicialização do cluster, usando o utilitário de linha de comando **azdata**. Para saber mais, confira [Introdução aos clusters de Big Data do SQL Server](deploy-get-started.md).

O fluxo de trabalho de buildout será disposto sobre o Kubernetes um cluster de Big Data do SQL Server totalmente funcional que inclui todos os componentes descritos no artigo [Visão geral](big-data-cluster-overview.md). O fluxo de trabalho de inicialização cria primeiro o serviço do controlador e, após ele ser implantado, o serviço do controlador coordenará a instalação e a configuração do restante da parte dos serviços referentes a mestre, computação, dados e pools de armazenamento.

## <a name="managing-the-cluster-through-the-controller-service"></a>Gerenciando o cluster por meio do serviço de controlador

Você pode gerenciar o cluster por meio do serviço de controlador usando os comandos de **azdata**. Se você implantar objetos de Kubernetes adicionais, como pods, no mesmo namespace, eles não serão gerenciados nem monitorados pelo serviço do controlador. Você também pode usar comandos **kubectl** para gerenciar o cluster no nível de Kubernetes. Para saber mais, confira [Monitoramento e solução de problemas de clusters de Big Data do SQL Server](cluster-troubleshooting-commands.md).

O controlador e os objetos de Kubernetes (conjuntos com estado, pods, segredos, etc.) criados para um cluster de Big Data residem em um namespace dedicado do Kubernetes. O serviço de controlador receberá permissão do administrador de cluster do Kubernetes para gerenciar todos os recursos dentro desse namespace.  A política de RBAC para esse cenário é configurada automaticamente como parte da implantação do cluster inicial usando **azdata**.

### <a name="azdata"></a>azdata

**azdata** é um utilitário de linha de comando escrito em Python que permite aos administradores de cluster inicializar e gerenciar clusters de Big Data por meio das APIs REST expostas pelo serviço do controlador.

## <a name="controller-service-security"></a>Segurança do serviço de controlador

Toda a comunicação com o serviço do controlador é conduzida por meio de uma API REST por HTTPS. Um certificado autoassinado será gerado automaticamente para você no momento da inicialização. 

A autenticação para o ponto de extremidade de serviço do controlador é baseada em nome de usuário e senha. Essas credenciais são provisionadas no momento da inicialização do cluster usando a entrada para variáveis de ambiente `CONTROLLER_USERNAME` e `CONTROLLER_PASSWORD`.

> [!NOTE]
> Você deve fornecer uma senha que esteja em conformidade com os [Requisitos de complexidade de senha do SQL Server](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de Big Data do SQL Server, confira os seguintes recursos:

- [O que são os clusters de Big Data do SQL Server 2019?](big-data-cluster-overview.md)
- [Workshop: Arquitetura de clusters de Big Data do Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
