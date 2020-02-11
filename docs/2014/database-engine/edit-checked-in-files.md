---
title: Editar arquivos com check-in | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying checked-in files
- checking in files
ms.assetid: 560cd19f-ab22-4273-b00c-149993a630e6
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 97d6ab997a1ece36919a49243e0f1dc3cc6f3593
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779600"
---
# <a name="edit-checked-in-files"></a>Editar arquivos com check-in
  Você normalmente deve fazer o check-out de arquivos com controle do código-fonte antes de poder editá-los. No entanto, você [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] pode configurar o para que você possa modificar os arquivos que não fez check-out. Ao fazer isso, suas alterações são mantidas na memória até que você salve os arquivos. Você será solicitado a fazer check–out do arquivo no controle do código-fonte.  
  
 Se você trabalhar em equipe, não se recomenda permitir o check-in de arquivos a menos que seu provedor de controle do código-fonte ofereça suporte a check-outs de versão local e de servidor. A maioria dos provedores não dá suporte a check-outs de versões locais. Se seu provedor não oferecer suporte a check-outs de versões locais e você editar um arquivo com check-in, será necessário mesclar as versões da memória e do servidor manualmente para que o arquivo possa ser submetido a check-in. Não há suporte para mesclagens automáticas e auxiliadas por provedor nesta situação.  
  
### <a name="to-edit-checked-in-files"></a>Para editar arquivos com check-in  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Na caixa de diálogo **Opções** , expanda a pasta **Controle do Código-Fonte**e clique em **Ambiente**.  
  
3.  Clique **Permitir edição de itens com check-in**e clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar Check-ins](../../2014/database-engine/manage-checkins.md)   
 [Gerenciar check-outs](../../2014/database-engine/manage-checkouts.md)  
  
  
