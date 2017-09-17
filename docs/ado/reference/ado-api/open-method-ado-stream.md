---
title: "Abra o método (fluxo de ADO) | Microsoft Docs"
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
- _Stream::raw_Open
- _Stream::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: d26f48fb-904e-4932-a245-3b4332ca1600
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dba50c39ff8c31154e52f8575a93acdf829df442
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="open-method-ado-stream"></a>Método Open (fluxo de ADO)
Abre uma [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto para manipular fluxos de dados binários ou de texto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Opcional. Um **Variant** valor que especifica a fonte de dados para o **fluxo**. *Origem* pode conter uma cadeia de caracteres de URL absoluta que aponte para um nó existente em uma estrutura de árvore conhecidas, como um sistema de email ou arquivo. Uma URL deve ser especificada usando a palavra-chave de URL ("URL =*esquema*://*servidor*/*pasta*"). Como alternativa, *fonte* pode conter uma referência a uma já aberto [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto, que abre o fluxo padrão associado a **registro**. Se *fonte* não for especificado, um **fluxo** é instanciada e aberta, associado a nenhuma fonte subjacente por padrão. Para obter mais informações sobre esquemas de URL e os provedores associados, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 *Modo*  
 Opcional. Um [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) valor que especifica o modo de acesso para os resultantes **fluxo** (por exemplo, leitura/gravação ou somente leitura). Valor padrão é **adModeUnknown**. Consulte o [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedade para obter mais informações sobre modos de acesso. Se *modo* não for especificado, ele é herdado por objeto de origem. Por exemplo, se a fonte **registro** é aberto no modo somente leitura, o **fluxo** também será aberto no modo somente leitura por padrão.  
  
 *OpenOptions*  
 Opcional. Um [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md) valor. Valor padrão é **adOpenStreamUnspecified**.  
  
 *UserName*  
 Opcional. Um **cadeia de caracteres** valor que contém a identificação do usuário que, se necessário, acessa o **fluxo** objeto.  
  
 *Senha*  
 Opcional. Um **cadeia de caracteres** valor que contém a senha, se necessário, acessa o **fluxo** objeto.  
  
## <a name="remarks"></a>Comentários  
 Quando um **registro** objeto é passado como o parâmetro de origem, o *UserID* e *senha* parâmetros não são usados como acesso a **registro** o objeto já está disponível. Da mesma forma, o [modo](../../../ado/reference/ado-api/mode-property-ado.md) do **registro** objeto é transferido para o **fluxo** objeto. Quando *fonte* não for especificado, o **fluxo** aberto não contém dados e tem um [tamanho](../../../ado/reference/ado-api/size-property-ado-stream.md) de zero (0). Para evitar a perda dos dados gravados isso **fluxo** quando o **fluxo** é fechado, salvar o **fluxo** com o [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) ou [ SaveToFile](../../../ado/reference/ado-api/savetofile-method.md) métodos, ou salvá-lo para outro local de memória.  
  
 Um *OpenOptions* valor **adOpenStreamFromRecord** identifica o conteúdo do *fonte* parâmetro seja já aberto **registro**objeto. O comportamento padrão é tratar *fonte* como uma URL que aponta diretamente para um nó em uma estrutura de árvore, como um arquivo. Fluxo padrão associado a esse nó é aberto.  
  
 Enquanto o **fluxo** é não está aberta, é possível ler todas as propriedades somente leitura do **fluxo**. Se um **fluxo** é aberto de forma assíncrona, todas as operações subsequentes (diferente de verificação de [estado](../../../ado/reference/ado-api/state-property-ado.md) e outras propriedades somente leitura) são bloqueadas até que o **abrir** concluir a operação.  
  
 Além das opções que foram abordadas anteriormente, não especificando *fonte*, você pode criar uma instância de um **fluxo** objeto na memória sem associá-la a uma fonte subjacente. Dinamicamente você pode adicionar dados ao fluxo de gravação de dados binários ou de texto para o **fluxo** com [gravar](../../../ado/reference/ado-api/write-method.md) ou [WriteText](../../../ado/reference/ado-api/writetext-method.md), ou ao carregar dados de um arquivo com [ LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Open (Conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (ADO registro)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)   
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)
