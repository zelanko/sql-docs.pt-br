---
title: ErrorValueEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ErrorValueEnum
helpviewer_keywords:
- ErrorValueEnum enumeration [ADO]
ms.assetid: 9469ba3a-5e4f-4a10-bbb8-a51a6c9660ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18117be8dccc64f7ed2583170cf062145836f337
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932871"
---
# <a name="errorvalueenum"></a>ErrorValueEnum
Especifica o tipo de erro de tempo de execução do ADO.  
  
 São listadas três formas do número do erro:  
  
-   Decimal positivo-os dois bytes baixos do número completo no formato decimal. Esse número é exibido na caixa de diálogo padrão Visual Basic mensagem de erro. Por exemplo, erro de tempo de execução ' 3707 '.  
  
-   Decimal negativo – a tradução decimal do número de erro completo.  
  
-   Hexadecimal-a representação hexadecimal do número de erro completo. O código de instalação do Windows está no quarto dígito. O código de recurso para números de erro do ADO é *um*. Por exemplo: 0x800***A***0E7B.  
  
> [!NOTE]
>  OLE DB erros podem ser passados para seu aplicativo ADO. Normalmente, eles podem ser identificados por um código de instalação do Windows de *4*. Por exemplo, 0x800***4***.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adErrBoundToCommand**|3707-2146824581 0x800A0E7B|Não é possível alterar a propriedade **ActiveConnection** de um objeto **Recordset** que tem um objeto **Command** como sua origem.|  
|**adErrCannotComplete**|3732-2146824556 0x800A0E94|O servidor não pode concluir a operação.|  
|**adErrCantChangeConnection**|3748-2146824540 0x800A0EA4|A conexão foi negada. Uma nova conexão solicitada tem características diferentes daquelas que já estão sendo usadas.|  
|**adErrCantChangeProvider**|3220-2146825068 0X800A0C94|O provedor fornecido difere do que já está sendo usado.|  
|**adErrCantConvertvalue**|3724-2146824564 0x800A0E8C|O valor de dados não pode ser convertido por razões diferentes de incompatibilidade de sinal ou estouro de dados. Por exemplo, a conversão teria dados truncados.|  
|**adErrCantCreate**|3725-2146824563 0x800A0E8D|O valor de dados não pode ser definido ou recuperado porque o tipo de dados do campo era desconhecido ou o provedor tinha recursos insuficientes para executar a operação.|  
|**adErrCatalogNotSet**|3747-2146824541 0x800A0EA3|A operação requer um **ParentCatalog**válido.|  
|**adErrColumnNotOnThisRow**|3726-2146824562 0x800A0E8E|O registro não contém este campo.|  
|**adErrDataConversion**|3421-2146824867 0x800A0D5D|O aplicativo usa um valor do tipo incorreto para a operação atual.|  
|**adErrDataOverflow**|3721-2146824567 0x800A0E89|O valor dos dados é muito grande para ser representado pelo tipo de dados Field.|  
|**adErrDelResOutOfScope**|3738-2146824550 0x800A0E9A|A URL do objeto a ser excluído está fora do escopo do registro atual.|  
|**adErrDenyNotSupported**|3750-2146824538 0x800A0EA6|O provedor não oferece suporte a restrições de compartilhamento.|  
|**adErrDenyTypeNotSupported**|3751-2146824537 0x800A0EA7|O provedor não oferece suporte ao tipo solicitado de restrição de compartilhamento.|  
|**adErrFeatureNotAvailable**|3251-2146825037 0x800A0CB3|O objeto ou provedor não pode executar a operação solicitada.|  
|**adErrFieldsUpdateFailed**|3749-2146824539 0x800A0EA5|Falha na atualização dos campos. Para obter mais informações, examine a propriedade **status** de objetos de campo individuais.|  
|**adErrIllegalOperation**|3219-2146825069 0x800A0C93|A operação não é permitida neste contexto.|  
|**adErrIntegrityViolation**|3719-2146824569 0x800A0E87|O valor dos dados está em conflito com as restrições de integridade do campo.|  
|**adErrInTransaction**|3246-2146825042 0x800A0CAE|O objeto de **conexão** não pode ser fechado explicitamente durante uma transação.|  
|**adErrInvalidArgument**|3001-2146825287 0x800A0BB9|Os argumentos são do tipo incorreto, estão fora do intervalo aceitável ou estão em conflito uns com os outros.|  
|**adErrInvalidConnection**|3709-2146824579 0x800A0E7D|A conexão não pode ser usada para executar esta operação. Ele está fechado ou é inválido neste contexto.|  
|**adErrInvalidParamInfo**|3708-2146824580 0x800A0E7C|O objeto de **parâmetro** está definido incorretamente. Informações inconsistentes ou incompletas foram fornecidas.|  
|**adErrInvalidTransaction**|3714-2146824574 0x800A0E82|A transação de coordenação é inválida ou não foi iniciada.|  
|**adErrInvalidURL**|3729-2146824559 0x800A0E91|A URL contém caracteres inválidos. Verifique se a URL foi digitada corretamente.|  
|**adErrItemNotFound**|3265-2146825023 0x800A0CC1|Não é possível encontrar o item na coleção que corresponde ao nome ou ordinal solicitado.|  
|**adErrNoCurrentRecord**|3021-2146825267 0x800A0BCD|**BOF** ou **EOF** é true ou o registro atual foi excluído. A operação solicitada requer um registro atual.|  
|**adErrNotExecuting**|3715-2146824573 0x800A0E83|Não é possível executar a operação enquanto não estiver em execução.|  
|**adErrNotReentrant**|3710-2146824578 0x800A0E7E|A operação não pode ser executada durante o processamento do evento.|  
|**adErrObjectClosed**|3704-2146824584 0x800A0E78|A operação não é permitida quando o objeto é fechado.|  
|**adErrObjectInCollection**|3367-2146824921 0x800A0D27|O objeto já está na coleção. Não é possível acrescentar.|  
|**adErrObjectNotSet**|3420-2146824868 0x800A0D5C|O objeto não é mais válido.|  
|**adErrObjectOpen**|3705-2146824583 0x800A0E79|A operação não é permitida quando o objeto está aberto.|  
|**adErrOpeningFile**|3002-2146825286 0x800A0BBA|Não foi possível abrir o arquivo.|  
|**adErrOperationCancelled**|3712-2146824576 0x800A0E80|A operação foi cancelada pelo usuário.|  
|**adErrOutOfSpace**|3734-2146824554 0x800A0E96|Não é possível executar a operação. O provedor não pode obter espaço de armazenamento suficiente.|  
|**adErrPermissionDenied**|3720-2146824568 0x800A0E88|Permissão insuficiente impede a gravação no campo.|  
|**adErrProviderFailed**|3000-2146825288 0x800A0BB8|O provedor não executou a operação solicitada.|  
|**adErrProviderNotFound**|3706-2146824582 0x800A0E7A|Provedor não encontrado. Ele pode não estar instalado corretamente.|  
|**adErrReadFile**|3003-2146825285 0x800A0BBB|Não foi possível ler o arquivo.|  
|**adErrResourceExists**|3731-2146824557 0x800A0E93|Não é possível executar a operação de cópia. O objeto nomeado pela URL de destino já existe. Especifique **adCopyOverwrite** para substituir o objeto.|  
|**adErrResourceLocked**|3730-2146824558 0x800A0E92|O objeto representado pela URL especificada está bloqueado por um ou mais processos. Aguarde até que o processo seja concluído e repita a operação.|  
|**adErrResourceOutOfScope**|3735-2146824553 0x800A0E97|A URL de origem ou de destino está fora do escopo do registro atual.|  
|**adErrSchemaViolation**|3722-2146824566 0x800A0E8A|O valor dos dados está em conflito com o tipo de dados ou as restrições do campo.|  
|**adErrSignMismatch**|3723-2146824565 0x800A0E8B|Falha na conversão porque o valor de dados estava assinado e o tipo de dados de campo usado pelo provedor não estava assinado.|  
|**adErrStillConnecting**|3713-2146824575 0x800A0E81|Não é possível executar a operação durante a conexão assíncrona.|  
|**adErrStillExecuting**|3711-2146824577 0x800A0E7F|A operação não pode ser executada durante a execução assíncrona.|  
|**adErrTreePermissionDenied**|3728-2146824560 0x800A0E90|As permissões são insuficientes para acessar árvore ou subárvore.|  
|**adErrUnavailable**|3736-2146824552 0x800A0E98|A operação não foi concluída e o status não está disponível. O campo pode estar indisponível ou a operação não foi tentada.|  
|**adErrUnsafeOperation**|3716-2146824572 0x800A0E84|As configurações de segurança neste computador impedem o acesso a uma fonte de dados em outro domínio.|  
|**adErrURLDoesNotExist**|3727-2146824561 0x800A0E8F|A URL de origem ou o pai da URL de destino não existe.|  
|**adErrURLNamedRowDoesNotExist**|3737-2146824551 0x800A0E99|O registro nomeado por esta URL não existe.|  
|**adErrVolumeNotFound**|3733-2146824555 0x800A0E95|O provedor não pode localizar o dispositivo de armazenamento indicado pela URL. Verifique se a URL foi digitada corretamente.|  
|**adErrWriteFile**|3004-2146825284 0x800A0BBC|Falha ao gravar no arquivo.|  
|**adWrnSecurityDialog**|3717-2146824571 0x800A0E85|Apenas para uso interno. Não use.|  
|**adWrnSecurityDialogHeader**|3718-2146824570 0x800A0E86|Apenas para uso interno. Não use.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
 Somente os seguintes subconjuntos de equivalentes ADO/WFC são definidos.  
  
