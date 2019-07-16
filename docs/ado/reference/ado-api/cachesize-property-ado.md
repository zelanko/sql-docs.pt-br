---
title: Propriedade CacheSize (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CacheSize
helpviewer_keywords:
- CacheSize property [ADO]
ms.assetid: 49dc9a49-af7b-433b-be36-7a14ca984fb7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6b33ef7eb4bae796fa2b2da59a7b1dc805d739e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920331"
---
# <a name="cachesize-property-ado"></a>Propriedade CacheSize (ADO)
Indica o número de registros de uma [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto armazenados em cache localmente na memória.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **longo** valor deve ser maior que 0. O padrão é 1.  
  
## <a name="remarks"></a>Comentários  
 Use o **CacheSize** propriedade para controlar quantos registros devem ser recuperados por vez na memória local do provedor. Por exemplo, se o **CacheSize** for 10, após a primeira abertura a **conjunto de registros** do objeto, o provedor recupera os primeiros 10 registros na memória local. Conforme você percorrer as **Recordset** do objeto, o provedor retorna os dados do buffer de memória local. Assim que você move além do último registro no cache, o provedor recupera os próximos 10 registros da fonte de dados no cache.  
  
> [!NOTE]
>  **CacheSize** se baseia o **máximo de linhas abertas** propriedade específica do provedor (no **propriedades** coleção do **Recordset** objeto). Não é possível definir **CacheSize** para um valor maior que **máximo de linhas abertas**. Para modificar o número de linhas que pode ser aberta pelo provedor, defina **máximo de linhas abertas**.  
  
 O valor de **CacheSize** podem ser ajustadas durante a vida útil do **Recordset** objeto, mas a alteração desse valor afeta somente o número de registros no cache após recuperações subsequentes da fonte de dados. Alterar o valor da propriedade sozinho não alterará o conteúdo atual do cache.  
  
 Se houver menos registros para recuperar-se que **CacheSize** Especifica, o provedor retorna os registros restantes e não ocorre nenhum erro.  
  
 Um **CacheSize** configuração de zero não é permitida e retornará um erro.  
  
 Registros recuperados do cache não refletem as alterações simultâneas feitas por outros usuários aos dados de origem. Para forçar uma atualização de todos os dados armazenados em cache, use o [ressincronizar](../../../ado/reference/ado-api/resync-method.md) método.  
  
 Se **CacheSize** é definido como um valor maior do que um, os métodos de navegação ([mover](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext e MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) pode resultar no painel de navegação para um Registro, deve ser excluído se a exclusão ocorrerá depois que os registros foram recuperados. Após a busca inicial, exclusões subsequentes não serão refletidas no seu cache de dados até que você tentar acessar um valor de dados de uma linha excluída. No entanto, definindo **CacheSize** para um elimina esse problema, pois as linhas excluídas não podem ser obtidas.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade CacheSize (VB)](../../../ado/reference/ado-api/cachesize-property-example-vb.md)   
 [Exemplo da propriedade CacheSize (VC + +)](../../../ado/reference/ado-api/cachesize-property-example-vc.md)   
 [Exemplo da propriedade CacheSize (JScript)](../../../ado/reference/ado-api/cachesize-property-example-jscript.md)
