---
title: Enviando conjuntos de resultados para o servidor (API de procedimento armazenado estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ab77fa15bb4d3d1e68b8335a1c9026b1831a8619
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47625594"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>Enviando conjuntos de resultados ao Servidor (API do procedimento armazenado estendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 Ao enviar um conjunto de resultados [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o procedimento armazenado estendido deve chamar a API apropriada da seguinte maneira:  
  
-   O **srv_sendmsg** função pode ser chamada em qualquer ordem antes ou depois que todas as linhas (se houver) tiverem sido enviadas com **srv_sendrow**. Todas as mensagens devem ser enviadas ao cliente antes do envio com o status de conclusão **srv_senddone**.  
  
-   A função **srv_sendrow** é chamada uma vez para cada linha enviada ao cliente. Todas as linhas devem ser enviadas para o cliente antes de qualquer mensagem, o valor de status ou status de conclusão são enviados com **srv_sendmsg**, o **srv_status** argumento **srv_pfield**, ou **srv_senddone**.  
  
-   Envio de uma linha que não tenha todas as suas colunas definidas com **srv_describe** faz com que o aplicativo para uma mensagem de erro informativa e retorne FAIL ao cliente. Neste caso, a linha não é enviada.  
  
## <a name="see-also"></a>Consulte também  
 [Criando procedimentos armazenados estendidos](../../relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures.md)  
  
  
