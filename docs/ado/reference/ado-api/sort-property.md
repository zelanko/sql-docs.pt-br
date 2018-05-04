---
title: Propriedade de classificação | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4fcc0421d855236b27d5babe75424f929c086ab8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sort-property"></a>Propriedade de classificação
Indica um ou mais nomes de campo no qual o [registros](../../../ado/reference/ado-api/recordset-object-ado.md) é classificada, e se cada campo é classificado em ordem crescente ou decrescente.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor que indica o campo de nomes no **registros** na qual classificar. Cada nome é separado por uma vírgula e, opcionalmente, é seguido por um espaço em branco e a palavra-chave **ASC**, que classifica o campo em ordem crescente, ou **DESC**, que classifica o campo em ordem decrescente. Por padrão, se nenhuma palavra-chave for especificado, o campo é classificado em ordem crescente.  
  
## <a name="remarks"></a>Remarks  
 Esta propriedade requer o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade a ser definida **adUseClient**. Um índice temporário será criado para cada campo especificado no **classificação** propriedade se um índice já não existe.  
  
 A operação de classificação é eficiente, porque os dados não é fisicamente reorganizados, mas simplesmente são acessados na ordem especificada pelo índice.  
  
 Quando o valor da **classificação** propriedade é algo diferente de uma cadeia de caracteres vazia, o **classificação** ordem de propriedade tem precedência sobre a ordem especificada em um **ORDER BY** cláusula incluído na instrução SQL usada para abrir o **registros**.  
  
 O **registros** não precisa ser aberta antes de acessar o **classificação** propriedade; pode ser definido a qualquer momento após o **registros** objeto é instanciado.  
  
 Definindo o **classificação** redefinirá as linhas à sua ordem original e excluir índices temporários propriedade como uma cadeia de caracteres vazia. Os índices existentes não serão excluídos.  
  
 Suponha que um **registros** contém três campos denominados *firstName*, *middleInitial*, e *lastName*. Definir o **classificação** propriedade para a cadeia de caracteres "`lastName DESC, firstName ASC`", que pedir o **conjunto de registros** por sobrenome em ordem decrescente e, em seguida, por nome em ordem crescente. A inicial do meio é ignorada.  
  
 Nenhum campo pode ser nomeado "ASC" ou "DESC" porque esses nomes em conflito com as palavras-chave **ASC** e **DESC**. Você pode criar um alias para um campo com um nome conflitante usando o **AS** palavra-chave na consulta que retorna o **registros**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedade de classificação (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [Exemplo de propriedade de classificação (VC + +)](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [Otimizar a propriedade dinâmica (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Propriedade SortColumn (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Propriedade SortDirection (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)
