---
title: Usando CacheSize | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c29fb18431d1f02d82db76605a8a53752ea0357
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184902"
---
# <a name="using-cachesize"></a>Usar CacheSize
Use o **CacheSize** propriedade para controlar quantos registros devem ser recuperados por vez na memória local do provedor. Por exemplo, se o **CacheSize** for 10, após a primeira abertura a **conjunto de registros** do objeto, o provedor recupera os primeiros 10 registros na memória local. Conforme você percorrer as **Recordset** do objeto, o provedor retorna os dados do buffer de memória local. Assim que você move além do último registro no cache, o provedor recupera os próximos 10 registros da fonte de dados no cache.  
  
> [!NOTE]
>  **CacheSize** se baseia o **máximo de linhas abertas** propriedade específica do provedor (no **propriedades** coleção do **Recordset** objeto). Não é possível definir **CacheSize** para um valor maior que **máximo de linhas abertas.** Para modificar o número de linhas que pode ser aberto pelo provedor, defina **máximo de linhas abertas**.  
  
 O valor de **CacheSize** podem ser ajustadas durante a vida útil do **Recordset** objeto, mas a alteração desse valor afeta somente o número de registros no cache após recuperações subsequentes da fonte de dados. Alterar o valor da propriedade sozinho não alterará o conteúdo atual do cache.  
  
 Se houver menos registros para recuperar-se que **CacheSize** Especifica, o provedor retorna os registros restantes e não ocorre nenhum erro.  
  
 Um **CacheSize** configuração de zero não é permitida e retornará um erro.  
  
 Registros recuperados do cache não refletem as alterações simultâneas feitas por outros usuários aos dados de origem. Para forçar uma atualização de todos os dados armazenados em cache, use o [ressincronizar](../../../ado/reference/ado-api/resync-method.md) método.  
  
 Se **CacheSize** é definido como um valor maior que 1, os métodos de navegação ([mover](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext e MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) pode resultar no painel de navegação para um excluído Registro, se a exclusão ocorrerá depois que os registros foram recuperados. Após a busca inicial, exclusões subsequentes não serão refletidas no seu cache de dados até que você tentar acessar um valor de dados de uma linha excluída. No entanto, definindo **CacheSize** como 1 elimina esse problema, porque as linhas excluídas não podem ser obtidas.
