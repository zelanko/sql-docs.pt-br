---
title: MSSQLSERVER_33081 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 33081 (Database Engine error)
ms.assetid: 839705e7-fa37-4c0d-9f3f-95a9eab98bcf
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fa36c1111e1397e0a652c5d784811984a4de0195
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120568"
---
# <a name="mssqlserver33081"></a>MSSQLSERVER_33081
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|33081|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_DLL_TRUST_VERIFICATION_FAILED|  
|Texto da mensagem|Falha ao carregar o provedor criptográfico '%.*ls' devido a uma assinatura inválida de Authenticode ou a um caminho de arquivo inválido.  Verifique as mensagens anteriores à procura de outras falhas.|  
  
## <a name="explanation"></a>Explicação  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde carregar o provedor criptográfico listado na mensagem de erro. Há várias falhas de API do Windows que poderiam causar esse erro. O buffer de anéis contém o nome da API com falha e o código de erro do Windows retornado pela API. Para obter mais informações, consulte a exibição sys.dm_os_ring_buffers usando a consulta a seguir.  
  
```  
SELECT * FROM sys.dm_os_ring_buffers   
WHERE ring_buffer_type = 'RING_BUFFER_SECURITY_ERROR';  
```  
  
## <a name="user-action"></a>Ação do usuário  
 Para investigar o problema, pesquise o código de erro do Windows no MSDN (http://msdn.microsoft.com/)). Resolva o erro ou contate o [!INCLUDE[msCoName](../../includes/msconame-md.md)] CSS para obter mais informações. Se for necessário contatar o CSS, colete as informações a seguir para nossa equipe de suporte.  
  
-   O log de erros que mostra a erro de falha no carregamento do provedor criptográfico.  
  
-   A saída da seguinte instrução:  
  
    ```  
    SELECT * FROM sys.dm_os_ring_buffers   
    WHERE ring_buffer_type = 'RING_BUFFER_SECURITY_ERROR';  
    ```  
  
> [!NOTE]  
>  Tente coletar as informações do buffer de anéis imediatamente, pois as informações de buffer de anéis podem ser perdidas durante uma reinicialização.  
  
  