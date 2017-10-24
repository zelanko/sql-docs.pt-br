---
title: Objeto de erro | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Error
helpviewer_keywords:
- error object [ADO]
ms.assetid: a175d453-fa55-4f49-9ede-a26d83177919
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a283d7d40140e46668dc704196316a4a52c1fdbf
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="error-object"></a>Objeto Error
Contém detalhes sobre erros de acesso de dados que pertencem a uma única operação que envolve o provedor.  
  
## <a name="remarks"></a>Comentários  
 Qualquer operação que envolva objetos ADO pode gerar um ou mais erros do provedor. Como cada erro, um ou mais **erro** objetos são colocados no [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção do [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto. Quando outra operação ADO gera um erro, o **erros** coleção é desmarcada e o novo conjunto de **erro** objetos é colocado no **erros** coleção.  
  
> [!NOTE]
>  Cada **erro** objeto representa um erro de provedor específico, não um erro de ADO. Erros de ADO são expostos para o mecanismo de tratamento de exceções de tempo de execução. Por exemplo, no Microsoft Visual Basic, a ocorrência de um erro específico de ADO irá disparar um **On Error** evento e aparece no **erro** objeto. Para obter uma lista completa de erros de ADO, consulte o [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md) tópico.  
  
 Você pode ler um **erro** propriedades do objeto para obter detalhes específicos sobre cada erro, incluindo o seguinte:  
  
-   O [descrição](../../../ado/reference/ado-api/description-property.md) propriedade, que contém o texto do erro. Esta é a propriedade padrão.  
  
-   O [número](../../../ado/reference/ado-api/number-property-ado.md) propriedade, que contém o **longo** valor de inteiro da constante de erro.  
  
-   O [fonte](../../../ado/reference/ado-api/source-property-ado-error.md) propriedade, que identifica o objeto que gerou o erro. Isso é particularmente útil quando você tem várias **erro** objetos no **erros** coleção após uma solicitação para uma fonte de dados.  
  
-   O [SQLState](../../../ado/reference/ado-api/sqlstate-property.md) e [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md) propriedades, que fornecem informações de fontes de dados do SQL.  
  
 Quando ocorre um erro de provedor, ele é colocado no **erros** coleção do **Conexão** objeto. ADO dá suporte a retorno de vários erros por uma única operação ADO para permitir que as informações de erro específica do provedor. Para obter essas informações de erros em um manipulador de erro, use os recursos adequados de interceptação de erro do idioma ou do ambiente que você está trabalhando com e use loops aninhados para enumerar as propriedades de cada **erro** objeto o **Erros** coleção.  
  
> [!NOTE]
>  **Microsoft Visual Basic e VBScript usuários** se não houver não válido **Conexão** do objeto, você precisará recuperar informações de erro o **erro** objeto.  
  
 Assim como provedores de fazer, ADO limpa o **informações de erro OLE** objeto antes de fazer uma chamada que potencialmente pode gerar um novo erro do provedor. No entanto, o **erros** coleção no **Conexão** objeto está desmarcado e preenchido somente quando o provedor gera um erro de novo, ou quando o [limpar](../../../ado/reference/ado-api/clear-method-ado.md) método é chamado.  
  
 Algumas propriedades e métodos retornam os avisos que aparecem como **erro** objetos no **erros** coleção, mas não interromper a execução do programa. Antes de chamar o [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) métodos em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto; o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método em um **Conexão** objeto; ou defina o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade em uma **Recordset** de objeto, chame o **limpar**método sobre o **erros** coleção. Dessa forma, você pode ler o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade o **erros** avisos retornados de coleção para testar.  
  
 O **erro** o objeto não é seguro para script.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto Error](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Descrição, HelpContext, HelpFile, NativeError, número, fonte e exemplo de propriedades de SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descrição, HelpContext, HelpFile, NativeError, número, fonte e exemplo de propriedades de SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Coleção de erros (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)

