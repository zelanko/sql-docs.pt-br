---
title: Adicionar um Trabalho do SSIS Scale Out com o Gerenciador do Scale Out | Microsoft Docs
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
ms.openlocfilehash: ef11448d03bd188aaea425225312af9f681f530c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>Adicionar um Trabalho do Scale Out com o Gerenciador do Scale Out

O Gerenciador do Scale Out do Integration Services reduz significativamente a complexidade ao adicionar o Trabalho do Scale Out ao ambiente do Scale Out existente. 

As etapas a seguir permitem que você adicione um Trabalho do Scale Out à sua topologia do Scale Out:

## <a name="1-install-scale-out-worker"></a>1. Instalar Trabalho do Scale Out
No assistente de instalação do SQL Server, selecione Integration Services e Trabalho do Scale Out na página **Seleção de Recursos**. 
![Trabalho de Seleção de Recurso](media/feature-select-worker.PNG)

Na página **Configuração do Scale Out Integration Services – nó de trabalho**, você pode simplesmente clicar em "Avançar" para ignorar a configuração aqui e usar o **Gerenciador do Scale Out** para fazer a configuração após a instalação.

Conclua o assistente de instalação.

## <a name="2-open-firewall-on-scale-out-master-computer"></a>2. Abrir o firewall no computador do Mestre do Scale Out
Abra a porta especificada durante a instalação do Mestre do Scale Out (8391, por padrão) e a porta do SQL Server (1433, por padrão), usando o Firewall do Windows no computador do Mestre do Scale Out.

## <a name="3-add-scale-out-worker-with-scale-out-manager"></a>3. Adicionar um Trabalho do Scale Out com o Gerenciador do Scale Out
Execute o SQL Server Management Studio como administrador e conecte-se à instância do SQL Server do Mestre do Scale Out.

Clique com o botão direito do mouse em **SSISDB** no Pesquisador de Objetos e selecione **Gerenciar Scale Out...**. 

![Gerenciar Scale Out](media/manage-scale-out.PNG)

No **Gerenciador do Scale Out** que aparece, mude para o **Gerenciador do Trabalho**. Clique em no botão "+" e siga as instruções na caixa de diálogo Conectar-se ao Trabalho. Para obter detalhes, consulte [Gerenciador do Scale Out](integration-services-ssis-scale-out-manager.md).
