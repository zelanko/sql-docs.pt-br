---
title: Marcador de propriedade (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Bookmark
helpviewer_keywords:
- Bookmark property [ADO]
ms.assetid: 481dcc93-487b-490e-ac58-a1e9b2ebfd43
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e645300f604e1880f98fd8d99cea8599062f72f
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35276195"
---
# <a name="bookmark-property-ado"></a>Propriedade Bookmark (ADO)
Indica um marcador que identifica exclusivamente o registro atual em um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) do objeto ou define o registro atual em um **Recordset** objeto para o registro identificado por um indicador válido.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **Variant** expressão que avalia um indicador válido.  
  
## <a name="remarks"></a>Remarks  
 Use o **indicador** propriedade para salvar a posição do registro atual e retornar a esse registro a qualquer momento. Indicadores estão disponíveis apenas em **registros** objetos que dão suporte à funcionalidade de indicador.  
  
 Quando você abre um **registros** do objeto, cada um dos seus registros possui um indicador exclusivo. Para salvar o indicador para o registro atual, atribuir o valor de **indicador** propriedade a uma variável. Para retornar rapidamente a esse registro a qualquer momento depois de mover para um registro diferente, defina o **registros** do objeto **indicador** propriedade para o valor da variável.  
  
 O usuário pode não ser capaz de exibir o valor do indicador. Além disso, os usuários não devem ter indicadores para ser diretamente comparáveis, porque os dois indicadores que se referem ao mesmo registro podem ter valores diferentes.  
  
 Se você usar o [Clone](../../../ado/reference/ado-api/clone-method-ado.md) método para criar uma cópia de um **registros** objeto, o **indicador** as configurações de propriedade para o original e a duplicata **conjunto de registros**  objetos são idênticos e podem ser usados alternadamente. No entanto, você não pode usar indicadores de diferentes **registros** objetos alternadamente, mesmo se elas foram criadas da mesma fonte ou do comando.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** quando usado em um cliente **registros** objeto, o **indicador** propriedade sempre está disponível.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades do indicador (VB), BOF e EOF](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [Exemplo de propriedades do indicador (VC + +), BOF e EOF](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
