---
title: Editar arquivos com Check-In | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- modifying checked-in files
- checking in files
ms.assetid: 560cd19f-ab22-4273-b00c-149993a630e6
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fd91efe4bd802a64ced4e6f93ac65f16ed4e5a71
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006695"
---
# <a name="edit-checked-in-files"></a>Editar arquivos com check-in
  Você normalmente deve fazer o check-out de arquivos com controle do código-fonte antes de poder editá-los. Entretanto, é possível configurar o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para que você possa modificar arquivos que não fizeram check-out. Ao fazer isso, suas alterações são mantidas na memória até os arquivos serem salvos. Você será solicitado a fazer check–out do arquivo no controle do código-fonte.  
  
 Se você trabalhar em equipe, não se recomenda permitir o check-in de arquivos a menos que seu provedor de controle do código-fonte ofereça suporte a check-outs de versão local e de servidor. A maioria dos provedores não dá suporte a check-outs de versões locais. Se seu provedor não oferecer suporte a check-outs de versões locais e você editar um arquivo com check-in, será necessário mesclar as versões da memória e do servidor manualmente para que o arquivo possa ser submetido a check-in. Não há suporte para mesclagens automáticas e auxiliadas por provedor nesta situação.  
  
### <a name="to-edit-checked-in-files"></a>Para editar arquivos com check-in  
  
1.  No menu **Ferramentas** , clique em **Opções**.  
  
2.  Na caixa de diálogo **Opções** , expanda a pasta **Controle do Código-Fonte**e clique em **Ambiente**.  
  
3.  Clique **Permitir edição de itens com check-in**e clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar check-ins](../../2014/database-engine/manage-checkins.md)   
 [Gerenciar check-outs](../../2014/database-engine/manage-checkouts.md)  
  
  