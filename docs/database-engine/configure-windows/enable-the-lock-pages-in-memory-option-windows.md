---
title: "Habilitar a opção Bloquear Páginas na Memória (Windows) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Lock Pages in Memory option
ms.assetid: cd581fbc-4747-439e-87f9-2f18e39c5bb9
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: b5758fcbb5e73e40a3022d5a97fb744b6735c7d2
ms.sourcegitcommit: 4a462c7339dac7d3951a4e1f6f7fb02a3e01b331
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2017
---
# <a name="enable-the-lock-pages-in-memory-option-windows"></a>Habilitar a opção Bloquear Páginas na Memória (Windows)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Essa política do Windows determina quais contas podem usar um processo para manter dados na memória física, impedindo o sistema de paginar os dados para a memória virtual em disco.  
  
> [!NOTE]  
>  O bloqueio de páginas na memória pode aumentar o desempenho quando se espera paginar a memória em disco.  
  
 Use a ferramenta Política de Grupo do Windows (gpedit.msc) para habilitar essa política para a conta usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você deve ser um administrador do sistema para alterar essa política.  
  
### <a name="to-enable-the-lock-pages-in-memory-option"></a>Para habilitar a opção de bloqueio de páginas na memória  
  
1.  No menu **Iniciar** , clique em **Executar**. Na caixa **Abrir** , digite **gpedit.msc**.  
  
2.  No console **Editor de Política de Grupo Local** , expanda **Configuração do Computador**e depois expanda **Configurações do Windows**.  
  
3.  Expanda **Configurações de Segurança**e então expanda **Políticas Locais**.  
  
4.  Selecione a pasta **Atribuição de direitos de usuários** .  
  
     As políticas serão exibidas no painel de detalhes.  
  
5.  No painel, clique duas vezes em **Bloquear páginas na memória**.  
  
6.  Na caixa de diálogo **Configuração de Segurança Local – Bloquear páginas na memória** , clique em **Adicionar Usuário ou Grupo**.  
  
7.  Na caixa de diálogo **Selecionar Usuários, Contas de Serviço ou Grupos** , adicione uma conta com privilégios para executar sqlservr.exe.  
  
8.  Reinicie o serviço de Mecanismo de Dados do SQL Server para que esta configuração entre em vigor.
  
## <a name="see-also"></a>Consulte também  
 [Opções Server Memory de configuração do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
