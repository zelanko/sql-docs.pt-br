---
title: Método (ADO Stream) Open | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Open
- _Stream::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: d26f48fb-904e-4932-a245-3b4332ca1600
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c1d1863b28367ba825541c6e334613f65d3bc657
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707087"
---
# <a name="open-method-ado-stream"></a>Método Open (Fluxo do ADO)
Abre um [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto para manipular fluxos de dados de texto ou binárias.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Opcional. Um **Variant** valor que especifica a fonte de dados para o **Stream**. *Origem* pode conter uma cadeia de caracteres de URL absoluta que aponta para um nó existente em uma estrutura de árvore bem conhecidos, como um sistema de email ou arquivo. Uma URL deve ser especificada usando a palavra-chave de URL ("URL =*esquema de*://*server*/*pasta*"). Como alternativa, *fonte* pode conter uma referência a uma já aberta [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto, que abre o fluxo padrão associado a **registro**. Se *fonte* não for especificado, um **Stream** é instanciada e aberta, associado a nenhuma fonte subjacente por padrão. Para obter mais informações sobre esquemas de URL e os provedores associados, consulte [absoluta e relativa URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 *Modo*  
 Opcional. Um [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) valor que especifica o modo de acesso para o resultante **Stream** (por exemplo, leitura/gravação ou somente leitura). Valor padrão é **adModeUnknown**. Consulte a [modo](../../../ado/reference/ado-api/mode-property-ado.md) propriedade para obter mais informações sobre modos de acesso. Se *modo* não for especificado, ela é herdada pelo objeto de fonte. Por exemplo, se o código-fonte **registro** é aberto no modo somente leitura, o **Stream** também será aberto no modo somente leitura por padrão.  
  
 *OpenOptions*  
 Opcional. Um [StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md) valor. Valor padrão é **adOpenStreamUnspecified**.  
  
 *UserName*  
 Opcional. Um **cadeia de caracteres** valor que contém a identificação do usuário que, se ela for necessária, acessa o **Stream** objeto.  
  
 *Senha*  
 Opcional. Um **cadeia de caracteres** valor que contém a senha que, se ela for necessária, acessa o **Stream** objeto.  
  
## <a name="remarks"></a>Comentários  
 Quando um **registro** objeto é passado como o parâmetro de origem, o *UserID* e *senha* parâmetros não forem usados, porque o acesso ao **registro** objeto já está disponível. Da mesma forma, o [modo](../../../ado/reference/ado-api/mode-property-ado.md) da **registro** objeto é transferido para o **Stream** objeto. Quando *fonte* não for especificado, o **Stream** aberto não contém dados e tem um [tamanho](../../../ado/reference/ado-api/size-property-ado-stream.md) de zero (0). Para evitar a perda dos dados que são gravados a este **Stream** quando o **Stream** é fechado, salve o **Stream** com o [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) ou [ SaveToFile](../../../ado/reference/ado-api/savetofile-method.md) métodos, ou salvá-lo em outro local da memória.  
  
 Uma *OpenOptions* valor de **adOpenStreamFromRecord** identifica o conteúdo do *origem* parâmetro já aberto **registro**objeto. O comportamento padrão é tratar *origem* como uma URL que aponte diretamente para um nó em uma estrutura de árvore, como um arquivo. O fluxo padrão associado a esse nó é aberto.  
  
 Enquanto o **Stream** é não está aberta, é possível ler todas as propriedades somente leitura do **Stream**. Se um **Stream** é aberto de forma assíncrona, todas as operações subsequentes (diferente de verificação a [estado](../../../ado/reference/ado-api/state-property-ado.md) e outras propriedades somente leitura) são bloqueados até que o **abrir** operação é concluída.  
  
 Além das opções que foram abordadas anteriormente, não especificando *fonte*, você pode criar uma instância de um **Stream** objeto na memória sem associá-la a uma fonte subjacente. Você pode adicionar dinamicamente dados no fluxo gravando os dados binários ou de texto para o **Stream** com [escrever](../../../ado/reference/ado-api/write-method.md) ou [WriteText](../../../ado/reference/ado-api/writetext-method.md), ou pelo carregamento de dados de um arquivo com [ LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Open (Conexão ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Método Open (registro ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Exemplo do método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)   
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)
