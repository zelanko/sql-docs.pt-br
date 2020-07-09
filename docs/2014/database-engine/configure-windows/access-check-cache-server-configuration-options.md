---
title: Opções de configuração de servidor access check cache | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- access check cache option
- access check cache bucket count
- access check cache quota
ms.assetid: 0a992ea8-3ec6-4a4d-97b5-460ae7326247
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: feed895eeb7b11b4c41c51c4c26859a1057d2733
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86158754"
---
# <a name="access-check-cache-server-configuration-options"></a>Opções access check cache de configuração de servidor
Quando objetos de banco de dados são acessados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a verificação de acesso é armazenada em cache em uma estrutura interna chamada **cache de resultado de verificação de acesso**. 
  
A opção **acessar contagem de buckets de cache** controla o número de buckets de hash que são usados para o cache de resultados da verificação de acesso. 

A opção de **cota de cache de verificação de acesso** controla o número de entradas armazenadas no cache de resultados da verificação de acesso. Quando o número máximo de entradas é atingido, as entradas mais antigas são removidas do cache de resultados da verificação de acesso.
  
Os valores padrão de 0 indicam aquele o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está gerenciando essas opções. De [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] até [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , os valores padrão são convertidos para as seguintes configurações internas:
-   Para a contagem de buckets de cache de verificação de acesso, o valor 0 define um valor padrão de 256 buckets para arquitetura x86 e 2.048 buckets para arquiteturas x64 e IA-64.
-   Para a cota de cache de verificação de acesso, o valor 0 define um valor padrão de 1.024 entradas para a arquitetura x86 e 28.192.048 buckets para arquiteturas x64 e IA-64.

Em circunstâncias raras, o desempenho pode ser melhorado alterando essas opções. Por exemplo, talvez você queira reduzir o tamanho do cache de resultados da verificação de acesso se for usada muita memória. Ou, talvez você queira aumentar o tamanho do cache de resultados da verificação de acesso se tiver um alto uso da CPU quando as permissões forem recalculadas.

> [!IMPORTANT]
> A Microsoft recomenda a alteração dessas opções apenas quando orientadas pelos Serviços de Atendimento ao Cliente da Microsoft.
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
