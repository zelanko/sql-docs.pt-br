---
title: Propriedade Bookmark (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Bookmark
helpviewer_keywords:
- Bookmark property [ADO]
ms.assetid: 481dcc93-487b-490e-ac58-a1e9b2ebfd43
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61fa4619bd70b170f13dbc879748364f019f8bdd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62821160"
---
# <a name="bookmark-property-ado"></a>Propriedade Bookmark (ADO)
Indica um marcador que identifica exclusivamente o registro atual em um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) do objeto ou define o registro atual em um **Recordset** objeto para o registro identificado por um indicador válido.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **Variant** expressão que é avaliada como um indicador válido.  
  
## <a name="remarks"></a>Comentários  
 Use o **indicador** propriedade para salvar a posição do registro atual e retornar a esse registro a qualquer momento. Indicadores estão disponíveis apenas nos **Recordset** objetos que dão suporte à funcionalidade de indicador.  
  
 Quando você abre um **Recordset** do objeto, cada um dos seus registros tem um indicador exclusivo. Para salvar o indicador para o registro atual, atribua o valor da **indicador** propriedade a uma variável. Para retornar rapidamente a esse registro a qualquer momento após a mudança para um registro diferente, defina as **conjunto de registros** do objeto **indicador** propriedade para o valor dessa variável.  
  
 O usuário pode não ser capaz de exibir o valor do indicador. Além disso, os usuários não devem esperar indicadores estejam diretamente comparáveis, porque os dois indicadores que se referem ao mesmo registro podem ter valores diferentes.  
  
 Se você usar o [Clone](../../../ado/reference/ado-api/clone-method-ado.md) método para criar uma cópia de um **conjunto de registros** objeto, o **indicador** configurações de propriedade para o original e a duplicata **conjunto de registros**  objetos são idênticos, e você pode usá-los de maneira intercambiável. No entanto, você não pode usar indicadores de diferentes **Recordset** objetos intercambiavelmente, mesmo que elas foram criadas da mesma fonte ou do comando.  
  
> [!NOTE]
>  **Uso do serviço de dados remotos** quando usado em um lado do cliente **conjunto de registros** objeto, o **indicador** propriedade está sempre disponível.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [BOF, EOF e exemplo de propriedades do indicador (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF, EOF e exemplo de propriedades do indicador (VC + +)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
