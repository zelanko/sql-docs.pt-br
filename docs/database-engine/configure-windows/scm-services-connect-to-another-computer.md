---
title: Conectar-se a outro computador (SQL Server Configuration Manager) | Microsoft Docs
description: Descubra como gerenciar os serviços existentes em um computador remoto. Confira como usar SQL Server Configuration Manager ou SQL Server Management Studio para essa tarefa.
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], other computers
ms.assetid: c4c1e94f-4f5f-431e-8b5b-d5ff97baf723
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e4a2ca1eea0ec4b42bba65b62525bb6d86e52c88
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85651349"
---
# <a name="scm-services---connect-to-another-computer"></a>Serviços SCM – conectar-se a outro computador

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este artigo descreve como conectar-se a outro computador no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Siga o primeiro procedimento para abrir o Windows Computer Management [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (mmc), conecte-se ao computador e expanda a árvore Serviços e Aplicativos. Siga o segundo procedimento para criar um arquivo com um link para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager em um computador remoto.

> [!NOTE]
> Algumas ações não podem ser executadas pelo Configuration Manager ao conectar-se remotamente.

Para iniciar, parar, pausar ou retomar o serviço em outro computador, você também pode conectar-se ao servidor com o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse no servidor ou no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agente e clique na ação desejada.

## <a name="SSMSProcedure"></a>

### <a name="to-connect-to-another-computer-with-windows-computer-management"></a>Para se conectar a outro computador com o Windows Computer Management

1. Clique com o botão direito do mouse no botão de menu **Iniciar** e clique em **Gerenciamento do Computador (Local)** .
2. No menu **Ação**, clique em **Conectar a outro computador**.
3. Na caixa de diálogo **Selecionar Computador** , na caixa de texto **Outro computador** , digite o nome do computador que você deseja administrar e clique em **OK**.

   O Computer Management exibe os serviços que estão sendo executados no computador remoto. O nó de nível superior é alterado para **Gerenciamento de Computador** \<*remotecomputer*>.

4. Na árvore de console, expanda **Serviços e Aplicativos**e expanda o **SQL Server Configuration Manager** para administrar os serviços do computador remoto.

### <a name="to-save-a-link-to-sql-server-configuration-manager-for-another-computer"></a>Para salvar um link no SQL Server Configuration Manager para outro computador

1. No menu **Iniciar** , clique em **Executar**.

2. Na caixa **Abrir**, digite **mmc -a** (digite **mmc /32 -a** em um computador de 64 bits) para abrir o console de gerenciamento do [!INCLUDE[msCoName](../../includes/msconame-md.md)] no modo de autor.
3. No menu **Arquivo** , clique em **Adicionar/Remover Snap-in**.
4. Na janela **Adicionar/Remover Snap-in** , clique em **Adicionar**.
5. Na janela **Adicionar Snap-in Autônomo** , clique em **Gerenciamento do Computador** e clique em **Adicionar**.
6. Na janela **Gerenciamento do Computador** , clique em **Outro computador**, digite o nome do computador remoto que deseja gerenciar e depois clique em **Terminar**.
7. Na janela **Adicionar Snap-in Autônomo** , clique em **Fechar**.
8. Na janela **Adicionar/Remover Snap-in** , clique em **OK**.
9. Expanda **Gerenciamento do Computador (** _\<computer name>_ **)** e **Serviços e Aplicativos**.
10. Clique com o botão direito do mouse no **SQL Server Configuration Manager**e clique em **Nova Janela daqui**.
11. No menu **Janela**, clique em **Raiz do Console** para retornar à primeira janela e exclui-la.
12. No menu **Arquivo** , clique em **Salvar como**e salve o arquivo na pasta desejada, com um nome apropriado com a extensão de arquivo **.msc** . Feche o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console.
13. Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager no computador de destino, clique duas vezes no arquivo. Se desejar, salve um link no arquivo na área de trabalho ou no menu **Iniciar** .

> [!CAUTION]
> Ao usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager em um computador remoto, o nome do computador não é óbvio e é possível parar erroneamente ou configurar o computador errado. Na guia **Serviço** , marque a caixa **Nome do Host** para confirmar o nome do computador antes de modificar um serviço.

## <a name="see-also"></a>Confira também

- [Configurar o WMI para mostrar o status do servidor nas ferramentas do SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)
