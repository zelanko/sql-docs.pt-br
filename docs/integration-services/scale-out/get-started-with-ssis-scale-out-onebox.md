---
title: "Introdução ao SSIS Scale Out em um único computador | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8514cd548b003a39bf198b83b6b80d775a55384b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>Introdução ao SSIS (Integration Services) Scale Out em um único computador
Esta seção fornece as diretrizes de configuração do Integration Services Scale Out em um ambiente onebox com configurações padrão.

## <a name="1-install-sql-server-features"></a>1. Instalar recursos do SQL Server
No assistente de instalação do SQL Server, selecione Serviços de Mecanismo de Banco de Dados, Integration Services e Mestre do Scale Out e Trabalho do Scale Out na página **Seleção de Recursos**.

![Seleção de Recurso Onebox 1](media/feature-select-onebox1.PNG)

![Seleção de Recurso Onebox 2](media/feature-select-onebox2.PNG)

Na página **Configuração do Servidor**, basta clicar em "Avançar" para usar contas de serviço padrão e tipos de inicialização.

Na página **Configuração do mecanismo de banco de dados**, selecione "**Modo Misto**"e clique no botão "**Adicionar Usuário Atual**". 

![Configuração do Mecanismo](media/engine-config.PNG)

Em uma das páginas **Configuração do Integration Services Scale Out – Nó Mestre** e **Configuração do Integration Services Scale Out – Nó de Trabalho**, basta clicar em "Avançar" para aplicar as configurações padrão de porta e certificados.

Conclua o Assistente de instalação do SQL Server.

## <a name="2-install-sql-server-management-studio"></a>2. Instalar o SQL Server Management Studio

[Baixe](../../ssms/download-sql-server-management-studio-ssms.md) o SQL Server Management Studio e instale-o.

## <a name="3-enable-scale-out"></a>3. Habilitar Scale Out
Abra o SSMS e conecte-se a uma instância local do SQL Server.
Clique com o botão direito do mouse em **Catálogos do Integration Services** no Pesquisador de Objetos e selecione **Criar Catálogo**.

Na caixa de diálogo **Criar Catálogo**, a opção **Habilitar este servidor como o mestre do SSIS Scale Out** é selecionada por padrão. Basta criar o catálogo como de costume. 

## <a name="4-enable-scale-out-worker"></a>4. Habilitar o Trabalho do Scale Out
No SSMS, clique com o botão direito do mouse em **SSISDB** e selecione **Gerenciar Scale Out...** . ![Gerenciar Scale Out](media/manage-scale-out.PNG)

O Gerenciador do Integration Services Scale Out aparecerá. Você pode gerenciar o Scale Out com ele. Para obter mais informações, consulte [Gerenciador do Integration Services Scale Out](integration-services-ssis-scale-out-manager.md).

Para habilitar o Trabalho do Scale Out, mude para o **Gerenciador de Trabalho** e selecione o trabalho que você deseja habilitar. O trabalhador está originalmente desabilitado. Clique em **Habilitar Trabalho** para habilitá-lo.

## <a name="5-run-packages-in-scale-out"></a>5. Executar pacotes em Expansão
Agora, você está pronto para executar pacotes SSIS no Scale Out. Veja [Executar pacotes no SSIS (Integration Services) Scale Out](run-packages-in-integration-services-ssis-scale-out.md).


Para adicionar mais trabalhos do Scale Out, consulte [Adicionar um Trabalho do Scale Out com o Gerenciador do Scale Out](add-scale-out-worker.md).
