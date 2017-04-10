---
title: "Op&#231;&#245;es access check cache de configura&#231;&#227;o de servidor | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "opção de cache de verificação de acesso"
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# Op&#231;&#245;es access check cache de configura&#231;&#227;o de servidor
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quando objetos de banco de dados são acessados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a verificação de acesso é armazenada em cache em uma estrutura interna chamada **cache de resultado de verificação de acesso**. As opções **cota de cache de verificação de acesso** e a **contagem de compartimentos de cache de acesso** controlam o número de entradas e o número de compartimentos de hash usados para o **cache de resultado de verificação de acesso**. Em circunstâncias raras, o desempenho pode ser melhorado alterando essas opções.  
  
 Os valores padrão de 0 indicam aquele o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está gerenciando essas opções. A Microsoft recomenda a alteração dessas opções apenas quando orientadas pelos Serviços de Atendimento ao Cliente da Microsoft.  
  
## Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  