---
title: "Localizar o método (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::raw_Find
- Recordset15::Find
helpviewer_keywords: Find method [ADO]
ms.assetid: 55c9810a-d8ca-46c2-a9dc-80e7ee7aa188
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3f2a2af33a7355084f85e80fda3ff92e5415adcb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="find-method-ado"></a>Localizar o método (ADO)
Pesquisa um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) para a linha que satisfaz os critérios especificados. Opcionalmente, a direção da pesquisa, linha inicial e o deslocamento da linha inicial pode ser especificada. Se os critérios forem atendidos, a posição da linha atual é definida no registro encontrado; Caso contrário, a posição é definida ao final (ou início) da **registros**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Critérios*  
 Um **cadeia de caracteres** valor que contém uma instrução, especificando o nome da coluna, o operador de comparação e o valor para usar na pesquisa.  
  
 *SkipRows*  
 Opcional*.* Um **longo** valor, cujo valor padrão é zero, que especifica o deslocamento da linha da linha atual ou *iniciar* indicador para iniciar a pesquisa. Por padrão, a pesquisa será iniciada na linha atual.  
  
 *SearchDirection*  
 Opcional*.* Um [SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md) valor que especifica se a pesquisa deve começar na linha atual ou a próxima linha disponível na direção da pesquisa. Para de pesquisas malsucedidas no final de **registros** se o valor for **adSearchForward**. Uma pesquisa bem-sucedida é interrompida no início do **registros** se o valor for **adSearchBackward**.  
  
 *Iniciar*  
 Opcional. Um **Variant** indicador que funciona como a posição inicial da pesquisa.  
  
## <a name="remarks"></a>Remarks  
 Apenas um nome de coluna única que pode ser especificado em *critérios*. Este método não oferece suporte a pesquisas de várias colunas.  
  
 O operador de comparação em *critérios* pode ser "**>**"(maior que),"**\<**" (menor que), "=" (igual), "> =" (maior ou igual) "< =" (menor ou igual), "<>" (não igual), ou "como" (correspondência de padrão).  
  
 O valor em *critérios* pode ser uma cadeia de caracteres, número de ponto flutuante ou data. Os valores de cadeia de caracteres são delimitados com aspas simples ou marcas "#" (sinal numérico) (por exemplo, "estado = 'WA'" ou "estado = WA # #"). Valores de data são delimitados por marcas de "#" (sinal numérico) (por exemplo, "start_date > # # 22/7/97"). Esses valores podem conter horas, minutos e segundos para indicar os carimbos de hora, mas não devem conter milissegundos ou ocorrerão erros.  
  
 Se o operador de comparação é "como", o valor de cadeia de caracteres pode conter um asterisco (*) para localizar uma ou mais ocorrências de qualquer caractere ou uma subcadeia de caracteres. Por exemplo, "estado como estou\*'" corresponde a rio grande do Norte e Massachusetts. Você também pode usar asteriscos à esquerda e à direita para localizar uma subcadeia de caracteres contida dentro dos valores. Por exemplo, "estado como '\*como\*'" corresponde a Alaska, Arkansas e Massachusetts.  
  
 Asteriscos podem ser usados somente no final de uma cadeia de caracteres de critérios ou no início e no final de uma cadeia de caracteres de critérios, como mostrado acima. Você não pode usar o asterisco como um caractere curinga à esquerda ('* str'), ou como um curinga incorporado ('s\*r'). Isso causará um erro.  
  
> [!NOTE]
>  Ocorrerá um erro se a posição de linha atual não está definida antes de chamar **localizar**. Qualquer método que define a posição de linha, como [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), deve ser chamado antes de chamar **localizar**.  
  
> [!NOTE]
>  Se você chamar o **localizar** método em um conjunto de registros e a posição atual no conjunto de registros é o último registro ou o final do arquivo (EOF), você não encontrará nada. Você precisa chamar o **MoveFirst** método para definir o posição atual/cursor para o início do conjunto de registros.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Localizar o exemplo de método (VB)](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [Propriedade Index](../../../ado/reference/ado-api/index-property.md)   
 [Otimizar a propriedade dinâmica (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Método Seek](../../../ado/reference/ado-api/seek-method.md)
