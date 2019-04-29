---
title: Método Find (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Find
- Recordset15::Find
helpviewer_keywords:
- Find method [ADO]
ms.assetid: 55c9810a-d8ca-46c2-a9dc-80e7ee7aa188
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e71776a43aa338246b4acb3b4d9f620c19234f0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028123"
---
# <a name="find-method-ado"></a>Método Find (ADO)
Pesquisas de um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) para a linha que satisfaz os critérios especificados. Opcionalmente, a direção da pesquisa, a linha inicial e deslocamento da linha inicial pode ser especificada. Se os critérios forem atendidos, a posição da linha atual é definida no registro encontrado; Caso contrário, a posição é definida até o final (ou inicial) do **conjunto de registros**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Critérios*  
 Um **cadeia de caracteres** valor que contém uma instrução, especificando o nome da coluna, o operador de comparação e o valor para usar na pesquisa.  
  
 *SkipRows*  
 Opcional *.* Um **longo** valor, cujo valor padrão é zero, que especifica o deslocamento da linha da linha atual ou *iniciar* indicador para iniciar a pesquisa. Por padrão, a pesquisa será iniciada na linha atual.  
  
 *SearchDirection*  
 Opcional *.* Um [SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md) valor que especifica se a pesquisa deve começar na linha atual ou a próxima linha disponível na direção da pesquisa. Uma pesquisa bem-sucedida é interrompida no final do **conjunto de registros** se o valor estiver **adSearchForward**. Uma pesquisa bem-sucedida é interrompida no início do **conjunto de registros** se o valor estiver **adSearchBackward**.  
  
 *Iniciar*  
 Opcional. Um **Variant** indicador que funciona como a posição inicial da pesquisa.  
  
## <a name="remarks"></a>Comentários  
 Somente um nome de coluna única pode ser especificado na *critérios*. Esse método não dá suporte a pesquisas de várias colunas.  
  
 O operador de comparação na *critérios* pode ser "**>**"(maior que),"**\<**" (menor que), "=" (igual), "> =" (maior que ou igual), "< =" (menor ou igual), "<>" (não igual), ou "como" (correspondência de padrões).  
  
 O valor em *critérios* pode ser uma cadeia de caracteres, número de ponto flutuante ou data. Os valores de cadeia de caracteres são delimitados com aspas simples ou marcas de "#" (sinal numérico) (por exemplo, "estado = 'WA'" ou "estado = WA # #"). Valores de data são delimitados com marcas de "#" (sinal numérico) (por exemplo, "start_date > # 97 / #7/22"). Esses valores podem conter horas, minutos e segundos para indicar os carimbos de hora, mas não devem conter milissegundos ou ocorrerão erros.  
  
 Se o operador de comparação é "como", o valor de cadeia de caracteres pode conter um asterisco (*) para localizar uma ou mais ocorrências de qualquer caractere ou subcadeia de caracteres. Por exemplo, "estado, como estou\*'" corresponde a Maine e Massachusetts. Você também pode usar asteriscos à esquerda e à direita para localizar uma subcadeia de caracteres contida dentro dos valores. Por exemplo, "estado como '\*como\*'" corresponde a Alaska, Arkansas e Massachusetts.  
  
 Os asteriscos podem ser usados somente no final de uma cadeia de caracteres de critérios ou no início e no final de uma cadeia de caracteres de critérios, como mostrado acima. Você não pode usar o asterisco como curinga à esquerda ('* str'), ou como um curinga incorporado ('s\*r'). Isso causará um erro.  
  
> [!NOTE]
>  Ocorrerá um erro se uma posição de linha atual não for definida antes de chamar **localizar**. Qualquer método que define a posição de linha, como [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), deve ser chamado antes de chamar **localizar**.  
  
> [!NOTE]
>  Se você chamar o **localizar** método em um conjunto de registros e a posição atual no conjunto de registros está no último registro ou no final do arquivo (EOF), você não encontrará nada. Você precisa chamar o **MoveFirst** método para definir o posição/cursor atual para o início do conjunto de registros.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Encontre um exemplo do método (VB)](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [Propriedade Index](../../../ado/reference/ado-api/index-property.md)   
 [Otimizar a propriedade dinâmica (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Método Seek](../../../ado/reference/ado-api/seek-method.md)
