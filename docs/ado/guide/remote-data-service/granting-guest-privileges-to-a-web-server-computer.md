---
description: Conceder privilégios de convidado para um computador do servidor Web
title: Concedendo privilégios de convidado a um computador do servidor Web | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- guest privileges in RDS [ADO]
ms.assetid: e851a22d-01bc-4eb0-bc42-92b8f65d1c63
author: rothja
ms.author: jroth
ms.openlocfilehash: d34e53f62b66197c7aaedcc0df57e489763c1dd0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978087"
---
# <a name="granting-guest-privileges-to-a-web-server-computer"></a>Conceder privilégios de convidado para um computador do servidor Web
A conta de servidor Web anônimo (IUSR_*ComputerName*) deve ser adicionada ao grupo local de convidados no computador do servidor Web para usar o RDS.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-grant-guest-privileges-to-a-web-server-computer"></a>Para conceder privilégios de convidado a um computador do servidor Web  
  
1.  No computador do Microsoft Windows 2000 Server, clique em **Iniciar**, aponte para **programas**, aponte para **Ferramentas administrativas**e clique em **Gerenciamento do computador**.  
  
2.  Na árvore de console, em **usuários e grupos locais**, clique em **grupos**.  
  
3.  Selecione o grupo local **convidados** . No menu **ação** , escolha **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades de convidados** , clique em **Adicionar**.  
  
5.  Se a conta de servidor Web anônimo não aparecer na lista da caixa de diálogo **Selecionar usuários ou grupos** , digite seu nome (IUSR_*ComputerName*) na caixa em branco inferior e clique em **Adicionar**.  
  
6.  Clique em **OK**.


