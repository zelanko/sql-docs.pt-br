---
title: "Adicionar um SSIS expansão trabalho com o Gerenciador de expansão | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b769236330941a107865a0b133961bce5bf6b85b
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>Adicionar uma expansão trabalho com o Gerenciador de expansão

Escala Out Gerenciador de serviços de integração libera significativamente a complexidade para adicionar escala Out trabalhador para expansão ambiente existente. 

As etapas a seguir permitem que você adicione um trabalho de fora de escala para sua topologia de expansão:

## <a name="1-install-scale-out-worker"></a>1. Instalar o trabalho de expansão
No Assistente de instalação do SQL Server, selecione Integration Services e escala Out trabalhador no **seleção de recursos** página. 
![Trabalho de Seleção de Recurso](media/feature-select-worker.PNG)

Sobre o **escala Out configuração do Integration Services - nó de trabalho** página, você pode simplesmente clicar em "Avançar" para ignorar configuração aqui e use **gerenciador fora de escala** para fazer a configuração após a instalação.

Conclua o Assistente de instalação.

## <a name="2-open-firewall-on-scale-out-master-computer"></a>2. Abra o firewall no computador de escala Out mestre
Abra a porta especificada durante a instalação de escala Out mestre (8391, por padrão) e a porta do SQL Server (1433, por padrão), usando o Firewall do Windows no computador escala Out mestre.

## <a name="3-add-scale-out-worker-with-scale-out-manager"></a>3. Adicionar expansão trabalho com o Gerenciador de expansão
Executar o SQL Server Management Studio como administrador e conecte-se à instância do SQL Server do mestre de fora da escala.

Clique com botão direito **SSISDB** no Pesquisador de objetos e selecione **gerenciar expansão...** . 

![Gerenciar a expansão](media/manage-scale-out.PNG)

Na ser exibido para cima **escala Out Manager**, alterne para o **Gerenciador de trabalho**. Clique em "+" botão e siga as instruções na caixa de diálogo Conecte-se o trabalho. Para obter detalhes, consulte [gerenciador fora de escala](integration-services-ssis-scale-out-manager.md).

