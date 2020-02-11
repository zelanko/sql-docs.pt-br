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
ms.openlocfilehash: 48b1c90b59b220841aa45f618fdfda5ff2db82da
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920348"
---
# <a name="bookmark-property-ado"></a>Propriedade Bookmark (ADO)
Indica um indicador que identifica exclusivamente o registro atual em um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ou define o registro atual em um objeto **Recordset** para o registro identificado por um indicador válido.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna uma expressão **Variant** que é avaliada como um indicador válido.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Bookmark** para salvar a posição do registro atual e retornar para esse registro a qualquer momento. Os indicadores estão disponíveis somente em objetos **Recordset** que dão suporte à funcionalidade de indicador.  
  
 Quando você abre um objeto **Recordset** , cada um de seus registros tem um indicador exclusivo. Para salvar o indicador para o registro atual, atribua o valor da propriedade **Bookmark** a uma variável. Para retornar rapidamente a esse registro a qualquer momento após a mudança para um registro diferente, defina a propriedade **Bookmark** do objeto **Recordset** para o valor dessa variável.  
  
 O usuário pode não conseguir exibir o valor do indicador. Além disso, os usuários não devem esperar que os indicadores sejam diretamente comparáveis, pois dois indicadores que se referem ao mesmo registro podem ter valores diferentes.  
  
 Se você usar o método [clone](../../../ado/reference/ado-api/clone-method-ado.md) para criar uma cópia de um objeto **Recordset** , as configurações de propriedade **Bookmark** para os objetos **Recordset** original e Duplicate serão idênticas e você poderá usá-las de maneira intercambiável. No entanto, você não pode usar indicadores de diferentes objetos **Recordset** de forma intercambiável, mesmo que eles tenham sido criados a partir da mesma fonte ou comando.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Quando usado em um objeto **Recordset** do lado do cliente, a propriedade **Bookmark** está sempre disponível.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades BOF, EOF e Bookmark (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [Exemplo das propriedades BOF, EOF e Bookmark (VC + +)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
