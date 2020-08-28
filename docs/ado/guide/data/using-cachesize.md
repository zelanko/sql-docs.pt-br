---
description: Usar CacheSize
title: Usando CacheSize | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
author: rothja
ms.author: jroth
ms.openlocfilehash: 97f6dba7bf01b3236d6b8b00e6338185cf6a8d41
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978997"
---
# <a name="using-cachesize"></a>Usar CacheSize
Use a propriedade **CacheSize** para controlar quantos registros recuperar ao mesmo tempo na memória local do provedor. Por exemplo, se o **CacheSize** for 10, depois de abrir primeiro o objeto **Recordset** , o provedor recuperará os 10 primeiros registros na memória local. À medida que você percorre o objeto **Recordset** , o provedor retorna os dados do buffer de memória local. Assim que você passa o último registro no cache, o provedor recupera os 10 registros seguintes da fonte de dados para o cache.  
  
> [!NOTE]
>  **CacheSize** é baseado na propriedade máxima específica do provedor **Open Rows** (na coleção **Properties** do objeto **Recordset** ). Não é possível definir o **CacheSize** com um valor maior que o **máximo de linhas abertas.** Para modificar o número de linhas que podem ser abertas pelo provedor, defina **máximo de linhas abertas**.  
  
 O valor de **CacheSize** pode ser ajustado durante a vida útil do objeto **Recordset** , mas a alteração desse valor afeta apenas o número de registros no cache após recuperações subsequentes da fonte de dados. Alterar o valor da propriedade sozinha não alterará o conteúdo atual do cache.  
  
 Se houver menos registros a serem recuperados que o **CacheSize** especifica, o provedor retornará os registros restantes e nenhum erro ocorrerá.  
  
 Uma configuração de **CacheSize** zero não é permitida e retorna um erro.  
  
 Os registros recuperados do cache não refletem as alterações simultâneas feitas por outros usuários nos dados de origem. Para forçar uma atualização de todos os dados armazenados em cache, use o método [Ressync](../../../ado/reference/ado-api/resync-method.md) .  
  
 Se **CacheSize** for definido como um valor maior que 1, os métodos de navegação ([move](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext e MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) poderão resultar na navegação para um registro excluído, se a exclusão ocorrer depois que os registros forem recuperados. Após a busca inicial, as exclusões subsequentes não serão refletidas no cache de dados até que você tente acessar um valor de dados de uma linha excluída. No entanto, a definição de **CacheSize** como 1 elimina esse problema porque as linhas excluídas não podem ser buscadas.
