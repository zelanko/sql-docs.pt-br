---
title: SSIS (SQL Server Integration Services) Scale Out | Microsoft Docs
description: Este artigo fornece uma visão geral do recurso SSIS (SQL Server Integration Services) Scale Out, que oferece execução de alto desempenho de pacotes SSIS
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0eb8532c10069f50283e13ab997560330dfa5a1c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47715364"
---
# <a name="integration-services-ssis-scale-out"></a>Expansão do Integration Services (SSIS)
O SSIS (SQL Server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]) Scale Out fornece execução de alto desempenho de pacotes do SSIS com a distribuição de execuções de pacote em vários computadores. Depois de configurar o Scale Out, você pode executar várias execuções de pacote em paralelo, no modo de expansão, por meio do SSMS (SQL Server Management Studio).

## <a name="components"></a>Componentes
O [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out consiste em um Mestre do [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out e um ou vários Trabalhos do [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale Out.

-   O Mestre de Expansão é responsável pelo gerenciamento da Expansão e recebe solicitações de execução de pacote dos usuários. Para obter mais informações, consulte [Mestre do Scale Out](integration-services-ssis-scale-out-master.md).

-   Os Trabalhos do Scale Out efetuam pull de tarefas de execução no Mestre do Scale Out e executam os pacotes. Para obter mais informações, consulte [Trabalho do Scale Out](integration-services-ssis-scale-out-worker.md).

## <a name="configuration-options"></a>Opções de configuração
Defina o Scale Out nas seguintes configurações:

-   **Em um único computador**, em que um Mestre do Scale Out e um Trabalho do Scale Out são executados lado a lado no mesmo computador.

-   **Em vários computadores**, em que cada Trabalho do Scale Out está em um computador diferente.

## <a name="what-you-can-do"></a>O que você pode fazer
Depois de configurar o Scale Out, você pode fazer o seguinte:

-   Executar vários pacotes implantados no catálogo do SSISDB em paralelo. Para obter mais informações, consulte [Executar pacotes no Scale Out](run-packages-in-integration-services-ssis-scale-out.md).

-   Gerenciar a topologia do Scale Out no aplicativo Gerenciador do Scale Out. Para obter mais informações, consulte [Gerenciador do Integration Services Scale Out](integration-services-ssis-scale-out-manager.md).

## <a name="next-steps"></a>Próximas etapas
-   [Introdução ao SSIS (Integration Services) Scale Out em um único computador](get-started-with-ssis-scale-out-onebox.md)

-   [Passo a passo: configurar a Expansão do Integration Services](walkthrough-set-up-integration-services-scale-out.md)
