---
title: Propriedade de classificação | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 946314f7be9f6c39d47a3f26b577e10834064dab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930941"
---
# <a name="sort-property"></a>Propriedade Sort
Indica um ou mais nomes de campo no qual o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) é classificada, e se cada campo é classificado em ordem crescente ou decrescente.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** nomes de valor que indica o campo na **Recordset** na qual classificar. Cada nome é separado por uma vírgula e, opcionalmente, é seguido por um espaço em branco e a palavra-chave **ASC**, que classifica o campo em ordem crescente, ou **DESC**, que classifica o campo em ordem decrescente. Por padrão, se nenhuma palavra-chave for especificado, o campo é classificado em ordem crescente.  
  
## <a name="remarks"></a>Comentários  
 Esta propriedade requer o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade ser definida como **adUseClient**. Um índice temporário será criado para cada campo especificado na **classificação** propriedade se um índice não existir.  
  
 A operação de classificação é eficiente porque os dados não são reorganizados fisicamente, mas simplesmente são acessados na ordem especificada pelo índice.  
  
 Quando o valor da **classificação** propriedade é algo diferente de uma cadeia de caracteres vazia, o **classificação** ordem de propriedade tem precedência sobre a ordem especificada em um **ORDER BY** cláusula incluído na instrução SQL usada para abrir o **conjunto de registros**.  
  
 O **conjunto de registros** não precisa ser aberta antes de acessar o **classificação** propriedade; ele pode ser definido a qualquer momento após a **Recordset** objeto é instanciado.  
  
 Definindo o **classificação** propriedade como uma cadeia de caracteres vazia será redefinir as linhas à sua ordem original e excluir índices temporários. Os índices existentes não serão excluídos.  
  
 Suponha que um **conjunto de registros** contém três campos denominados *firstName*, *middleInitial*, e *lastName*. Defina a **classificação** propriedade na cadeia de caracteres "`lastName DESC, firstName ASC`", qual será a ordem a **conjunto de registros** por sobrenome em ordem decrescente e, em seguida, por nome em ordem crescente. A inicial do meio será ignorada.  
  
 Nenhum campo pode ser nomeado "ASC" ou "DESC" porque esses nomes em conflito com as palavras-chave **ASC** e **DESC**. Você pode criar um alias para um campo com um nome conflitante, usando o **AS** palavra-chave na consulta que retorna os **conjunto de registros**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade Sort (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [Exemplo da propriedade Sort (VC + +)](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [Otimizar a propriedade dinâmica (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Propriedade SortColumn (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Propriedade SortDirection (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)
