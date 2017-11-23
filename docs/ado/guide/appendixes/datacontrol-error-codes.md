---
title: "Códigos de erro de DataControl | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- errors [ADO], DataControl
- DataControl errors [ADO]
ms.assetid: 293df9d5-e1a2-406d-9107-07bf7cdc6f96
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 54dcd3721781ccb2889d88c2545d8bb3630cb7bc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="datacontrol-object-error-codes"></a>Códigos de erro do objeto DataControl
A seguinte tabela lista o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) códigos de erro do objeto. A conversão decimal positiva de dois bytes de baixa, a conversão decimal negativa do código de erro completa e os valores hexadecimais são mostrados.

|RDS. Códigos de erro DataControl|Número|Description|
|---------------------------------|------------|-----------------|
|**IDS_AsyncPending**|4107-2146824175 0x800A1011|Operação não pode ser executada enquanto a operação assíncrona está pendente.|
|**IDS_BadInlineTablegram**|4105-2146824183 0x800A1009|Tablegram embutido incorreta.|
|**IDS_CantConnect**|4099-2146824189 0x800A1003|Não é possível se conectar ao servidor.|
|**IDS_CantCreateObject**|4100-2146824188 0x800A1004|Não é possível criar o objeto comercial.|
|**IDS_CantFindDataspace**|4102-2146824186 0x800A1006|A propriedade Dataspace não é válida.|
|**IDS_CantInvokeMethod**|4101-2146824187 0x800A1005|Método não pode ser chamado no objeto comercial.|
|**IDS_CrossDomainWarning**|4112-2146824170 0x800A1016|Esta página acessa dados em outro domínio. Você deseja permitir isso? Para evitar esta mensagem no Internet Explorer, você pode adicionar um site seguro à zona Sites confiáveis no **segurança** guia o **opções da Internet** caixa de diálogo.|
|**IDS_InvalidADCClientVersion**|4106-2146824176 0x800A1010|Versão de cliente RDS inválida, O cliente é mais recente do que o servidor.|
|**IDS_INVALIDARG**|5376-2147019520 0x80071500|Um ou mais argumentos são inválidos.|
|**IDS_InvalidBindings**|4097-2146824191 0x800A1001|Erro na propriedade de associações.|
|**IDS_InvalidParam**|4110-2146824172 0x800A1014|Um ou mais argumentos são inválidos.|
|**IDS_NOINTERFACE**|5377-2147019519 0x80071501|Essa interface não é suportado.|
|**IDS_NotReentrant**|4111-2146824171 0x800A1015|Solicitação não pode ser executada enquanto ainda está processando o manipulador de eventos.|
|**IDS_ObjectNotSafe**|4103-2146824185 0x800A1007|As configurações de segurança deste computador proíbem criação do objeto comercial.|
|**IDS_RecordsetNotOpen**|4109-2146824173 0x800A1013|**Conjunto de registros** não está aberto.|
|**IDS_ResetInvalidField**|4108-2146824174 0x800A1012|Coluna especificada em **SortColumn** ou **FilterColumn** não existe.|
|**IDS_RowsetNotUpdateable**|4104-2146824184 0x800A1008|Conjunto de linhas não atualizável.|
|**IDS_UnexpectedError**|4351-2146823937 0x800A10FF|Erro inesperado.|
|**IDS_UpdatesFailed**|4098-2146824190 0x800A1002|Não é possível atualizar o banco de dados.|
|**IDS_URLMONNotFound**|4119-2146824169 0x800A1017|DataControl **URL** propriedade requer que o arquivo de sistema Urlmon.dll, que não pode ser encontrado.|

## <a name="see-also"></a>Consulte também
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)
