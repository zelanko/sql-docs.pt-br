---
title: MSSQLSERVER_33081 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 33081 (Database Engine error)
ms.assetid: 839705e7-fa37-4c0d-9f3f-95a9eab98bcf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 829b909cf8bf8dd3c2dd8249fa7b6ce30570c6a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908477"
---
# <a name="mssqlserver33081"></a>MSSQLSERVER_33081
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
Para investigar o problema, pesquise o código de erro do Windows no MSDN (https://msdn.microsoft.com/) ). Resolva o erro ou contate o [!INCLUDE[msCoName](../../includes/msconame-md.md)] CSS para obter mais informações. Se for necessário contatar o CSS, colete as informações a seguir para nossa equipe de suporte.  
  
-   O log de erros que mostra a erro de falha no carregamento do provedor criptográfico.  
  
-   A saída da seguinte instrução:  
  
    ```  
    SELECT * FROM sys.dm_os_ring_buffers   
    WHERE ring_buffer_type = 'RING_BUFFER_SECURITY_ERROR';  
    ```  
  
> [!NOTE]  
> Tente coletar as informações do buffer de anéis imediatamente, pois as informações de buffer de anéis podem ser perdidas durante uma reinicialização.  
  
