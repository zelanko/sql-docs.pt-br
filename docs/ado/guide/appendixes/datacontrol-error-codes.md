---
description: Códigos de erro do objeto DataControl
title: Códigos de erro de controle de Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], DataControl
- DataControl errors [ADO]
ms.assetid: 293df9d5-e1a2-406d-9107-07bf7cdc6f96
author: rothja
ms.author: jroth
ms.openlocfilehash: 3554898451228afee73914a82907f6348ad1cff0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991127"
---
# <a name="datacontrol-object-error-codes"></a>Códigos de erro do objeto DataControl
A tabela a seguir lista o [RDS. ](../../reference/rds-api/datacontrol-object-rds.md) Códigos de erro do objeto DataControl. A tradução decimal positiva dos dois bytes baixos, a conversão decimal negativa do código de erro completo e os valores hexadecimais são mostrados.

|Serviços. Códigos de erro de controle de|Número|Descrição|
|---------------------------------|------------|-----------------|
|**IDS_AsyncPending**|4107-2146824175 0x800A1011|Não é possível executar a operação enquanto a operação Async está pendente.|
|**IDS_BadInlineTablegram**|4105-2146824183 0x800A1009|Tablegram embutido inválido.|
|**IDS_CantConnect**|4099-2146824189 0x800A1003|Não é possível se conectar ao servidor.|
|**IDS_CantCreateObject**|4100-2146824188 0x800A1004|Não é possível criar o objeto comercial.|
|**IDS_CantFindDataspace**|4102-2146824186 0x800A1006|A Propriedade DataSpace não é válida.|
|**IDS_CantInvokeMethod**|4101-2146824187 0x800A1005|O método não pode ser invocado no objeto comercial.|
|**IDS_CrossDomainWarning**|4112-2146824170 0x800A1016|Esta página acessa dados em outro domínio. Deseja permitir isso? Para evitar essa mensagem no Internet Explorer, você pode adicionar um site da Web seguro à zona de sites confiáveis na guia **segurança** da caixa de diálogo **Opções da Internet** .|
|**IDS_InvalidADCClientVersion**|4106-2146824176 0x800A1010|Versão do cliente RDS inválida-o cliente é mais novo que o servidor.|
|**IDS_INVALIDARG**|5376-2147019520 0x80071500|Um ou mais argumentos são inválidos.|
|**IDS_InvalidBindings**|4097-2146824191 0x800A1001|Erro na propriedade bindings.|
|**IDS_InvalidParam**|4110-2146824172 0x800A1014|Um ou mais argumentos são inválidos.|
|**IDS_NOINTERFACE**|5377-2147019519 0x80071501|Não há suporte para essa interface.|
|**IDS_NotReentrant**|4111-2146824171 0x800A1015|A solicitação não pode ser executada enquanto o manipulador de eventos ainda está processando.|
|**IDS_ObjectNotSafe**|4103-2146824185 0x800A1007|As configurações de segurança neste computador proíbem a criação de objeto comercial.|
|**IDS_RecordsetNotOpen**|4109-2146824173 0x800A1013|O **conjunto de registros** não está aberto.|
|**IDS_ResetInvalidField**|4108-2146824174 0x800A1012|A coluna especificada em **SortColumn** ou **FilterColumn** não existe.|
|**IDS_RowsetNotUpdateable**|4104-2146824184 0x800A1008|Conjunto de linhas não atualizável.|
|**IDS_UnexpectedError**|4351-2146823937 0x800A10FF|Erro inesperado.|
|**IDS_UpdatesFailed**|4098-2146824190 0x800A1002|Não é possível atualizar o banco de dados.|
|**IDS_URLMONNotFound**|4119-2146824169 0x800A1017|A propriedade de **URL** do DataControl requer o arquivo do sistema Urlmon.dll, que não foi encontrado.|

## <a name="see-also"></a>Consulte Também
 [Objeto DataControl (RDS)](../../reference/rds-api/datacontrol-object-rds.md)