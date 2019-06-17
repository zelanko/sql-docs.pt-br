---
title: Comando SET EXCLUSIVE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fccbc9b258cbff1e14ccc76e10af9d26efc4b70b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63159266"
---
# <a name="set-exclusive-command"></a>Comando SET EXCLUSIVE
Especifica se os arquivos de tabela são abertos para uso exclusivo ou compartilhado em uma rede.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 Limita a acessibilidade de uma tabela aberta em uma rede para o usuário que abriu a ele. A tabela não está acessível para outros usuários na rede. SET exclusivos ON também impede que todos os outros usuários que têm acesso somente leitura.  
  
 OFF  
 (Padrão para o driver; os padrões para o Visual FoxPro são ON para a sessão de dados globais e OFF para uma sessão de dados privados). Permite que uma tabela aberta em uma rede para ser compartilhado e modificada por qualquer usuário na rede.  
  
## <a name="remarks"></a>Comentários  
 Alterando a configuração de um conjunto exclusivo não altera o status das tabelas abertos anteriormente. Por exemplo, se uma tabela é aberta com um conjunto exclusivo definido como ON e exclusivo definido mais tarde é alterado para OFF, a tabela retém seu status de uso exclusivo.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo da instalação do Visual FoxPro do ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
