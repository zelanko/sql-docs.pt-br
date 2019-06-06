---
title: FieldStatusEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldStatusEnum
helpviewer_keywords:
- FieldStatusEnum enumeration [ADO]
ms.assetid: e06da1e2-303f-41b2-a3b0-61e233da152c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1ba7fe546f7ac8e1a036fc8fe7e5f523ebf09d4c
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719212"
---
# <a name="fieldstatusenum"></a>FieldStatusEnum
Especifica o [status](../../../ado/reference/ado-api/status-property-ado-field.md) de uma [objeto Field](../../../ado/reference/ado-api/field-object.md).  
  
 O **adFieldPending\***  valores indicam a operação que causou o status ser definido e pode ser combinada com outros valores de status.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adFieldAlreadyExists**|26|Indica que o campo especificado já existe.|  
|**adFieldBadStatus**|12|Indica que um valor de status inválido foi enviado do ADO para o provedor OLE DB. Possíveis causas incluem um 1.0 OLE DB ou provedor 1.1 ou uma combinação incorreta dos [valor](../../../ado/reference/ado-api/value-property-ado.md) e [Status](../../../ado/reference/ado-api/status-property-ado-field.md).|  
|**adFieldCannotComplete**|20|Indica que o servidor da URL especificado por [origem](../../../ado/reference/ado-api/source-property-ado-record.md) não foi possível concluir a operação.|  
|**adFieldCannotDeleteSource**|23|Indica que, durante uma operação de movimentação, uma árvore ou uma subárvore foi movido para um novo local, mas a fonte não pôde ser excluída.|  
|**adFieldCantConvertValue**|2|Indica que o campo não pode ser recuperado ou armazenado sem perda de dados.|  
|**adFieldCantCreate**|7|Indica que o campo não pôde ser adicionado porque o provedor excedeu uma limitação (como o número de campos são permitidos).|  
|**adFieldDataOverflow**|6|Indica que a retornada do provedor de dados estouraram o tipo de dados do campo.|  
|**adFieldDefault**|13|Indica que o valor padrão para o campo foi usado ao definir os dados.|  
|**adFieldDoesNotExist**|16|Indica que o campo especificado não existe.|  
|**adFieldIgnore**|15|Indica que esse campo foi ignorado quando valores na fonte de dados de configuração. O provedor não definir nenhum valor.|  
|**adFieldIntegrityViolation**|10|Indica que o campo não pode ser modificado porque é uma entidade calculada ou derivada.|  
|**adFieldInvalidURL**|17|Indica que a URL da fonte de dados contém caracteres inválidos.|  
|**adFieldIsNull**|3|Indica que o provedor retornou um valor de VARIANTE do tipo VT_NULL e se o campo não está vazio.|  
|**adFieldOK**|0|Padrão. Indica que o campo foi adicionado ou excluído com êxito.|  
|**adFieldOutOfSpace**|22|Indica que o provedor é não é possível obter espaço de armazenamento suficiente para concluir uma movimentação ou a operação de cópia.|  
|**adFieldPendingChange**|0x40000|Indica que o campo foi excluído e, em seguida, adicionado novamente, talvez com um tipo de dados diferente, ou que o valor do campo que anteriormente tinha um status de **adFieldOK** foi alterado. Modifica a forma final do campo a [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção após o [atualização](../../../ado/reference/ado-api/update-method.md) método é chamado.|  
|**adFieldPendingDelete**|0x20000|Indica que o **excluir** operação causou o status a ser definido. O campo foi marcado para exclusão do **campos** coleção após o **atualização** método é chamado.|  
|**adFieldPendingInsert**|0x10000|Indica que o **Append** operação causou o status a ser definido. O **campo** foi marcado para ser adicionado à **campos** coleção após o **atualização** método é chamado.|  
|**adFieldPendingUnknown**|0x80000|Indica que o provedor não pode determinar quais status de campo de operação que causou a ser definido.|  
|**adFieldPendingUnknownDelete**|0x100000|Indica que o provedor não pode determinar qual operação causou o status de campo a ser definido e que o campo será excluído do **campos** coleção após o **atualização** método é chamado.|  
|**adFieldPermissionDenied**|9|Indica que o campo não pode ser modificado porque ele está definido como somente leitura.|  
|**adFieldReadOnly**|24|Indica que o campo na fonte de dados é definido como somente leitura.|  
|**adFieldResourceExists**|19|Indica que o provedor não pôde executar a operação porque já existe um objeto a URL de destino e não é capaz de substituir o objeto.|  
|**adFieldResourceLocked**|18|Indica que o provedor não pôde executar a operação porque a fonte de dados está bloqueada por um ou mais outros aplicativos ou o processo.|  
|**adFieldResourceOutOfScope**|25|Indica que uma URL de origem ou destino está fora do escopo do registro atual.|  
|**adFieldSchemaViolation**|11|Indica que o valor violou a restrição de esquema de fonte de dados para o campo.|  
|**adFieldSignMismatch**|5|Indica que o valor de dados retornado pelo provedor foi assinado, mas o tipo de dados do valor do campo ADO não estava assinado.|  
|**adFieldTruncated**|4|Indica que os dados de comprimento variável foram truncados durante a leitura da fonte de dados.|  
|**adFieldUnavailable**|8|Indica que o provedor não pôde determinar o valor durante a leitura da fonte de dados. Por exemplo, a linha acabou de ser criada, o valor padrão para a coluna não estava disponível e um novo valor ainda não tivesse sido especificado.|  
|**adFieldVolumeNotFound**|21|Indica que o provedor é incapaz de localizar o volume de armazenamento, indicado pela URL.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade Status (campo ADO)](../../../ado/reference/ado-api/status-property-ado-field.md)
