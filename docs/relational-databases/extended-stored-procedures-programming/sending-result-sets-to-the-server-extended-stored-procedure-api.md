---
title: Enviando conjuntos de resultados para o servidor (Extended API de procedimento armazenado) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0dd49eba42bd735430bd73f244e76a13c8315806
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>Enviando conjuntos de resultados ao Servidor (API do procedimento armazenado estendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 Ao enviar um conjunto de resultados para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o procedimento armazenado estendido deve chamar a API apropriada da seguinte maneira:  
  
-   O **srv_sendmsg** função pode ser chamada em qualquer ordem antes ou depois que todas as linhas (se houver) tiverem sido enviadas com **srv_sendrow**. Todas as mensagens devem ser enviadas para o cliente antes do status de conclusão é enviado com **srv_senddone**.  
  
-   A função **srv_sendrow** é chamada uma vez para cada linha enviada ao cliente. Todas as linhas devem ser enviadas para o cliente antes de qualquer mensagem, o valor de status ou status de conclusão são enviadas com **srv_sendmsg**, o **srv_status** argumento de **srv_pfield**, ou **srv_senddone**.  
  
-   Envio de uma linha que não tenha todas as suas colunas definidas com **srv_describe** faz com que o aplicativo gerar uma mensagem de erro informativa e retorne FAIL ao cliente. Neste caso, a linha não é enviada.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando procedimentos armazenados estendidos](../../relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures.md)  
  
  