|Constante|  
|--------------|  
|AdoEnums. Errorvalue. BOUNDTOCOMMAND|  
|AdoEnums. Errorvalue. dataconversion|  
|AdoEnums. Errorvalue. FEATURENOTAVAILABLE|  
|AdoEnums. Errorvalue. ILLEGALOPERATION|  
|AdoEnums. Errorvalue. retransaction|  
|AdoEnums. Errorvalue. INVALIDARGUMENT|  
|AdoEnums. Errorvalue. INVALIDCONNECTION|  
|AdoEnums. Errorvalue. INVALIDPARAMINFO|  
|AdoEnums. Errorvalue. ITEMNOTFOUND|  
|AdoEnums. Errorvalue. NOCURRENTRECORD|  
|AdoEnums. Errorvalue. não está em execução|  
|AdoEnums. Errorvalue. NOTREENTRANT|  
|AdoEnums. Errorvalue. objectcloseed|  
|AdoEnums. Errorvalue. OBJECTINCOLLECTION|  
|AdoEnums. Errorvalue. objectnotset|  
|AdoEnums. Errorvalue. objectopen|  
|AdoEnums. Errorvalue. OPERATIONCANCELLED|  
|AdoEnums. Errorvalue. PROVIDERNOTFOUND|  
|AdoEnums. Errorvalue. STILLCONNECTING|  
|AdoEnums. Errorvalue. STILLEXECUTING|  
|AdoEnums. Errorvalue. UNSAFEOPERATION|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Códigos de erro ADO](../../../ado/guide/appendixes/ado-error-codes.md)
