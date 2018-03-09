---
title: Gerenciador do SQL Server Integration Services Scale Out | Microsoft Docs
ms.description: This article describes the Scale Out Manager tool which you can use to manager SSIS Scale Out
ms.custom: 
ms.date: 12/19/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e0180a4820781e19b728ddb1157db2010a8988ec
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="integration-services-scale-out-manager"></a>Gerenciador do Integration Services Scale Out

O Gerenciador do Scale Out é uma ferramenta de gerenciamento que permite gerenciar toda a topologia do SSIS Scale Out em um único aplicativo. Ele remove a carga de realizar tarefas de gerenciamento e executar comandos Transact-SQL em vários computadores.

## <a name="open-scale-out-manager"></a>Abrir o Gerenciador do Scale Out

Há duas maneiras de abrir o Gerenciador do Scale Out.

### <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1. Abrir o Gerenciador do Scale Out do SQL Server Management Studio
Abra o SSMS (SQL Server Management Studio) e conecte-se à instância do SQL Server do Mestre do Scale Out.

No Pesquisador de Objetos, clique com o botão direito do mouse em **SSISDB** e selecione **Gerenciar Scale Out**.

![Gerenciar Scale Out](media/manage-scale-out.PNG)

> [!NOTE]
> Recomendamos executar o SSMS como administrador, pois algumas operações de gerenciamento do Scale Out, como a adição de um Trabalho do Scale Out, exigem privilégio administrativo.

### <a name="2-open-scale-out-manager-by-running-ismanagerexe"></a>2. Abrir o Gerenciador do Scale Out executando ISManager.exe

Localize `ISManager.exe` em `%SystemDrive%\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn\Management`. Clique com o botão direito do mouse em **ISManager.exe** e selecione **Executar como administrador**. 

Depois de abrir o Gerenciador do Scale Out, insira o nome da instância do SQL Server do Mestre do Scale Out e conecte-se a ela para gerenciar seu ambiente do Scale Out.

![Conexão do Portal](media/portal-connect.PNG)

## <a name="tasks-available-in-scale-out-manager"></a>Tarefas disponíveis no Gerenciador do Scale Out
No Gerenciador do Scale Out, você pode fazer o seguinte:

### <a name="enable-scale-out"></a>Habilitar Scale Out
Depois de se conectar ao SQL Server, se o Scale Out não estiver habilitado, você poderá selecionar **Habilitar** para habilitá-lo.

![Portal Habilitar o Scale Out](media/portal-enable-scale-out.PNG) 

### <a name="view-scale-out-master-status"></a>Exibir status do Mestre do Scale Out
O status do Mestre do Scale Out será mostrado na página **Painel**.

![Painel do Portal](media/portal-dashboard.PNG)

### <a name="view-scale-out-worker-status"></a>Exibir o status do Trabalho do Scale Out
O status do Trabalho do Scale Out é mostrado na página **Gerenciador do Trabalho**. Selecione cada trabalho para ver o status individual.

![Portal Gerenciador do Trabalho](media/portal-worker-manager.PNG)

### <a name="add-a-scale-out-worker"></a>Adicionar um Trabalho do Scale Out
Para adicionar um Trabalho do Scale Out, selecione **+** na parte inferior da lista do Trabalho do Scale Out. 

Insira o nome do computador do Trabalho do Scale Out que você deseja adicionar e clique em **Validar**. O Gerenciador do Scale Out verifica se o usuário atual tem acesso aos repositórios de certificados nos computadores do Mestre do Scale Out e do Trabalho do Scale Out

![Conectar Trabalho](media/connect-worker.PNG)

Se a validação for bem-sucedida, o Gerenciador do Scale Out tentará ler o arquivo de configuração do servidor de trabalho e obter a impressão digital do certificado do trabalho. Para obter mais informações, consulte [Trabalho do Scale Out](integration-services-ssis-scale-out-worker.md). Se o Gerenciador do Scale Out não puder ler o arquivo de configuração de serviço do trabalho, há duas maneiras alternativas de fornecer o certificado de trabalho. 

1.  Você pode inserir a impressão digital do certificado de trabalho diretamente.

    ![Certificado do trabalho 1](media/portal-cert1.PNG)

2.  Ou fornecer o arquivo de certificado. 

    ![Certificado do trabalho 2](media/portal-cert2.PNG)

Depois de coletar as informações, o Gerenciador do Scale Out descreverá as ações a serem executadas. Normalmente, essas ações incluem a instalação do certificado, atualização do arquivo de configuração de serviço do trabalho e reinicialização do serviço do trabalho.

![Portal Adicionar Confirmação 1](media/portal-add-confirm1.PNG)

Caso o certificado de trabalho não esteja acessível, você precisará atualizá-lo manualmente e reiniciar o serviço do trabalho.

![Portal Adicionar Confirmação 2](media/portal-add-confirm2.PNG)

Marque a caixa de seleção **Confirmar** e, em seguida, selecione **OK** para começar a adicionar um Trabalho do Scale Out.

### <a name="delete-a-scale-out-worker"></a>Excluir um Trabalho do Scale Out
Para excluir um Trabalho do Scale Out, selecione o Trabalho do Scale Out e, em seguida, selecione **-** na parte inferior da lista do Trabalho do Scale Out.

### <a name="enable-or-disable-a-scale-out-worker"></a>Habilitar ou desabilitar um Trabalho do Scale Out
Para habilitar ou desabilitar um Trabalho do Scale Out, selecione o Trabalho do Scale Out e, em seguida, selecione **Habilitar Trabalho** ou **Desabilitar Trabalho.** Se o trabalho não estiver offline, o status do trabalho exibido no Gerenciador do Scale Out será alterado de acordo.

## <a name="edit-a-scale-out-worker-description"></a>Editar a descrição de um Trabalho do Scale Out
Para editar a descrição de um Trabalho do Scale Out, selecione o Trabalho do Scale Out e, em seguida, selecione **Editar**. Depois de terminar de editar a descrição, selecione **Salvar**.

![Portal Salvar o Trabalho](media/portal-save-worker.PNG)

## <a name="next-steps"></a>Próximas etapas
Para saber mais, veja os tópicos a seguir:
-   [Mestre do SSIS (Integration Services) Scale Out](integration-services-ssis-scale-out-master.md)
-   [Trabalho do SSIS (Integration Services) Scale Out](integration-services-ssis-scale-out-worker.md)