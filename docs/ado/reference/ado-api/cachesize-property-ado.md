---
title: Propriedade CacheSize (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CacheSize
helpviewer_keywords:
- CacheSize property [ADO]
ms.assetid: 49dc9a49-af7b-433b-be36-7a14ca984fb7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2aeb7b018a34e2efe17fde2b4aa3c7f7e7df9113
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="cachesize-property-ado"></a>Propriedade CacheSize (ADO)
Indica o número de registros de um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto são armazenadas localmente em cache.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **longo** valor deve ser maior que 0. O padrão é 1.  
  
## <a name="remarks"></a>Remarks  
 Use o **CacheSize** propriedade para controlar quantos registros devem ser recuperados por vez na memória local do provedor. Por exemplo, se o **CacheSize** é 10, após abertura primeiro o **registros** do objeto, o provedor recupera os primeiros 10 registros na memória local. Quando você percorre o **registros** do objeto, o provedor retorna os dados do buffer de memória local. Assim que você passa o último registro no cache, o provedor recupera os 10 registros da fonte de dados no cache.  
  
> [!NOTE]
>  **CacheSize** se baseia o **máximo de linhas aberto** propriedade específica de provedor (no **propriedades** coleção do **registros** objeto). Não é possível definir **CacheSize** para um valor maior que **máximo de linhas aberto**. Para modificar o número de linhas que pode ser aberta pelo provedor, defina **máximo de linhas aberto**.  
  
 O valor de **CacheSize** podem ser ajustadas durante a vida do **registros** objeto, mas a alteração desse valor afeta somente o número de registros no cache após recuperações subsequentes da fonte de dados. Alterar o valor da propriedade sozinho não alterará o conteúdo atual do cache.  
  
 Se houver menos registros a serem recuperados de **CacheSize** Especifica, o provedor retorna os registros restantes e não ocorre nenhum erro.  
  
 Um **CacheSize** configuração de zero não é permitida e retornará um erro.  
  
 Registros recuperados do cache não refletem as alterações simultâneas que outros usuários feitos nos dados de origem. Para forçar uma atualização de todos os dados armazenados em cache, use o [Resync](../../../ado/reference/ado-api/resync-method.md) método.  
  
 Se **CacheSize** é definido como um valor maior do que um, os métodos de navegação ([mover](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext e MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) pode resultar na barra de navegação para um excluiu o registro, se a exclusão ocorrer depois que os registros foram recuperados. Após a busca inicial, exclusões subsequentes não serão refletidas em seu cache de dados até que você tentar acessar um valor de dados de uma linha excluída. Entretanto, a configuração **CacheSize** para um elimina esse problema, desde que as linhas excluídas não podem ser obtidas.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedade CacheSize (VB)](../../../ado/reference/ado-api/cachesize-property-example-vb.md)   
 [Exemplo de propriedade CacheSize (VC + +)](../../../ado/reference/ado-api/cachesize-property-example-vc.md)   
 [Exemplo da propriedade CacheSize (JScript)](../../../ado/reference/ado-api/cachesize-property-example-jscript.md)
