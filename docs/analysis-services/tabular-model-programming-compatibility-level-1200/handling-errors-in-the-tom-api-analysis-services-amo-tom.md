---
title: Tratamento de erros na API de TOM (Analysis Services AMO-TOM) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b2483d4d6d443a21f43cf11e5271bb11041f1c53
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34039617"
---
# <a name="handling-errors-in-the-tom-api-analysis-services-amo-tom"></a>Tratamento de erros na API de TOM (Analysis Services AMO-TOM)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Uma prática comum para as bibliotecas gerenciadas como o modelo de objeto Tabular do Analysis Services Management Objects (AMO) (TOM) é usar exceções como um mecanismo de relatório de condições de erro para o usuário.  

Quando for detectado um erro no AMO TOM, além de gerar algumas exceções .NET padrão como **ArgumentException** e **InvalidOperationException**, TOM também pode gerar várias exceções específicas de TOM.  

TOM exceções são derivadas de [classe AmoException](http://msdn.microsoft.com/library/microsoft.analysisservices.amoexception.aspx), que abrangem as duas exceções específicas de TOM e AMO. 

Para ilustrar a manipulação de exceção no TOM, vamos examinar uma das exceções mais comuns, que é [OperationException classe](http://msdn.microsoft.com/library/microsoft.analysisservices.operationexception.aspx).

**OperationException** é lançada quando um usuário inicia uma operação no servidor do Analysis Services e o servidor não pode executar uma operação, porque a ação foi ilegal ou devido a outro erro interno ou externo. 

Quando lançada, * * OperationException * * o objeto contém uma lista de erros XMLA retornados pelo servidor. 

Observe que o servidor não aceitará as alterações que são inválidas. Se isso ocorrer, reverta a **modelo** árvore de volta para o último estado bom conhecido usando o [UndoLocalChanges método](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.model.undolocalchanges.aspx), corrija o modelo e envie novamente. 

## <a name="code-example-handle-exceptions"></a>Exemplo de código: manipular exceções 
 
```
 try 
 { 
  // Change the Model, for example create a table. 
  // … 
   model.saveChanges(); 
 } 
  catch(operationException ex) 
 { 
  foreach(XmlaError err in ex.Results.OfType<XmlaError>().cast<XmlaError>()) 
  { 
   Console.WriteLine(“Error returned from the server:” + err.Messsage ); 
  } 
 } 
```

## <a name="next-steps"></a>Próximas etapas

Outras exceções relevantes incluem o seguinte:

- [Classe TomInternalException](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.tominternalexception.aspx)
- [Classe TomValidationException](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.tomvalidationexception.aspx)
- [Classe JsonSerializationException](http://www.newtonsoft.com/json/help/html/T_Newtonsoft_Json_JsonSerializationException.htm)
