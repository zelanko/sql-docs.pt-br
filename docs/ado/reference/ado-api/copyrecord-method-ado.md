---
title: Método CopyRecord (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_CopyRecord
- _Record::CopyRecord
helpviewer_keywords:
- CopyRecord method [ADO]
ms.assetid: b9bcf272-3c74-479f-95dd-0229a32e98fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 5fc8cfec5752f88909214301931c69dddfe89dc5
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758792"
---
# <a name="copyrecord-method-ado"></a>Método CopyRecord (ADO)
Copia uma entidade representada por um [registro](../../../ado/reference/ado-api/record-object-ado.md) para outro local.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Fonte*  
 Opcional. Um valor de **cadeia de caracteres** que contém uma URL que especifica a entidade a ser copiada (por exemplo, um arquivo ou diretório). Se a *origem* for omitida ou especificar uma cadeia de caracteres vazia, o arquivo ou diretório representado pelo [registro](../../../ado/reference/ado-api/record-object-ado.md) atual será copiado.  
  
 *Destino*  
 Opcional. Um valor de **cadeia de caracteres** que contém uma URL especificando o local onde a *fonte* será copiada.  
  
 *Usu*  
 Opcional. Um valor de **cadeia de caracteres** que contém a ID de usuário que, se necessário, autoriza o acesso ao *destino*.  
  
 *Senha*  
 Opcional. Um valor de **cadeia de caracteres** que contém a senha que, se necessário, verifica o *nome de usuário*.  
  
 *Opções*  
 Opcional. Um valor de [CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md) que tem um valor padrão de **adCopyUnspecified**. Especifica o comportamento desse método.  
  
 *Async*  
 Opcional. Um valor **booliano** que, quando **true**, especifica que essa operação deve ser assíncrona.  
  
## <a name="return-value"></a>Valor Retornado  
 Um valor de **cadeia de caracteres** que normalmente retorna o valor de *destino*. No entanto, o valor exato retornado é dependente do provedor.  
  
## <a name="remarks"></a>Comentários  
 Os valores de *origem* e *destino* não devem ser idênticos; caso contrário, ocorrerá um erro em tempo de execução. Pelo menos um dos nomes de servidor, caminho ou recurso deve ser diferente.  
  
 Todos os filhos (por exemplo, subdiretórios) da *origem* são copiados recursivamente, a menos que **adCopyNonRecursive** seja especificado. Em uma operação recursiva, o *destino* não deve ser um subdiretório da *origem*; caso contrário, a operação não será concluída.  
  
 Esse método falhará se o *destino* identificar uma entidade existente (por exemplo, um arquivo ou diretório), a menos que **adCopyOverWrite** seja especificado.  
  
> [!IMPORTANT]
>  Use a opção **adCopyOverWrite** criteriosamente. Por exemplo, especificar essa opção ao copiar um arquivo para um diretório *excluirá* o diretório e o substituirá pelo arquivo.  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
