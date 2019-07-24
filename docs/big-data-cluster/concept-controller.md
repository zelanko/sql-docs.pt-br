---
title: O que é o controlador?
titleSuffix: SQL Server big data clusters
description: Este artigo descreve o controlador de um cluster SQL Server 2019 Big Data (versão prévia).
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e984c3dced4bde713ac98d67c22481e54491cd68
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419541"
---
# <a name="what-is-the-controller-on-a-sql-server-big-data-cluster"></a>O que é o controlador em um cluster SQL Server Big Data?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

O controlador hospeda a lógica principal para implantar e gerenciar um cluster Big Data. Ele cuida de todas as interações com o kubernetes, SQL Server instâncias que fazem parte do cluster e outros componentes, como HDFS e Spark.

O serviço de controlador fornece a seguinte funcionalidade básica:

- Gerenciar ciclo de vida do cluster: inicialização do cluster & excluir, atualizar configurações
- Gerenciar instâncias de SQL Server mestre
- Gerenciar pools de computação, dados e armazenamento
- Expor as ferramentas de monitoramento para observar o estado do cluster
- Expor ferramentas de solução de problemas para detectar e reparar problemas inesperados
- Gerenciar a segurança do cluster:
  - Garantir pontos de extremidade de cluster seguros
  - Gerenciar usuários e funções
  - Configurar credenciais para comunicação dentro do cluster

## <a name="deploying-the-controller-service"></a>Implantando o serviço do controlador

O controlador é implantado e hospedado no mesmo namespace kubernetes em que o cliente deseja criar um cluster Big Data. Esse serviço é instalado por um administrador do kubernetes durante a inicialização do cluster, usando o utilitário de linha de comando **azdata** . Para obter mais informações, consulte Introdução [aos clusters de Big data de SQL Server](deploy-get-started.md).

O fluxo de trabalho de Build out fará o layout do kubernetes um cluster SQL Server Big Data totalmente funcional que inclui todos os componentes descritos no artigo de [visão geral](big-data-cluster-overview.md) . O fluxo de trabalho de inicialização cria primeiro o serviço do controlador e, depois que isso é implantado, o serviço do controlador coordenará a instalação e a configuração do restante da parte dos serviços dos pools mestre, de computação, de dados e de armazenamento.

## <a name="managing-the-cluster-through-the-controller-service"></a>Gerenciando o cluster por meio do serviço de controlador

Você pode gerenciar o cluster por meio do serviço de controlador usando os comandos **azdata** . Se você implantar objetos kubernetes adicionais como pods no mesmo namespace, eles não serão gerenciados ou monitorados pelo serviço do controlador. Você também pode usar comandos **kubectl** para gerenciar o cluster no nível de kubernetes. Para obter mais informações, consulte [monitoramento e solução de problemas SQL Server clusters de Big data](cluster-troubleshooting-commands.md).

O controlador e os objetos kubernetes (conjuntos com estado, pods, segredos, etc.) criados para um cluster Big Data residem em um namespace kubernetes dedicado. O serviço de controlador receberá permissão do administrador de cluster kubernetes para gerenciar todos os recursos dentro desse namespace.  A política de RBAC para esse cenário é configurada automaticamente como parte da implantação de cluster inicial usando o **azdata**.

### <a name="azdata"></a>azdata

**azdata** é um utilitário de linha de comando escrito em Python que permite que os administradores de cluster inicializem e gerenciem Big data clusters por meio das APIs REST expostas pelo serviço do controlador.

## <a name="controller-service-security"></a>Segurança do serviço do controlador

Toda a comunicação com o serviço do controlador é conduzida por meio de uma API REST por HTTPS. Um certificado autoassinado será gerado automaticamente para você no momento da inicialização. 

A autenticação para o ponto de extremidade de serviço do controlador é baseada em nome de usuário e senha. Essas credenciais são provisionadas no momento da inicialização do cluster usando a entrada para variáveis `CONTROLLER_USERNAME` de `CONTROLLER_PASSWORD`ambiente e.

> [!NOTE]
> Você deve fornecer uma senha que esteja em conformidade com [os requisitos de complexidade de senha do SQL Server](https://docs.microsoft.com/sql/relational-databases/security/password-policy?view=sql-server-2017).

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre os clusters de Big Data SQL Server, confira os seguintes recursos:

- [O que são SQL Server clusters de Big Data 2019?](big-data-cluster-overview.md)
- [Oficina Arquitetura de clusters de Big Data Microsoft SQL Server](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
