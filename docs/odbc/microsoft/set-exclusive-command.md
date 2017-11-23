---
title: Comando exclusivo do conjunto | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f5aa039c9af4b3dfbabce2647408be7f612c80f3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="set-exclusive-command"></a>Comando exclusivo do conjunto
Especifica se os arquivos de tabela são abertos para uso exclusivo ou compartilhado em uma rede.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 Limita a acessibilidade de uma tabela aberta em uma rede para o usuário que foi aberto. A tabela não está acessível a outros usuários na rede. SET exclusivos ON também impede que todos os outros usuários tenham acesso somente leitura.  
  
 OFF  
 (Padrão para o driver; os padrões para o Visual FoxPro ON para a sessão de dados globais e OFF para uma sessão de dados particulares.) Permite que uma tabela aberta em uma rede compartilhada e modificados por qualquer usuário na rede.  
  
## <a name="remarks"></a>Comentários  
 Alterando a configuração de um conjunto exclusivo não altera o status de tabelas abertos anteriormente. Por exemplo, se uma tabela é aberta com o conjunto exclusivo definido como ON e definir exclusivo for alterado posteriormente como OFF, a tabela retém seu status de uso exclusivo.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo da instalação do Visual FoxPro do ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
