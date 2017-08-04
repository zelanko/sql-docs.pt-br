---
title: "Gerenciador de expansão do SQL Server Integration Services | Microsoft Docs"
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
ms.openlocfilehash: 96748296acd1b2f5ba98558335fece9637eadb87
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-scale-out-manager"></a>Integration Services expansão Manager

Gerenciador de fora da escala é uma ferramenta de gerenciamento que permite que você gerencie a sua topologia de SSIS expansão completa em um único local. Remove a carga de operação em vários computadores e lidar com comandos TSQL. 

Há duas maneiras para disparar o Gerenciador de fora de escala.

## <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1. Abra o Gerenciador de expansão do SQL Server Management Studio
Abra o SQL Server Management Studio e conecte-se à instância do SQL Server do mestre de fora da escala.

Clique com botão direito **SSISDB** no Pesquisador de objetos e selecione **gerenciar expansão...** . 
![Gerenciar a expansão](media/manage-scale-out.PNG)

> [!NOTE]
> É recomendável executar o SQL Server Management Studio como administrador, como as operações de gerenciamento fora de escala, como "adicionar um trabalho de expansão", será necessário privilégio administrativo.


## <a name="2-open-scale-out-manager-by-runing-ismanagerexe-directly"></a>2. Abrir Gerenciador de fora da escala, executando ISManager.exe diretamente

ISManager.exe localiza em %SystemDrive%\Program arquivos (x86) \Microsoft SQL Server\140\DTS\Binn\Management. Clique com botão direito **ISManager.exe** e selecione "Executar como administrador". 

Depois que ele for aberto, você precisa inserir o nome do Sql Server de escala Out mestre e conectá-lo antes de gerenciar sua expansão.

![Conexão do Portal](media/portal-connect.PNG)

Escala Out Manager fornece várias funcionalidades como a seguir. 

## <a name="enable-scale-out"></a>Habilitar de expansão
Depois de se conectar ao SQL Server, se a expansão não estiver habilitado, você pode clique no botão "Habilitar" para habilitá-lo.

![Habilitar portal em expansão](media/portal-enable-scale-out.PNG) 
## <a name="view-scale-out-master-status"></a>Exibir o status de escala Out mestre
O status de escala Out mestre será mostrado no **painel** página.

![Painel do Portal](media/portal-dashboard.PNG)
## <a name="view-scale-out-worker-status"></a>Exibir status da escala fora do trabalho
O status da escala fora do trabalho é mostrado no **Gerenciador de trabalho** página. Você pode clicar em cada trabalho para ver o status individual.

![Gerenciador de trabalho do Portal](media/portal-worker-manager.PNG)

## <a name="add-scale-out-worker"></a>Adicionar o trabalho de expansão
Para adicionar um trabalho de fora de escala, clique no botão "+" na parte inferior da lista de escala fora do trabalho. 

Insira o nome da máquina de escala Out trabalho você deseja adicionar e clique em "Validação". O Gerenciador de fora de escala verificará se o usuário atual tem acesso para os repositórios de certificados nos computadores de escala Out mestre e escala fora do trabalho.

![Conecte-se o trabalho](media/connect-worker.PNG)

Se a validação passa, escala Out Manager tentará ler arquivo de configuração de seu trabalho e obtenha a impressão digital do certificado do trabalhador. Para obter mais informações, consulte [escala Out trabalho](integration-services-ssis-scale-out-worker.md). Se não for capaz de ler o arquivo de configuração de trabalho, há duas formas alternativas para fornecer o certificado do trabalhador. 

Você pode inserir a impressão digital do certificado do trabalhador diretamente 

![Certificado do trabalhador 1](media/portal-cert1.PNG)

ou forneça o arquivo de certificado. 

![Certificado do trabalhador 2](media/portal-cert2.PNG)

Depois de coletar todas as informações, a escala Out gerente fornecerá as ações a serem executadas. Normalmente, ele inclui instalação do certificado, a atualização do arquivo de configuração de trabalho e reiniciar o serviço do trabalhador. 

![Adicionar portal confirmar 1](media/portal-add-confirm1.PNG)

Caso o certificado do trabalhador não está acessível, você precisa atualizá-lo manualmente por você mesmo e reinicie o serviço do trabalhador.

![Adicionar portal confirmar 2](media/portal-add-confirm2.PNG)

Clique na caixa de seleção Confirmar e começar a adicionar escala fora do trabalho.

## <a name="delete-scale-out-worker"></a>Excluir o trabalho de expansão
Para excluir um trabalho de fora de escala, selecione o trabalho de fora de escala e clique no "-" botão na parte inferior da lista de escala fora do trabalho.


## <a name="enabledisable-scale-out"></a>Habilitar/desabilitar de expansão
Para habilitar ou desabilitar um trabalho de fora de escala, selecione o trabalho de fora de escala e clique no botão de "Desabilitar o trabalho" ou "Habilitar o trabalho". O status do trabalho no Gerenciador de fora da escala mudará adequadamente, se o trabalhador não está offline.

## <a name="edit-scale-out-worker-description"></a>Editar descrição da escala fora do trabalho
Para editar a descrição de um trabalho de fora de escala, selecione o trabalho de fora de escala e clique no botão "Editar". Depois de terminar de editar, clique no botão "Salvar".

![Portal de salvar o trabalho](media/portal-save-worker.PNG)


