---
title: Habilitar a opção Bloquear Páginas na Memória (Windows) | Microsoft Docs
description: Saiba como ativar a opção "Bloquear Páginas na Memória". Veja como ela pode aumentar o desempenho mantendo os dados na memória física, em vez de paginá-los no disco.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Lock Pages in Memory option
ms.assetid: cd581fbc-4747-439e-87f9-2f18e39c5bb9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6390c4a4bb4d8ea2ed9b5e5be1712eb7e782a29b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772480"
---
# <a name="enable-the-lock-pages-in-memory-option-windows"></a>Habilitar a opção Bloquear Páginas na Memória (Windows)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Essa política do Windows determina quais contas podem usar um processo para manter dados na memória física, impedindo o sistema de paginar os dados para a memória virtual em disco.  
  
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
  
6.  Na caixa de diálogo **Configuração de Segurança Local – Bloquear páginas na memória**, clique em **Adicionar Usuário ou Grupo**.  
  
7.  Na caixa de diálogo **Selecionar Usuários, Contas de Serviço ou Grupos**, selecione a conta do Serviço SQL Server.  
  
8.  Reinicie o Serviço SQL Server para que essa configuração tenha efeito.
  
## <a name="see-also"></a>Consulte Também  
 [Opções Server Memory de configuração do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
