---
title: "Introdução à escala SSIS Out em um único computador | Microsoft Docs"
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
ms.openlocfilehash: 7175c63be4c0e15e50f2020f75d283ac0e3dfdbf
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="get-started-with-integration-services-ssis-scale-out-on-a-single-computer"></a>Introdução ao Integration Services (SSIS) expansão em um único computador
Esta seção fornece as diretrizes de configuração de integração de serviços de expansão em um ambiente de uma caixa com as configurações padrão.

## <a name="1-install-sql-server-features"></a>1. Instalar recursos do SQL Server
No Assistente de instalação do SQL Server, selecione Serviços de mecanismo de banco de dados, Integration Services, escala Out mestre e escala Out trabalhador no **seleção de recursos** página.

![Recurso Onebox selecione 1](media/feature-select-onebox1.PNG)

![Recurso selecione Onebox 2](media/feature-select-onebox2.PNG)

Sobre o **configuração do servidor** página, basta clicar em "Avançar" para usar contas de serviço padrão e tipos de inicialização.

Sobre o **configuração do mecanismo de banco de dados** página, selecione "**modo misto**"e clique em"**adicionar usuário atual**" botão. 

![Configuração do mecanismo](media/engine-config.PNG)

Um o **escala Out configuração do Integration Services - mestre nó** e **escala Out configuração do Integration Services - trabalho nó** páginas, basta clicar em "Avançar" para aplicar as configurações padrão de porta e certificados.

Conclua o Assistente de instalação do SQL Server.

## <a name="2-install-sql-server-management-studio"></a>2. Instalar o SQL Server Management Studio

[Baixar](../../ssms/download-sql-server-management-studio-ssms.md) SQL Server Management Studio e instalá-lo.

## <a name="3-enable-scale-out"></a>3. Habilitar de expansão
Abra o SSMS e conecte-se à instância local do Sql Server.
Clique com botão direito **catálogos do Integration Services** no Pesquisador de objetos e selecione **criar catálogo**.

No **criar catálogo** caixa de diálogo, **habilitar este servidor como o mestre de expansão do SSIS** é selecionada por padrão. Basta crie o catálogo como de costume. 

## <a name="4-enable-scale-out-worker"></a>4. Habilitar o trabalho de expansão
No SSMS, clique com botão direito **SSISDB** e selecione **gerenciar expansão...** . 
![Gerenciar a expansão](media/manage-scale-out.PNG)

O Integration Services escala Out Manager será exibida. Você pode gerenciar a expansão com ele. Para obter mais informações, consulte [escala Out Gerenciador de serviços de integração](integration-services-ssis-scale-out-manager.md).

Para habilitar o trabalho de fora de escala, alterne para o **Gerenciador de trabalho** e selecione o trabalho que você deseja habilitar. O trabalhador originalmente está desabilitado. Clique em **habilitar trabalho** para habilitá-lo.

## <a name="5-run-packages-in-scale-out"></a>5. Executar pacotes em Expansão
Agora, você está pronto para executar pacotes SSIS em expansão. Consulte [executar pacotes do Integration Services (SSIS) expansão](run-packages-in-integration-services-ssis-scale-out.md).


Para adicionar mais trabalhadores de expansão, consulte [adicionar um trabalhador escala Out com o Gerenciador de fora da escala](add-scale-out-worker.md).
