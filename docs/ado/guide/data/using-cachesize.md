---
title: Usando CacheSize | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 74ec85c5907485edc5ad8dbcb6c24826fc21ccf3
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-cachesize"></a>Usando CacheSize
Use o **CacheSize** propriedade para controlar quantos registros devem ser recuperados por vez na memória local do provedor. Por exemplo, se o **CacheSize** é 10, após abertura primeiro o **registros** do objeto, o provedor recupera os primeiros 10 registros na memória local. Quando você percorre o **registros** do objeto, o provedor retorna os dados do buffer de memória local. Assim que você passa o último registro no cache, o provedor recupera os 10 registros da fonte de dados no cache.  
  
> [!NOTE]
>  **CacheSize** se baseia o **máximo de linhas aberto** propriedade específica de provedor (no **propriedades** coleção do **registros** objeto). Não é possível definir **CacheSize** para um valor maior que **máximo de linhas aberto.** Para modificar o número de linhas que podem ser abertos pelo provedor, defina **máximo de linhas aberto**.  
  
 O valor de **CacheSize** podem ser ajustadas durante a vida do **registros** objeto, mas a alteração desse valor afeta somente o número de registros no cache após recuperações subsequentes da fonte de dados. Alterar o valor da propriedade sozinho não alterará o conteúdo atual do cache.  
  
 Se houver menos registros a serem recuperados de **CacheSize** Especifica, o provedor retorna os registros restantes e não ocorre nenhum erro.  
  
 Um **CacheSize** configuração de zero não é permitida e retornará um erro.  
  
 Registros recuperados do cache não refletem as alterações simultâneas que outros usuários feitos nos dados de origem. Para forçar uma atualização de todos os dados armazenados em cache, use o [Resync](../../../ado/reference/ado-api/resync-method.md) método.  
  
 Se **CacheSize** é definido como um valor maior que 1, os métodos de navegação ([mover](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext e MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) pode resultar na navegação excluído Registro, se a exclusão ocorrer depois que os registros foram recuperados. Após a busca inicial, exclusões subsequentes não serão refletidas em seu cache de dados até que você tentar acessar um valor de dados de uma linha excluída. Entretanto, a configuração **CacheSize** como 1 elimina esse problema, porque as linhas excluídas não podem ser obtidas.

