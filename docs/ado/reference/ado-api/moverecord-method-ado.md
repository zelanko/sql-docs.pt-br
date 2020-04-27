---
title: Método MoveRecord (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::MoveRecord
- _Record::raw_MoveRecord
helpviewer_keywords:
- MoveRecord method [ADO]
ms.assetid: 6d2807b0-b861-4583-bcaf-fb0b82e0f2d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 157e38c2c9c23ff8f7e92af40385b0962c6dcb70
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918071"
---
# <a name="moverecord-method-ado"></a>Método MoveRecord (ADO)
Move a entidade representada por um [registro](../../../ado/reference/ado-api/record-object-ado.md) para outro local.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Fonte*  
 Opcional. Um valor de **cadeia de caracteres** que contém uma URL que identifica o **registro** a ser movido. Se a *origem* for omitida ou especificar uma cadeia de caracteres vazia, o objeto representado por esse **registro** será movido. Por exemplo, se o **registro** representar um arquivo, o conteúdo do arquivo será movido para o local especificado pelo *destino*.  
  
 *Destino*  
 Opcional. Um valor de **cadeia de caracteres** que contém uma URL especificando o local onde a *fonte* será movida.  
  
 *Usu*  
 Opcional. Um valor de **cadeia de caracteres** que contém a ID de usuário que, se necessário, autoriza o acesso ao *destino*.  
  
 *Senha*  
 Opcional. Uma **cadeia de caracteres** que contém a senha que, se necessário, verifica o *nome de usuário*.  
  
 *Opções*  
 Opcional. Um valor de [MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md) cujo valor padrão é **adMoveUnspecified**. Especifica o comportamento desse método.  
  
 *Async*  
 Opcional. Um valor **booliano** que, quando **true**, especifica que essa operação deve ser assíncrona.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor de **cadeia de caracteres** . Normalmente, o valor de *destino* é retornado. No entanto, o valor exato retornado é dependente do provedor.  
  
## <a name="remarks"></a>Comentários  
 Os valores de *origem* e *destino* não devem ser idênticos; caso contrário, ocorrerá um erro em tempo de execução. Pelo menos os nomes de servidor, caminho e recurso devem ser diferentes.  
  
 Para arquivos movidos usando o provedor de publicação da Internet, esse método atualiza todos os links de hipertexto em arquivos que estão sendo movidos, a menos que especificado em contrário por *Opções*. Esse método falhará se o *destino* identificar um objeto existente (por exemplo, um arquivo ou diretório), a menos que **adMoveOverWrite** seja especificado.  
  
> [!NOTE]
>  Use a opção **adMoveOverWrite** criteriosamente. Por exemplo, especificar essa opção ao mover um arquivo para um diretório excluirá o diretório e o substituirá pelo arquivo.  
  
 Determinados atributos do objeto de **registro** , como a propriedade [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) , não serão atualizados após a conclusão dessa operação. Atualize as propriedades do objeto de **registro** fechando o **registro**e, em seguida, reabri-lo com a URL do local em que o arquivo ou diretório foi movido.  
  
 Se esse **registro** foi obtido de um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md), o novo local do arquivo ou diretório movido não será refletido imediatamente no **conjunto de registros**. Atualize o **conjunto de registros** fechando-o e reabrindo-o.  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Métodos MoveFirst, MoveLast, MoveNext e MovePrevious (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)
