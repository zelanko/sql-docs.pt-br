---
description: Método ReadText
title: Método ReadText | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
author: rothja
ms.author: jroth
ms.openlocfilehash: d2e55657dc0bf2e5cd508897196138e842e23b8e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989867"
---
# <a name="readtext-method"></a>Método ReadText
Lê o número especificado de caracteres de um objeto de [fluxo](./stream-object-ado.md) de texto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *NumChars*  
 Opcional. Um valor **longo** que especifica o número de caracteres a serem lidos do arquivo ou um valor de [StreamReadEnum](./streamreadenum.md) . O valor padrão é **adReadAll**.  
  
## <a name="return-value"></a>Valor de retorno  
 O método **READTEXT** lê um número especificado de caracteres, uma linha inteira ou todo o fluxo de um objeto de **fluxo** e retorna a cadeia de caracteres resultante.  
  
## <a name="remarks"></a>Comentários  
 Se *NumChar* for maior que o número de caracteres deixados no fluxo, somente os caracteres restantes serão retornados. A cadeia de caracteres lida não é preenchida para corresponder ao comprimento especificado por *NumChar*. Se não houver nenhum caractere restante para leitura, uma variante cujo valor é NULL será retornado. **READTEXT** não pode ser usado para ler para trás.  
  
> [!NOTE]
>  O método **READTEXT** é usado com fluxos de texto (o[tipo](./type-property-ado-stream.md) é **adTypeText**). Para fluxos binários (o**tipo** é **adTypeBinary**), use [ler](./read-method.md).  
  
 As consultas que resultam em uma grande quantidade de dados XML sendo retornados por meio do método **READTEXT** do objeto de fluxo ADO (ActiveX Data Object) podem levar muito tempo para serem executadas; Se isso for feito em um componente COM+ que é invocado de uma página ASP, a sessão do usuário poderá atingir o tempo limite. O ADO converte dados de objeto de fluxo de codificação UTF-8 para Unicode; a realocação de memória frequente envolvida na conversão de uma grande quantidade de dados ao mesmo tempo é muito demorada. Para resolver, faça chamadas repetidas para o método **READTEXT** do objeto de comando ADO e especifique um número menor de caracteres. Os testes mostraram que um valor equivalente a 128K (131.072) é ideal. O tempo de resposta diminui à medida que esse valor é reduzido. Para obter mais informações, consulte o artigo 280067 da base de dados de conhecimento, "problema: recuperar documentos XML muito grandes do SQL Server 2000 usando o método ReadText do objeto de fluxo ADO pode ser lento", na base de dados de conhecimento Microsoft em https://support.microsoft.com .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método Read](./read-method.md)