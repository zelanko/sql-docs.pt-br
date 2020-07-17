---
title: Opções de configuração de servidor access check cache | Microsoft Docs
description: Saiba mais sobre o cache de resultados da verificação de acesso e as opções que controlam o comportamento do cache. Veja quando alterar essas opções no SQL Server.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- access check cache option
- access check cache bucket count
- access check cache quota
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f5790d5eb416f789bbe67f10d28f18a375b4c572
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86158924"
---
# <a name="access-check-cache-server-configuration-options"></a>Opções access check cache de configuração de servidor
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Quando objetos de banco de dados são acessados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a verificação de acesso é armazenada em cache em uma estrutura interna chamada **cache de resultado de verificação de acesso**. 
  
A opção **número de buckets do cache de verificação de acesso** controla o número de buckets de hash que são usados para o cache de resultados de verificação de acesso. 

A opção **cota do cache de verificação de acesso** controla o número de entradas que são armazenadas no cache de resultados de verificação de acesso. Quando o número máximo de entradas é alcançado, as entradas mais antigas são removidas do cache de resultados de verificação de acesso.
  
Os valores padrão de 0 indicam aquele o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está gerenciando essas opções. Começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], os valores padrão são convertidos para as seguintes configurações internas:
-   Para o número de buckets do cache de verificação de acesso, o valor 0 define um valor padrão igual a 256 buckets.
-   Para a cota do cache de verificação de acesso, o valor 0 define um valor padrão igual a 1.024 entradas.

Em circunstâncias raras, o desempenho pode ser melhorado alterando essas opções. Por exemplo, talvez você queira reduzir o tamanho do cache de resultados de verificação de acesso se for usada muita memória. Ou, talvez você queira aumentar o tamanho do cache de resultados de verificação de acesso se tiver um alto uso da CPU quando as permissões forem recalculadas.
 
> [!IMPORTANT]
> A Microsoft recomenda a alteração dessas opções apenas quando orientadas pelos Serviços de Atendimento ao Cliente da Microsoft. Se você tiver que alterar os valores do "número de buckets do cache de verificação de acesso" e da "cota do cache de verificação de acesso", use a proporção de 1:4. Por exemplo, se você alterar o valor do "número de buckets do cache de verificação de acesso" para 512, deverá alterar o valor da "cota do cache de verificação de acesso" para 2.048. 
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
