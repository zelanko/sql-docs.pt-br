---
title: Comando exclusivo do conjunto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a5ab2ccf22c7322fa0e35cd281a8953b7685a02
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>Remarks  
 Alterando a configuração de um conjunto exclusivo não altera o status de tabelas abertos anteriormente. Por exemplo, se uma tabela é aberta com o conjunto exclusivo definido como ON e definir exclusivo for alterado posteriormente como OFF, a tabela retém seu status de uso exclusivo.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo da instalação do Visual FoxPro do ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
