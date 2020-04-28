---
title: Objeto de erro | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932968"
---
# <a name="error-object"></a>Objeto Error
Contém detalhes sobre erros de acesso a dados que pertencem a uma única operação envolvendo o provedor.  
  
## <a name="remarks"></a>Comentários  
 Qualquer operação que envolva objetos ADO pode gerar um ou mais erros de provedor. À medida que cada erro ocorre, um ou mais objetos de **erro** são colocados na coleção de [erros](../../../ado/reference/ado-api/errors-collection-ado.md) do objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) . Quando outra operação ADO gera um erro, a coleção de **erros** é desmarcada e o novo conjunto de objetos de **erro** é colocado na coleção de **erros** .  
  
> [!NOTE]
>  Cada objeto de **erro** representa um erro de provedor específico, não um erro de ADO. Os erros do ADO são expostos ao mecanismo de tratamento de exceção de tempo de execução. Por exemplo, no Microsoft Visual Basic, a ocorrência de um erro específico do ADO irá disparar um evento **On Error** e aparecerá no objeto **Error** . Para obter uma lista completa de erros do ADO, consulte o tópico [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md) .  
  
 Você pode ler as propriedades de um objeto de **erro** para obter detalhes específicos sobre cada erro, incluindo o seguinte:  
  
-   A propriedade [Description](../../../ado/reference/ado-api/description-property.md) , que contém o texto do erro. Essa é a propriedade padrão.  
  
-   A propriedade [Number](../../../ado/reference/ado-api/number-property-ado.md) , que contém o valor inteiro **longo** da constante de erro.  
  
-   A propriedade [Source](../../../ado/reference/ado-api/source-property-ado-error.md) , que identifica o objeto que gerou o erro. Isso é particularmente útil quando você tem vários objetos de **erro** na coleção de **erros** após uma solicitação para uma fonte de dados.  
  
-   As propriedades [SQLSTATE](../../../ado/reference/ado-api/sqlstate-property.md) e [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md) , que fornecem informações de fontes de dados SQL.  
  
 Quando ocorre um erro de provedor, ele é colocado na coleção de **erros** do objeto de **conexão** . O ADO dá suporte ao retorno de vários erros por uma única operação ADO para permitir informações de erro específicas ao provedor. Para obter essas informações de erro avançadas em um manipulador de erro, use os recursos de interceptação de erro apropriados do idioma ou do ambiente com o qual você está trabalhando e, em seguida, use loops aninhados para enumerar as propriedades de cada objeto de **erro** na coleção de **erros** .  
  
> [!NOTE]
>  **Usuários do Microsoft Visual Basic e VBScript** Se não houver um objeto de **conexão** válido, você precisará recuperar informações de erro do objeto de **erro** .  
  
 Assim como os provedores fazem, o ADO limpa o objeto de **informações de erro OLE** antes de fazer uma chamada que poderia gerar potencialmente um novo erro de provedor. No entanto, a coleção de **erros** no objeto de **conexão** é limpa e preenchida somente quando o provedor gera um novo erro ou quando o método [Clear](../../../ado/reference/ado-api/clear-method-ado.md) é chamado.  
  
 Algumas propriedades e métodos retornam avisos que aparecem como objetos de **erro** na coleção de **erros** , mas não interrompem a execução de um programa. Antes de chamar os métodos [Ressync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)ou [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) em um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ; o método [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) em um objeto **Connection** ; ou defina a propriedade [Filter](../../../ado/reference/ado-api/filter-property.md) em um objeto **Recordset** , chame o método **Clear** na coleção **Errors** . Dessa forma, você pode ler a propriedade [Count](../../../ado/reference/ado-api/count-property-ado.md) da coleção de **erros** para testar os avisos retornados.  
  
 O objeto de **erro** não é seguro para scripts.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto Error](../../../ado/reference/ado-api/error-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades Description, HelpContext, ArquivoDeAjuda, NativeError, Number, Source e SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Exemplo das propriedades Description, HelpContext, ArquivoDeAjuda, NativeError, Number, Source e SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Objeto de conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Coleta de erros (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
