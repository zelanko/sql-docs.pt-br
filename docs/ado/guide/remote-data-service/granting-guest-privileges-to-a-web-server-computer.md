---
title: Concedendo privilégios de convidado a um servidor Web | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- guest privileges in RDS [ADO]
ms.assetid: e851a22d-01bc-4eb0-bc42-92b8f65d1c63
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21c4eae0608e433ed3ca7888091a7c658726192d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63214790"
---
# <a name="granting-guest-privileges-to-a-web-server-computer"></a>Conceder privilégios de convidado para um computador do servidor Web
A conta do servidor Web anônima (IUSR _*ComputerName*) deve ser adicionado ao local grupo convidados no computador do servidor Web para usar o RDS.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-grant-guest-privileges-to-a-web-server-computer"></a>Para conceder privilégios de convidado em um computador do servidor Web  
  
1.  No seu computador Microsoft Windows 2000 Server, clique em **inicie**, aponte para **programas**, aponte para **ferramentas administrativas**e, em seguida, clique em **computador Gerenciamento**.  
  
2.  Na árvore de console, no **usuários e grupos locais**, clique em **grupos**.  
  
3.  Selecione o **convidados** grupo local. Dos **ação** menu, escolha **propriedades**.  
  
4.  No **propriedades de convidados** caixa de diálogo, clique em **Add**.  
  
5.  Se a conta anônima do servidor Web não aparecerá na lista na **selecionar usuários ou grupos** diálogo caixa, digite seu nome (IUSR _*ComputerName*) na caixa em branco da parte inferior e clique **adicionar** .  
  
6.  Clique em **OK**.


