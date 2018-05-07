---
title: Método CopyRecord (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_CopyRecord
- _Record::CopyRecord
helpviewer_keywords:
- CopyRecord method [ADO]
ms.assetid: b9bcf272-3c74-479f-95dd-0229a32e98fc
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1af576e7aab76c6e505b2346a74924d8b2ec843e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="copyrecord-method-ado"></a>Método CopyRecord (ADO)
Copia uma entidade representada por um [registro](../../../ado/reference/ado-api/record-object-ado.md) para outro local.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Opcional. Um **cadeia de caracteres** valor que contém uma URL especificando a entidade a ser copiado (por exemplo, um arquivo ou diretório). Se *fonte* for omitido ou especifica uma cadeia de caracteres vazia, o arquivo ou diretório representado pelo atual [registro](../../../ado/reference/ado-api/record-object-ado.md) serão copiados.  
  
 *Destino*  
 Opcional. Um **cadeia de caracteres** valor que contém uma URL que especifica o local onde *fonte* serão copiados.  
  
 *UserName*  
 Opcional. Um **cadeia de caracteres** valor que contém a ID de usuário que, se necessário, conceda acesso ao *destino*.  
  
 *Senha*  
 Opcional. Um **cadeia de caracteres** valor que contém a senha, se necessário, verifica *nome de usuário*.  
  
 *Opções*  
 Opcional. Um [CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md) valor que tem um valor padrão de **adCopyUnspecified**. Especifica o comportamento desse método.  
  
 *Async*  
 Opcional. Um **booliano** valor que, quando **True**, especifica que esta operação deve ser assíncrona.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** valor que geralmente retorna o valor de *destino*. No entanto, o valor exato retornado depende do provedor.  
  
## <a name="remarks"></a>Remarks  
 Os valores de *fonte* e *destino* não deve ser idêntico; caso contrário, ocorre um erro de tempo de execução. Pelo menos um dos nomes de servidor, caminho ou recurso deve ser diferente.  
  
 Todos os filhos (por exemplo, subdiretórios) de *fonte* são copiado repetidamente, a menos que **adCopyNonRecursive** for especificado. Em uma operação recursiva, *destino* não deve ser um subdiretório do *fonte*; caso contrário, a operação não será concluída.  
  
 Esse método falhar se *destino* identifica uma entidade existente (por exemplo, um arquivo ou diretório), a menos que **adCopyOverWrite** for especificado.  
  
> [!IMPORTANT]
>  Use o **adCopyOverWrite** opção criteriosamente. Por exemplo, especificar essa opção quando copiar um arquivo em um diretório será *excluir* o diretório e substituí-lo com o arquivo.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
