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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aaabb32234cefe2e3c3727ce5a18dd2d98549a77
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933413"
---
# <a name="copyrecord-method-ado"></a>Método CopyRecord (ADO)
Copia uma entidade representada por uma [registro](../../../ado/reference/ado-api/record-object-ado.md) para outro local.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Source*  
 Opcional. Um **cadeia de caracteres** valor que contém uma URL especificando a entidade a ser copiado (por exemplo, um arquivo ou diretório). Se *fonte* for omitido ou especifica uma cadeia de caracteres vazia, o arquivo ou diretório representado pelo atual [registro](../../../ado/reference/ado-api/record-object-ado.md) serão copiados.  
  
 *Destino*  
 Opcional. Um **cadeia de caracteres** valor que contém uma URL especificando o local em que *origem* serão copiados.  
  
 *UserName*  
 Opcional. Um **cadeia de caracteres** valor que contém a ID de usuário que, se necessário, autoriza o acesso ao *destino*.  
  
 *Senha*  
 Opcional. Um **cadeia de caracteres** valor que contém a senha, se necessário, verifica *nome de usuário*.  
  
 *Opções*  
 Opcional. Um [CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md) valor que tem um valor padrão de **adCopyUnspecified**. Especifica o comportamento desse método.  
  
 *Async*  
 Opcional. Um **Boolean** valor que, quando **verdadeiro**, especifica que esta operação deve ser assíncrona.  
  
## <a name="return-value"></a>Valor retornado  
 Um **cadeia de caracteres** valor que normalmente retorna o valor de *destino*. No entanto, o valor exato retornado depende do provedor.  
  
## <a name="remarks"></a>Comentários  
 Os valores de *fonte* e *destino* não deve ser idêntico; caso contrário, ocorrerá um erro de tempo de execução. Pelo menos um dos nomes de servidor, o caminho ou o recurso deve ser diferente.  
  
 Todos os filhos (por exemplo, subdiretórios) do *fonte* serão copiado recursivamente, a menos que **adCopyNonRecursive** for especificado. Em uma operação de recursiva *destino* não deve ser um subdiretório do *origem*; caso contrário, a operação não será concluída.  
  
 Esse método falhar se *destino* identifica uma entidade existente (por exemplo, um arquivo ou diretório), a menos que **adCopyOverWrite** for especificado.  
  
> [!IMPORTANT]
>  Use o **adCopyOverWrite** opção criteriosamente. Por exemplo, especificar essa opção ao copiar um arquivo para um diretório serão *excluir* o diretório e substituí-lo com o arquivo.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [absoluta e relativa URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
