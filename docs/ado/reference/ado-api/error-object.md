---
title: Objeto Error | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error
helpviewer_keywords:
- error object [ADO]
ms.assetid: a175d453-fa55-4f49-9ede-a26d83177919
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5018dc921267663d64037024ef21c82ac6e3f7c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932968"
---
# <a name="error-object"></a>Objeto Error
Contém detalhes sobre erros de acesso de dados que pertencem a uma única operação que envolva o provedor.  
  
## <a name="remarks"></a>Comentários  
 Qualquer operação que envolva objetos ADO pode gerar um ou mais erros do provedor. Conforme cada erro ocorrer, um ou mais **erro** objetos são colocados na [erros](../../../ado/reference/ado-api/errors-collection-ado.md) coleção dos [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto. Quando outra operação ADO gera um erro, o **erros** coleção estiver desmarcada e o novo conjunto de **erro** objetos é colocado no **erros** coleção.  
  
> [!NOTE]
>  Cada **erro** objeto representa um erro de provedor específico, não um erro do ADO. Erros ADO são expostos para o mecanismo de tratamento de exceções de tempo de execução. Por exemplo, no Microsoft Visual Basic, a ocorrência de um erro específico de ADO irá disparar uma **On Error** evento e aparece no **erro** objeto. Para obter uma lista completa de erros ADO, consulte o [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md) tópico.  
  
 Você pode ler um **erro** propriedades do objeto para obter detalhes específicos sobre cada erro, incluindo o seguinte:  
  
-   O [descrição](../../../ado/reference/ado-api/description-property.md) propriedade, que contém o texto do erro. Isso é a propriedade padrão.  
  
-   O [número](../../../ado/reference/ado-api/number-property-ado.md) propriedade, que contém o **longo** valor inteiro constante de erro.  
  
-   O [origem](../../../ado/reference/ado-api/source-property-ado-error.md) propriedade, que identifica o objeto que gerou o erro. Isso é particularmente útil quando você tem várias **erro** objetos na **erros** após uma solicitação para uma fonte de dados de coleção.  
  
-   O [SQLState](../../../ado/reference/ado-api/sqlstate-property.md) e [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md) propriedades, que fornecem informações de fontes de dados SQL.  
  
 Quando ocorre um erro do provedor, ele será colocado na **erros** coleção da **Conexão** objeto. O ADO oferece suporte para o retorno de vários erros por uma única operação de ADO para permitir a informações de erro específica do provedor. Para obter essas informações de erros completa em um manipulador de erro, use os recursos adequados de interceptação de erro da linguagem ou ambiente você está trabalhando com, em seguida, usar loops aninhados para enumerar as propriedades de cada **erro** objeto a **Erros** coleção.  
  
> [!NOTE]
>  **Microsoft Visual Basic e os usuários do VBScript** se não houver não válido **Conexão** do objeto, você precisará recuperar as informações de erro do **erro** objeto.  
  
 Assim como provedores de fazer, ADO limpa os **informações de erro OLE** antes de fazer uma chamada que potencialmente pode gerar um novo erro de provedor do objeto. No entanto, o **erros** coleta na **Conexão** objeto é limpo e populado somente quando o provedor gera um erro de novo, ou quando o [clara](../../../ado/reference/ado-api/clear-method-ado.md) método é chamado.  
  
 Algumas propriedades e métodos retornam os avisos que aparecem como **erro** objetos na **erros** coleção, mas não interrompem a execução de um programa. Antes de chamar o [ressincronizar](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) métodos em um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) do objeto; o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método em um **Conexão** do objeto; ou defina o [filtro](../../../ado/reference/ado-api/filter-property.md) propriedade em um **Recordset** de objeto, chame o **limpar**método de **erros** coleção. Dessa forma, você pode ler o [contagem](../../../ado/reference/ado-api/count-property-ado.md) propriedade da **erros** avisos retornados de coleção para testar.  
  
 O **erro** objeto não é seguro para script.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto Error](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Descrição, HelpContext, HelpFile, NativeError, número, código-fonte e exemplo de propriedades de SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descrição, HelpContext, HelpFile, NativeError, número, código-fonte e SQLState exemplo das propriedades (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Coleção Errors (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Apêndice a: provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
