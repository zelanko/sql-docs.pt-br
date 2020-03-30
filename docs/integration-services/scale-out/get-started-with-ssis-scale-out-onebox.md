---
title: Introdução ao SSIS Scale Out em um único computador | Microsoft Docs
description: Este artigo mostra tudo o que você precisa saber para começar a usar o SSIS Scale Out em um único computador
ms.custom: performance
ms.date: 12/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: a2d6929277b7d024e45daaefd5cb41dccd495c63
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68082160"
---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>Introdução ao SSIS (Integration Services) Scale Out em um único computador

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Esta seção fornece diretrizes de configuração do Integration Services Scale Out em um ambiente de um único computador com as configurações padrão.

## <a name="1-install-sql-server-features"></a>1. Instalar recursos do SQL Server
No assistente de instalação do SQL Server, na página **Seleção de Recursos**, selecione os seguintes itens:
-   Serviços do Mecanismo de Banco de Dados
-   Integration Services
    -   Mestre do Scale Out
    -   Trabalho do Scale Out

![A primeira metade da lista de Seleção de Recursos](media/feature-select-onebox1.PNG)

![A segunda metade da lista de Seleção de Recursos](media/feature-select-onebox2.PNG)

Na página **Configuração do Servidor**, clique em **Avançar** para aceitar as contas de serviço e os tipos de inicialização padrão.

Na página **Configuração do Mecanismo de Banco de Dados**, selecione **Modo Misto** e clique em **Adicionar Usuário Atual**. 

![Configuração do Mecanismo](media/engine-config.PNG)

Nas páginas **Configuração do Integration Services Scale Out – Nó Mestre** e **Configuração do Integration Services Scale Out – Nó de Trabalho**, clique em **Avançar** para aceitar as configurações padrão da porta e dos certificados.

Conclua o Assistente de instalação do SQL Server.

## <a name="2-install-sql-server-management-studio"></a>2. Instale o SQL Server Management Studio

Baixe e instale o [SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md).

## <a name="3-enable-scale-out"></a>3. Habilitar Scale Out
Abra o SSMS e conecte-se a uma instância local do SQL Server.
No Pesquisador de Objetos, clique com o botão direito do mouse em **Catálogos do Integration Services** e selecione **Criar Catálogo**.

Na caixa de diálogo **Criar Catálogo**, a opção **Habilitar este servidor como o mestre do SSIS Scale Out** está selecionada por padrão.

## <a name="4-enable-a-scale-out-worker"></a>4. Habilitar um Trabalho do Scale Out
No SSMS, clique com o botão direito do mouse em **SSISDB** e selecione **Gerenciar Scale Out**. 

![Gerenciar Scale Out](media/manage-scale-out.PNG)

O aplicativo Gerenciador do Integration Services Scale Out será aberto. Para obter mais informações, consulte [Gerenciador do Scale Out](integration-services-ssis-scale-out-manager.md).

Para habilitar um Trabalho do Scale Out, alterne para o **Gerenciador do Trabalho** e selecione o trabalho que deseja habilitar. Os trabalhos estão desabilitados por padrão. Clique em **Habilitar Trabalho** para habilitar o trabalho selecionado.

## <a name="5-run-packages-in-scale-out"></a>5. Executar pacotes em Expansão
Agora, você está pronto para executar pacotes do SSIS no Scale Out. Para obter mais informações, consulte [Executar pacotes no SSIS (Integration Services) Scale Out](run-packages-in-integration-services-ssis-scale-out.md).

## <a name="next-steps"></a>Próximas etapas
-   [Adicionar um Trabalho do Scale Out com o Gerenciador do Scale Out](add-scale-out-worker.md).
