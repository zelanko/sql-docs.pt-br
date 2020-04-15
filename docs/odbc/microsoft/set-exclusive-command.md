---
title: COMANDO SET EXCLUSIVE | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d140c4be3ab850547ac82f9b954e7313b008dbf0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300856"
---
# <a name="set-exclusive-command"></a>Comando SET EXCLUSIVE
Especifica se os arquivos de tabela são abertos para uso exclusivo ou compartilhado em uma rede.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ATIVADO  
 Limita a acessibilidade de uma tabela aberta em uma rede ao usuário que a abriu. A tabela não é acessível a outros usuários da rede. SET EXCLUSIVE ON também impede que todos os outros usuários tenham acesso somente à leitura.  
  
 OFF  
 (Padrão para o driver; os padrões do Visual FoxPro são ON para a sessão global de dados e OFF para uma sessão de dados privada.) Permite que uma tabela aberta em uma rede seja compartilhada e modificada por qualquer usuário da rede.  
  
## <a name="remarks"></a>Comentários  
 Alterar a configuração do SET EXCLUSIVE não altera o status das tabelas abertas anteriormente. Por exemplo, se uma tabela for aberta com SET EXCLUSIVE set to ON e SET EXCLUSIVE for posteriormente alterado para OFF, a tabela manterá seu status de uso exclusivo.  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo da instalação do Visual FoxPro do ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
