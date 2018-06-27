---
title: Adicionar um Trabalho do SSIS Scale Out com o Gerenciador do Scale Out | Microsoft Docs
description: Este artigo descreve como adicionar um Trabalho do SSIS Scale Out em um ambiente do Scale Out existente usando o Gerenciador do Scale Out.
ms.custom: performance
ms.date: 12/19/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: f4f9f055cefe4e3212066ea06868e88e399eaf36
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35335900"
---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>Adicionar um Trabalho do Scale Out com o Gerenciador do Scale Out

O Gerenciador do Integration Services Scale Out simplifica o processo de adição de um Trabalho do Scale Out ao ambiente existente do Scale Out. 

Siga estas etapas para adicionar um Trabalho do Scale Out à sua topologia do Scale Out:

## <a name="1-install-scale-out-worker"></a>1. Instalar Trabalho do Scale Out
No assistente de instalação do SQL Server, selecione Integration Services e Trabalho do Scale Out na página **Seleção de Recursos**. 
![Trabalho de Seleção de Recurso](media/feature-select-worker.PNG)

Na página **Configuração do Integration Services Scale Out – Nó de Trabalho**, clique em **Avançar** para ignorar a configuração neste momento e usar o **Gerenciador do Scale Out** para fazer a configuração após a instalação.

Conclua o assistente de instalação.

## <a name="2-open-the-firewall-on-the-scale-out-master-computer"></a>2. Abrir o firewall no computador do Mestre do Scale Out
Abra a porta especificada durante a instalação do Mestre do Scale Out (8391, por padrão) e a porta do SQL Server (1433, por padrão) no Firewall do Windows no computador do Mestre do Scale Out.

## <a name="3-add-a-scale-out-worker-with-scale-out-manager"></a>3. Adicionar um Trabalho do Scale Out com o Gerenciador do Scale Out
Execute o SQL Server Management Studio como administrador e conecte-se à instância do SQL Server do Mestre do Scale Out.

No Pesquisador de Objetos, clique com o botão direito do mouse em **SSISDB** e selecione **Gerenciar Scale Out**. 

![Gerenciar Scale Out](media/manage-scale-out.PNG)

Na caixa de diálogo **Gerenciador do Scale Out**, alterne para **Gerenciador do Trabalho**. Selecione **+** e siga as instruções da caixa de diálogo **Conectar Trabalho**. 

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte [Gerenciador do Scale Out](integration-services-ssis-scale-out-manager.md).