---
title: "Habilitar a op&#231;&#227;o Bloquear P&#225;ginas na Mem&#243;ria (Windows) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "opção Bloquear Páginas na Memória"
ms.assetid: cd581fbc-4747-439e-87f9-2f18e39c5bb9
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Habilitar a op&#231;&#227;o Bloquear P&#225;ginas na Mem&#243;ria (Windows)
  Essa política do Windows determina quais contas podem usar um processo para manter dados na memória física, impedindo o sistema de paginar os dados para a memória virtual em disco.  
  
> [!NOTE]  
>  O bloqueio de páginas na memória pode aumentar o desempenho quando se espera paginar a memória em disco.  
  
 Use a ferramenta Política de Grupo do Windows (gpedit.msc) para habilitar essa política para a conta usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você deve ser um administrador do sistema para alterar essa política.  
  
### Para habilitar a opção de bloqueio de páginas na memória  
  
1.  No menu **Iniciar** , clique em **Executar**. Na caixa **Abrir** , digite **gpedit.msc**.  
  
2.  No console **Editor de Política de Grupo Local** , expanda **Configuração do Computador**e depois expanda **Configurações do Windows**.  
  
3.  Expanda **Configurações de Segurança**e então expanda **Políticas Locais**.  
  
4.  Selecione a pasta **Atribuição de direitos de usuários** .  
  
     As políticas serão exibidas no painel de detalhes.  
  
5.  No painel, clique duas vezes em **Bloquear páginas na memória**.  
  
6.  Na caixa de diálogo **Configuração de Segurança Local – Bloquear páginas na memória** , clique em **Adicionar Usuário ou Grupo**.  
  
7.  Na caixa de diálogo **Selecionar Usuários, Contas de Serviço ou Grupos** , adicione uma conta com privilégios para executar sqlservr.exe.  
  
8.  Faça logoff e depois faça logon para que essas alterações entrem em vigor.  
  
## Consulte também  
 [Opções Server Memory de configuração do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  