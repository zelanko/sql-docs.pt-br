---
title: "Método MoveRecord (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Record::MoveRecord
- _Record::raw_MoveRecord
helpviewer_keywords:
- MoveRecord method [ADO]
ms.assetid: 6d2807b0-b861-4583-bcaf-fb0b82e0f2d0
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f385fc1fd6c7374a9d693d8fcb898f817c54bbc7
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="moverecord-method-ado"></a>Método MoveRecord (ADO)
Move a entidade representada por um [registro](../../../ado/reference/ado-api/record-object-ado.md) para outro local.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Opcional. Um **cadeia de caracteres** valor que contém um URL que identifica o **registro** a ser movido. Se *fonte* for omitido ou especifica uma cadeia de caracteres vazia, o objeto representado por esse **registro** é movido. Por exemplo, se o **registro** representa um arquivo, o conteúdo do arquivo é movidas para o local especificado por *destino*.  
  
 *Destino*  
 Opcional. Um **cadeia de caracteres** valor que contém uma URL que especifica o local onde *fonte* será movido.  
  
 *UserName*  
 Opcional. Um **cadeia de caracteres** valor que contém a ID de usuário que, se necessário, conceda acesso ao *destino*.  
  
 *Senha*  
 Opcional. Um **cadeia de caracteres** que contém a senha, se necessário, verifica *nome de usuário*.  
  
 *Opções*  
 Opcional. Um [MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md) valor cujo valor padrão é **adMoveUnspecified**. Especifica o comportamento desse método.  
  
 *Assíncrono*  
 Opcional. Um **booliano** valor que, quando **True**, especifica que esta operação deve ser assíncrona.  
  
## <a name="return-value"></a>Valor de retorno  
 Um **cadeia de caracteres** valor. Normalmente, o valor de *destino* é retornado. No entanto, o valor exato retornado depende do provedor.  
  
## <a name="remarks"></a>Comentários  
 Os valores de *fonte* e *destino* não deve ser idêntico; caso contrário, ocorre um erro de tempo de execução. Pelo menos os nomes de servidor, o caminho e o recurso devem ser diferente.  
  
 Para arquivos movidos usando o provedor de publicação, este método atualizará todos os links de hipertexto em arquivos que está sendo movidos a menos que especificado de outra forma por *opções*. Esse método falhar se *destino* identifica um objeto existente (por exemplo, um arquivo ou diretório), a menos que **adMoveOverWrite** for especificado.  
  
> [!NOTE]
>  Use o **adMoveOverWrite** opção criteriosamente. Por exemplo, especificar essa opção, ao mover um arquivo para um diretório excluirá o diretório e substituí-lo com o arquivo.  
  
 Determinados atributos do **registro** objeto, como o [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) propriedade, não será atualizada depois que a operação for concluída. Atualizar o **registro** propriedades do objeto fechando o **registro**, em seguida, abra-o novamente com a URL do local onde o arquivo ou diretório foi movido.  
  
 Se este **registro** foi obtido um [registros](../../../ado/reference/ado-api/recordset-object-ado.md), o novo local do arquivo movido ou diretório não será refletido imediatamente no **registros**. Atualizar o **registros** fechando e abri-lo novamente.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext e MovePrevious métodos (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)

