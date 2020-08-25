---
description: Método Find (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0312fb8a8f91e8b56cb6c29a3a64b3a36bcec69d
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775225"
---
# <a name="find-method-ado"></a>Método Find (ADO)
Pesquisa um [conjunto de registros](./recordset-object-ado.md) para a linha que satisfaz os critérios especificados. Opcionalmente, a direção da pesquisa, a linha inicial e o deslocamento da linha inicial podem ser especificados. Se os critérios forem atendidos, a posição da linha atual será definida no registro encontrado; caso contrário, a posição será definida como o final (ou início) do **conjunto de registros**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Critérios*  
 Um valor de **cadeia de caracteres** que contém uma instrução que especifica o nome da coluna, o operador de comparação e o valor a ser usado na pesquisa.  
  
 *SkipRows*  
 Opcional. Um valor **longo** , cujo valor padrão é zero, que especifica o deslocamento de linha da linha atual ou do indicador *inicial* para iniciar a pesquisa. Por padrão, a pesquisa será iniciada na linha atual.  
  
 *SearchDirection*  
 Opcional. Um valor [SearchDirectionEnum](./searchdirectionenum.md) que especifica se a pesquisa deve começar na linha atual ou na próxima linha disponível na direção da pesquisa. Uma pesquisa malsucedida será interrompida no final do conjunto de **registros** se o valor for **adSearchForward**. Uma pesquisa malsucedida será interrompida no início do conjunto de **registros** se o valor for **adSearchBackward**.  
  
 *Iniciar*  
 Opcional. Um indicador de **variante** que funciona como a posição inicial da pesquisa.  
  
## <a name="remarks"></a>Comentários  
 Somente um nome de coluna única pode ser especificado em *critérios*. Este método não oferece suporte a pesquisas de várias colunas.  
  
 O operador de comparação em *critérios* pode ser " **>** " (maior que), "* * * \<**" (less than), "=" (equal), "> =" (maior ou igual), "<=" (menor ou igual), "<>" (não igual) ou "Like" (correspondência de padrões).  
  
 O valor em *critérios* pode ser uma cadeia de caracteres, um número de ponto flutuante ou uma data. Os valores de cadeia de caracteres são delimitados por aspas simples ou marcas "#" (sinal numérico) (por exemplo, "State = ' WA '" ou "state = #WA #"). Os valores de data são delimitados com marcas "#" (sinal numérico) (por exemplo, "start_date > #7/22/97 #"). Esses valores podem conter horas, minutos e segundos para indicar carimbos de data/hora, mas não devem conter milissegundos ou erros ocorrerão.  
  
 Se o operador de comparação for "Like", o valor da cadeia de caracteres poderá conter um asterisco (*) para localizar uma ou mais ocorrências de qualquer caractere ou Subcadeia de caracteres. Por exemplo, "estado like" \* "corresponde a Maine e a Massachusetts. Você também pode usar asteriscos à esquerda e à direita para localizar uma subcadeia de caracteres contida nos valores. Por exemplo, "estado como" \* como " \* " corresponde a Alasca, Arkansas e Massachusetts.  
  
 Os asteriscos só podem ser usados no final de uma cadeia de caracteres de critérios ou no início e no final de uma cadeia de caracteres de critério, conforme mostrado acima. Você não pode usar o asterisco como um curinga à esquerda (' * Str ') ou como um curinga incorporado ( \* r ' s). Isso causará um erro.  
  
> [!NOTE]
>  Ocorrerá um erro se uma posição de linha atual não for definida antes de chamar **Find**. Qualquer método que define a posição da linha, como [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md), deve ser chamado antes de chamar **Find**.  
  
> [!NOTE]
>  Se você chamar o método **Find** em um conjunto de registros e a posição atual no conjunto de registros estiver no último registro ou no final do arquivo (EOF), você não encontrará nada. Você precisa chamar o método **MoveFirst** para definir a posição/cursor atual como o início do conjunto de registros.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Find (VB)](./find-method-example-vb.md)   
 [Propriedade index](./index-property.md)   
 [Otimizar propriedade-dinâmica (ADO)](./optimize-property-dynamic-ado.md)   
 [Método Seek](./seek-method.md)