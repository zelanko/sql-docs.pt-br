---
title: Gerenciador do SQL Server Integration Services Scale Out | Microsoft Docs
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
ms.openlocfilehash: 84fe58d4dc7894728c43cb19d17d3444b5b84820
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-scale-out-manager"></a>Gerenciador do Integration Services Scale Out

O Gerenciador do Scale Out é uma ferramenta de gerenciamento que permite que você gerencie a sua topologia do SSIS Scale Out completa em um único local. Ele remove a carga decorrente de operar em vários computadores e lidar com comandos TSQL. 

Há duas maneiras para disparar o Gerenciador do Scale Out.

## <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1. Abrir o Gerenciador do Scale Out do SQL Server Management Studio
Abra o SQL Server Management Studio e conecte-se à instância do SQL Server do Mestre do Scale Out.

Clique com o botão direito do mouse em **SSISDB** no Pesquisador de Objetos e selecione **Gerenciar Scale Out...**. ![Gerenciar Scale Out](media/manage-scale-out.PNG)

> [!NOTE]
> É recomendável executar o SQL Server Management Studio como administrador, pois operações de gerenciamento do Scale Out como "adicionar um trabalho de Scale Out" exigirão privilégio administrativo.


## <a name="2-open-scale-out-manager-by-runing-ismanagerexe-directly"></a>2. Abrir o Gerenciador do Scale Out executando o ISManager.exe diretamente

O ISManager.exe está localizado em %SystemDrive%\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn\Management. Clique com o botão direito do mouse em **ISManager.exe** e selecione "Executar como administrador". 

Depois que ele for aberto, você precisará inserir o nome do SQL Server do Mestre do Scale Out e conectar-se a ele antes de gerenciar seu Scale Out.

![Conexão do Portal](media/portal-connect.PNG)

O Gerenciador do Scale Out fornece várias funcionalidades, conforme descrito a seguir. 

## <a name="enable-scale-out"></a>Habilitar Scale Out
Depois de se conectar ao SQL Server, se o Scale Out não estiver habilitado, você poderá clicar no botão "Habilitar" para habilitá-lo.

![Portal Habilitar o Scale Out](media/portal-enable-scale-out.PNG) 
## <a name="view-scale-out-master-status"></a>Exibir status do Mestre do Scale Out
O status do Mestre do Scale Out será mostrado na página **Painel**.

![Painel do Portal](media/portal-dashboard.PNG)
## <a name="view-scale-out-worker-status"></a>Exibir o status do Trabalho do Scale Out
O status do Trabalho do Scale Out é mostrado na página **Gerenciador do Trabalho**. Você pode clicar em cada trabalho para ver o status individual.

![Portal Gerenciador do Trabalho](media/portal-worker-manager.PNG)

## <a name="add-scale-out-worker"></a>Adicionar Trabalho do Scale Out
Para adicionar um Trabalho do Scale Out, clique no botão "+" na parte inferior da lista de Trabalho do Scale Out. 

Insira o nome do computador do Trabalho do Scale Out que você deseja adicionar e clique em "Validar". O Gerenciador do Scale Out verificará se o usuário atual tem acesso para os repositórios de certificados nos computadores do Mestre do Scale Out e do Trabalho do Scale Out.

![Conectar Trabalho](media/connect-worker.PNG)

Se a validação for aprovada, o Gerenciador do Scale Out tentará ler arquivo de configuração de seu trabalho e obter a impressão digital do certificado do trabalho. Para obter mais informações, consulte [Trabalho do Scale Out](integration-services-ssis-scale-out-worker.md). Se ele não é capaz de ler o arquivo de configuração de trabalho, há duas formas alternativas para fornecer o certificado do trabalho. 

Você pode inserir a impressão digital do certificado do trabalho diretamente 

![Certificado do trabalho 1](media/portal-cert1.PNG)

ou fornecer o arquivo de certificado. 

![Certificado do trabalho 2](media/portal-cert2.PNG)

Depois de coletar todas as informações, o Gerenciador do Scale Out fornecerá as ações a serem executadas. Normalmente, isso inclui a instalação do certificado, a atualização do arquivo de configuração de trabalho e a reinicialização do serviço do trabalho. 

![Portal Adicionar Confirmação 1](media/portal-add-confirm1.PNG)

Caso o certificado do trabalho não esteja acessível, você precisará atualizá-lo manualmente por conta própria e reiniciar o serviço do trabalho.

![Portal Adicionar Confirmação 2](media/portal-add-confirm2.PNG)

Clique na caixa de seleção de confirmação e comece a adicionar o Trabalho do Scale Out.

## <a name="delete-scale-out-worker"></a>Excluir o Trabalho do Scale Out
Para excluir um Trabalho do Scale Out, selecione-o e clique no botão "-" na parte inferior da lista de Trabalhos do Scale Out.


## <a name="enabledisable-scale-out"></a>Habilitar/Desabilitar o Scale Out
Para habilitar ou desabilitar um Trabalho do Scale Out, selecione-o e clique no botão "Desabilitar o Trabalho" ou "Habilitar o Trabalho". O status do trabalho no Gerenciador do Scale Out mudará adequadamente se o trabalho não estiver offline.

## <a name="edit-scale-out-worker-description"></a>Editar descrição de Trabalho do Scale Out
Para editar a descrição de um Trabalho do Scale Out, selecione-o e clique no botão "Editar". Depois de terminar de editar, clique no botão "Salvar".

![Portal Salvar o Trabalho](media/portal-save-worker.PNG)

