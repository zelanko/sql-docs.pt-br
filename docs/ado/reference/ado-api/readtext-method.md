---
title: Método ReadText | Microsoft Docs
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
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26221c32339aab70311a6ca9254bb5d514724070
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="readtext-method"></a>Método ReadText
Leituras de número especificado de caracteres de um texto [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *NumChars*  
 Opcional. Um **longo** valor que especifica o número de caracteres a serem lidos do arquivo, ou um [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) valor. O valor padrão é **adReadAll**.  
  
## <a name="return-value"></a>Valor de retorno  
 O **ReadText** método lê um número especificado de caracteres, uma linha inteira ou o fluxo inteiro de um **fluxo** de objeto e retorna a cadeia de caracteres resultante.  
  
## <a name="remarks"></a>Remarks  
 Se *NumChar* mais do que o número de caracteres for deixado no fluxo, somente os caracteres restantes são retornados. A cadeia de caracteres de leitura não está preenchida para corresponder ao comprimento especificado por *NumChar*. Se não houver nenhum caractere à esquerda para ler, uma variante cujo valor é null é retornada. **ReadText** não pode ser usado para ler com versões anteriores.  
  
> [!NOTE]
>  O **ReadText** método é usado com fluxos de texto ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) é **adTypeText**). Para fluxos binários (**tipo** é **adTypeBinary**), use [leitura](../../../ado/reference/ado-api/read-method.md).  
  
 Consultas que resultaram em uma grande quantidade de dados XML que estão sendo retornados por meio de **ReadText** método do objeto de fluxo do ActiveX Data Object (ADO) pode levar muito tempo para ser executada; se isso for feito em um componente COM+ que é chamado de um Página ASP, a sessão do usuário atinjam o tempo limite. ADO converte dados de objeto de fluxo de codificação UTF-8 para Unicode. a realocação de memória frequente envolvida na conversão de uma grande quantidade de dados de uma vez é muito demorada. Para resolver, fazer chamadas repetidas para o **ReadText** método do ADO objeto de comando e especifique um número menor de caracteres. Testes mostraram que um valor equivalente a 128K (131,072) é ideal. Tempo de resposta diminui à medida que esse valor é diminuído. Para obter mais informações, consulte o artigo da Base de dados de Conhecimento 280067, "PRB: recuperar documentos XML muito grandes do SQL Server 2000 usando o método ReadText do objeto de fluxo ADO pode ser lento", na Base de dados de Conhecimento Microsoft em http://support.microsoft.com.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Read](../../../ado/reference/ado-api/read-method.md)
