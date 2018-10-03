---
title: Método LoadFromFile (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_LoadFromFile
helpviewer_keywords:
- LoadFromFile method [ADO]
ms.assetid: b18d8d38-7354-4a94-b637-6ac035faa433
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed02b621b79ebf46dbb0dc6e66a2e5366610a19d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761234"
---
# <a name="loadfromfile-method-ado"></a>Método LoadFromFile (ADO)
Carrega o conteúdo de um arquivo existente em uma [Stream](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *FileName*  
 Um **cadeia de caracteres** que contém o nome de um arquivo a ser carregado no valor de **Stream**. *Nome de arquivo* pode conter qualquer caminho válido e o nome no formato UNC. Se o arquivo especificado não existir, ocorrerá um erro de tempo de execução.  
  
## <a name="remarks"></a>Comentários  
 Esse método pode ser usado para carregar o conteúdo de um arquivo local em um **Stream** objeto. Isso pode ser usado para carregar o conteúdo de um arquivo local em um servidor.  
  
 O **Stream** objeto já deve estar aberto antes de chamar **LoadFromFile**. Esse método não altera a associação de uma a **Stream** do objeto; ainda será associado ao objeto especificado pela URL ou **registro** com a qual o **Stream** foi originalmente aberto.  
  
 **LoadFromFile** substitui o conteúdo atual dos **Stream** objeto com os dados lidos do arquivo. Quaisquer bytes existentes na **Stream** são substituídos pelos conteúdos do arquivo. Quaisquer bytes restantes e anteriormente existentes seguindo as [EOS](../../../ado/reference/ado-api/eos-property.md) criados pelo **LoadFromFile**, são truncados.  
  
 Após uma chamada para **LoadFromFile**, a posição atual está definida para o início da **Stream** ([posição](../../../ado/reference/ado-api/position-property-ado.md) é 0).  
  
 Como 2 bytes podem ser adicionados para o início do fluxo para a codificação, é possível que o tamanho do fluxo não exatamente corresponder o tamanho do arquivo do qual ele foi carregado.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
