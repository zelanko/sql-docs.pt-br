---
description: Método Open (Fluxo do ADO)
title: Método Open (fluxo ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 333d20ee58123e9f1120e22d1770bd2a74ad97ae
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773775"
---
# <a name="open-method-ado-stream"></a>Método Open (Fluxo do ADO)
Abre um objeto de [fluxo](./stream-object-ado.md) para manipular fluxos de dados binários ou de texto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.Open Source, Mode , OpenOptions, UserName, Password  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Origem*  
 Opcional. Um valor de **variante** que especifica a fonte de dados para o **fluxo**. A *origem* pode conter uma cadeia de caracteres de URL absoluta que aponta para um nó existente em uma estrutura de árvore conhecida, como um email ou sistema de arquivos. Uma URL deve ser especificada usando a palavra-chave URL ("URL =*esquema*://pasta*do servidor* / *folder*"). Como alternativa, a *origem* pode conter uma referência a um objeto de [registro](./record-object-ado.md) já aberto, que abre o fluxo padrão associado ao **registro**. Se a *origem* não for especificada, um **fluxo** será instanciado e aberto, associado a nenhuma fonte subjacente por padrão. Para obter mais informações sobre esquemas de URL e seus provedores associados, consulte [URLs absolutas e relativas](../../guide/data/absolute-and-relative-urls.md).  
  
 *Modo*  
 Opcional. Um valor de [ConnectModeEnum](./connectmodeenum.md) que especifica o modo de acesso para o **fluxo** resultante (por exemplo, leitura/gravação ou somente leitura). O valor padrão é **adModeUnknown**. Consulte a propriedade [Mode](./mode-property-ado.md) para obter mais informações sobre modos de acesso. Se o *modo* não for especificado, ele será herdado pelo objeto de origem. Por exemplo, se o **registro** de origem for aberto no modo somente leitura, o **fluxo** também será aberto no modo somente leitura por padrão.  
  
 *OpenOptions*  
 Opcional. Um valor de [StreamOpenOptionsEnum](./streamopenoptionsenum.md) . O valor padrão é **adOpenStreamUnspecified**.  
  
 *UserName*  
 Opcional. Um valor de **cadeia de caracteres** que contém a identificação de usuário que, se necessário, acessa o objeto de **fluxo** .  
  
 *Senha*  
 Opcional. Um valor de **cadeia de caracteres** que contém a senha que, se necessário, acessa o objeto de **fluxo** .  
  
## <a name="remarks"></a>Comentários  
 Quando um objeto de **registro** é passado como o parâmetro de origem, os parâmetros *userid* e *password* não são usados porque o acesso ao objeto de **registro** já está disponível. Da mesma forma, o [modo](./mode-property-ado.md) do objeto de **registro** é transferido para o objeto **Stream** . Quando a *origem* não é especificada, o **fluxo** aberto não contém dados e tem um [tamanho](./size-property-ado-stream.md) de zero (0). Para evitar a perda de todos os dados que são gravados nesse **fluxo** quando o **fluxo** é fechado, salve o **fluxo** com os métodos [CopyTo](./copyto-method-ado.md) ou [SaveToFile](./savetofile-method.md) ou salve-o em outro local da memória.  
  
 Um valor *openoptions* de **adOpenStreamFromRecord** identifica o conteúdo do parâmetro de *origem* como um objeto de **registro** já aberto. O comportamento padrão é tratar a *origem* como uma URL que aponta diretamente para um nó em uma estrutura de árvore, como um arquivo. O fluxo padrão associado a esse nó é aberto.  
  
 Embora o **fluxo** não esteja aberto, é possível ler todas as propriedades somente leitura do **fluxo**. Se um **fluxo** for aberto de forma assíncrona, todas as operações subsequentes (além de verificar o [estado](./state-property-ado.md) e outras propriedades somente leitura) serão bloqueadas até que a operação de **abertura** seja concluída.  
  
 Além das opções que foram discutidas anteriormente, não especificando a *origem*, você pode criar uma instância de um objeto de **fluxo** na memória sem associá-la a uma fonte subjacente. Você pode adicionar dados dinamicamente ao fluxo, gravando dados binários ou de texto no **fluxo** com [Write](./write-method.md) ou [WriteText](./writetext-method.md)ou carregando dados de um arquivo com [LoadFromFile](./loadfromfile-method-ado.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método Open (conexão ADO)](./open-method-ado-connection.md)   
 [Método Open (registro ADO)](./open-method-ado-record.md)   
 [Método Open (conjunto de registros ADO)](./open-method-ado-recordset.md)   
 [Método OpenSchema](./openschema-method.md)   
 [Método SaveToFile](./savetofile-method.md)