---
description: Propriedade Sort
title: Propriedade de classificação | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::get_Sort
- Recordset15::put_Sort
- Recordset15::PutSort
- Recordset15::GetSort
- Recordset15::Sort
helpviewer_keywords:
- DESC [ADO]
- ASC [ADO]
- Sort property [ADO]
ms.assetid: 3683ffa0-6f93-4906-9533-ef6942f24f39
author: rothja
ms.author: jroth
ms.openlocfilehash: 9397d99d2d020fcf2c703bd96420ee4af4b1a610
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988987"
---
# <a name="sort-property"></a>Propriedade Sort
Indica um ou mais nomes de campo nos quais o [conjunto de registros](./recordset-object-ado.md) é classificado e se cada campo é classificado em ordem crescente ou decrescente.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **cadeia de caracteres** que indica os nomes de campo no **conjunto de registros** no qual classificar. Cada nome é separado por uma vírgula e é opcionalmente seguido por um espaço em branco e a palavra-chave, **ASC**, que classifica o campo em ordem crescente, ou **desc**, que classifica o campo em ordem decrescente. Por padrão, se nenhuma palavra-chave for especificada, o campo será classificado em ordem crescente.  
  
## <a name="remarks"></a>Comentários  
 Esta propriedade requer que a propriedade [CursorLocation](./cursorlocation-property-ado.md) seja definida como **adUseClient**. Um índice temporário será criado para cada campo especificado na propriedade **Sort** se um índice ainda não existir.  
  
 A operação de classificação é eficiente porque os dados não são reorganizados fisicamente, mas são simplesmente acessados na ordem especificada pelo índice.  
  
 Quando o valor da propriedade **Sort** é algo diferente de uma cadeia de caracteres vazia, a ordem da propriedade de **classificação** tem precedência sobre a ordem especificada em uma cláusula **order by** incluída na instrução SQL usada para abrir o **conjunto de registros**.  
  
 O **conjunto de registros** não precisa ser aberto antes de acessar a propriedade **Sort** ; Ele pode ser definido a qualquer momento depois que o objeto **Recordset** é instanciado.  
  
 Definir a propriedade **Sort** como uma cadeia de caracteres vazia redefinirá as linhas para sua ordem original e excluirá índices temporários. Os índices existentes não serão excluídos.  
  
 Suponha que um **conjunto de registros** contenha três campos nomeados *FirstName*, *inicialdomeio*e *LastName*. Defina a propriedade de **classificação** como a cadeia de caracteres " `lastName DESC, firstName ASC` ", que ordenará o **conjunto de registros** por sobrenome em ordem decrescente, em seguida, pelo nome em ordem crescente. A inicial do meio é ignorada.  
  
 Nenhum campo pode ser nomeado "ASC" ou "DESC" porque esses nomes entram em conflito com as palavras-chave **ASC** e **desc**. Você pode criar um alias para um campo com um nome conflitante usando **a palavra-chave as na** consulta que retorna o **conjunto de registros**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da Propriedade Sort (VB)](./sort-property-example-vb.md)   
 [Exemplo da Propriedade Sort (VC + +)](./sort-property-example-vc.md)   
 [Otimizar propriedade-dinâmica (ADO)](./optimize-property-dynamic-ado.md)   
 [Propriedade SortColumn (RDS)](../rds-api/sortcolumn-property-rds.md)   
 [Propriedade SortDirection (RDS)](../rds-api/sortdirection-property-rds.md)