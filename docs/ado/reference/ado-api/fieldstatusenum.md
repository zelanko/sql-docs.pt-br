---
description: FieldStatusEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 06044b54be7066deb5cf7510f060716106816805
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443708"
---
# <a name="fieldstatusenum"></a>FieldStatusEnum
Especifica o [status](../../../ado/reference/ado-api/status-property-ado-field.md) de um [objeto de campo](../../../ado/reference/ado-api/field-object.md).  
  
 Os valores de **adFieldPending \* ** indicam a operação que fez com que o status fosse definido e pode ser combinado com outros valores de status.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adFieldAlreadyExists**|26|Indica que o campo especificado já existe.|  
|**adFieldBadStatus**|12|Indica que um valor de status inválido foi enviado do ADO para o provedor de OLE DB. As possíveis causas incluem um provedor OLE DB 1,0 ou 1,1 ou uma combinação imprópria de [valor](../../../ado/reference/ado-api/value-property-ado.md) e [status](../../../ado/reference/ado-api/status-property-ado-field.md).|  
|**adFieldCannotComplete**|20|Indica que o servidor da URL especificada pela [origem](../../../ado/reference/ado-api/source-property-ado-record.md) não pôde concluir a operação.|  
|**adFieldCannotDeleteSource**|23|Indica que durante uma operação de movimentação, uma árvore ou subárvore foi movida para um novo local, mas a origem não pôde ser excluída.|  
|**adFieldCantConvertValue**|2|Indica que o campo não pode ser recuperado ou armazenado sem perda de dados.|  
|**adFieldCantCreate**|7|Indica que o campo não pôde ser adicionado porque o provedor excedeu uma limitação (como o número de campos permitidos).|  
|**adFieldDataOverflow**|6|Indica que os dados retornados do provedor estouram o tipo de dados do campo.|  
|**adFieldDefault**|13|Indica que o valor padrão do campo foi usado ao definir dados.|  
|**adFieldDoesNotExist**|16|Indica que o campo especificado não existe.|  
|**adFieldIgnore**|15|Indica que esse campo foi ignorado ao definir valores de dados na origem. O provedor não definiu nenhum valor.|  
|**adFieldIntegrityViolation**|10|Indica que o campo não pode ser modificado porque é uma entidade calculada ou derivada.|  
|**adFieldInvalidURL**|17|Indica que a URL da fonte de dados contém caracteres inválidos.|  
|**adFieldIsNull**|3|Indica que o provedor retornou um valor de variante do tipo VT_NULL e que o campo não está vazio.|  
|**adFieldOK**|0|Padrão. Indica que o campo foi adicionado ou excluído com êxito.|  
|**adFieldOutOfSpace**|22|Indica que o provedor não pode obter espaço de armazenamento suficiente para concluir uma operação de movimentação ou cópia.|  
|**adFieldPendingChange**|0x40000|Indica que o campo foi excluído e, em seguida, adicionado novamente, talvez com um tipo de dados diferente, ou que o valor do campo que anteriormente tinha um status de **adFieldOK** foi alterado. A forma final do campo modificará a coleção [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) depois que o método [Update](../../../ado/reference/ado-api/update-method.md) for chamado.|  
|**adFieldPendingDelete**|0x20000|Indica que a operação de **exclusão** fez com que o status fosse definido. O campo foi marcado para exclusão da coleção **Fields** depois que o método **Update** é chamado.|  
|**adFieldPendingInsert**|0x10000|Indica que a operação de **acréscimo** fez com que o status fosse definido. O **campo** foi marcado para ser adicionado à coleção **Fields** depois que o método **Update** é chamado.|  
|**adFieldPendingUnknown**|0x80000|Indica que o provedor não pode determinar qual operação causou o status do campo a ser definido.|  
|**adFieldPendingUnknownDelete**|0x100000|Indica que o provedor não pode determinar qual operação causou o status do campo a ser definido e que o campo será excluído da coleção **Fields** depois que o método **Update** for chamado.|  
|**adFieldPermissionDenied**|9|Indica que o campo não pode ser modificado porque está definido como somente leitura.|  
|**adFieldReadOnly**|24|Indica que o campo na fonte de dados é definido como somente leitura.|  
|**adFieldResourceExists**|19|Indica que o provedor não pôde executar a operação porque um objeto já existe na URL de destino e não é capaz de substituir o objeto.|  
|**adFieldResourceLocked**|18|Indica que o provedor não pôde executar a operação porque a fonte de dados está bloqueada por um ou mais aplicativos ou processos.|  
|**adFieldResourceOutOfScope**|25|Indica que uma URL de origem ou de destino está fora do escopo do registro atual.|  
|**adFieldSchemaViolation**|11|Indica que o valor violou a restrição de esquema da fonte de dados para o campo.|  
|**adFieldSignMismatch**|5|Indica que o valor de dados retornado pelo provedor foi assinado, mas o tipo de dados do valor do campo ADO não estava assinado.|  
|**adFieldTruncated**|4|Indica que os dados de comprimento variável foram truncados ao ler da fonte de dados.|  
|**adFieldUnavailable**|8|Indica que o provedor não pôde determinar o valor ao ler a partir da fonte de dados. Por exemplo, a linha acabou de ser criada, o valor padrão para a coluna não estava disponível e um novo valor ainda não tinha sido especificado.|  
|**adFieldVolumeNotFound**|21|Indica que o provedor não pode localizar o volume de armazenamento indicado pela URL.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade Status (campo ADO)](../../../ado/reference/ado-api/status-property-ado-field.md)
