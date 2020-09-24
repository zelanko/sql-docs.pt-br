---
title: Configurar a segurança de dados avançada
titleSuffix: Azure Arc
description: Configurar a segurança de dados avançada para a instância do SQL Server habilitado para o Azure Arc
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: a51ec53b5b5e928bd19dd66cb1ac6a8da162e817
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90990369"
---
# <a name="configure-advanced-data-security-for-azure-arc-enabled-sql-server-instance"></a>Configurar a segurança de dados avançada para a instância do SQL Server habilitado para o Azure Arc

Você pode habilitar a segurança de dados avançada para suas instâncias do SQL Server locais seguindo estas etapas.

## <a name="prerequisites"></a>Pré-requisitos

* Sua instância do SQL Server é integrada ao SQL Server habilitado para o Arc. Siga estas instruções para [integrar sua instância do SQL Server ao SQL Server habilitado para o Arc](connect.md).

* Sua conta de usuário recebe uma das [Funções da Central de Segurança (RBAC)](/azure/security-center/security-center-permissions)

## <a name="create-a-log-analytics-workspace"></a>Criar um workspace do Log Analytics

1. Procure o tipo de recurso __workspaces do Log Analytics__ e adicione outro por meio da folha de criação.

   ![Criar novo workspace](media/configure-advanced-data-security/create-new-log-analytics-workspace.png)

   > [!NOTE]
   > Um workspace do Log Analytics pode ser usado em qualquer região, portanto, se você já tiver um, poderá usá-lo. Mas é recomendado criá-lo na mesma região em que seu recurso __Computador – Azure Arc__ é criado.

1. Acesse a página de visão geral do recurso workspace do Log Analytics e selecione “Windows, Linux e outras fontes”. Copie a ID do workspace e a chave primária para uso posterior.

   ![Folha do workspace do Log Analytics](media/configure-advanced-data-security/log-analytics-workspace-blade.png)

## <a name="install-microsoft-monitoring-agent-mma"></a>Instalar o MMA (Microsoft Monitoring Agent)

A próxima etapa só será necessária se você ainda não tiver configurado o agente MMA no computador remoto.

1. Selecione o recurso __Computador – Azure Arc__ do servidor virtual ou físico no qual a instância do SQL Server está instalada e adicione a extensão __Microsoft Monitoring Agent – Azure Arc__ usando o recurso **Extensões**. Quando for solicitado que você configure o workspace do Log Analytics, use a ID do workspace e a chave primária que você salvou na etapa anterior.

   ![Instalar o MMA](media/configure-advanced-data-security/install-mma-extension.png)

1. Depois que a validação for realizada com sucesso, clique em **Criar** para iniciar o fluxo de trabalho de implantação da Extensão MMA do Arc. Quando a implantação for concluída, o status será atualizado para **Bem-sucedido**.

1. Para obter mais detalhes, confira [Gerenciamento de extensão com o Azure Arc](/azure/azure-arc/servers/manage-vm-extensions)

## <a name="enable-advanced-data-security"></a>Habilitar a segurança de dados avançada

Em seguida, você precisará habilitar a segurança de dados avançada para a instância do SQL Server.

1. Acesse a Central de Segurança e abra a página **Preços e configurações** na barra lateral.

1. Selecione o workspace que você configurou para a extensão MMA na etapa anterior

1. Selecione **Padrão**. Verifique se a opção de **SQL Servers no Computador (Versão prévia)** está habilitada.

   ![Atualizar o workspace](media/configure-advanced-data-security/upgrade-log-analytics-workspace.png)

 > [!NOTE]
   > A primeira verificação para gerar a avaliação de vulnerabilidades ocorrerá em até 24 horas depois que a segurança de dados avançada for habilitada. Depois disso, as verificações automáticas serão executadas todas as semanas aos domingos.

## <a name="explore"></a>Explorar

Explore as anomalias e as ameaças de segurança na Central de Segurança do Azure.

1. Abra o recurso SQL Server – Azure Arc e selecione **Segurança** no menu à esquerda. para ver as recomendações e os alertas dessa instância.

   ![Selecionar o título de segurança](media/configure-advanced-data-security/security-heading-sql-server-arc.png)

1. Clique em uma das recomendações para ver os detalhes da vulnerabilidade na __Central de Segurança__.

   ![Relatório de vulnerabilidades](media/configure-advanced-data-security/vulnerabilities-report.png)

1. Clique em qualquer alerta de segurança para obter detalhes completos e explorar mais o ataque no [Azure Sentinel](https://docs.microsoft.com/azure/sentinel/overview). O diagrama a seguir é um exemplo do alerta de força bruta.

   ![Alerta de força bruta](media/configure-advanced-data-security/brute-force-alert.png)

1. Clique em **Executar ação** para mitigar o alerta.

   ![Mitigação de alerta](media/configure-advanced-data-security/brute-force-alert-mitigation.png)

> [!NOTE]
> O link geral da __Central de Segurança__ na parte superior da página não usa a URL do portal de Versão prévia para que os recursos __SQL Server – Azure Arc__ não fiquem visíveis lá. É recomendado seguir os links das recomendações ou dos alertas individuais.

## <a name="next-steps"></a>Próximas etapas

Você pode continuar investigando os alertas de segurança e os ataques usando o [Azure Sentinel](/azure/sentinel/overview). Siga estas instruções para [integrar o Azure Sentinel](/azure/sentinel/connect-data-sources).
