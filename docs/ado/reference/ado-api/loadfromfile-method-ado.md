---
description: Método LoadFromFile (ADO)
title: Método LoadFromFile (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 76c00998c8fd7c3c6f737ab9b2ab0e2e35c74101
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990697"
---
# <a name="loadfromfile-method-ado"></a>Método LoadFromFile (ADO)
Carrega o conteúdo de um arquivo existente em um [fluxo](./stream-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *FileName*  
 Um valor de **cadeia de caracteres** que contém o nome de um arquivo a ser carregado no **fluxo**. O *nome de arquivo* pode conter qualquer caminho e nome válidos no formato UNC. Se o arquivo especificado não existir, ocorrerá um erro em tempo de execução.  
  
## <a name="remarks"></a>Comentários  
 Esse método pode ser usado para carregar o conteúdo de um arquivo local em um objeto de **fluxo** . Isso pode ser usado para carregar o conteúdo de um arquivo local em um servidor.  
  
 O objeto de **fluxo** já deve estar aberto antes de chamar **loaddofile**. Esse método não altera a associação do objeto de **fluxo** ; Ele ainda será associado ao objeto especificado pela URL ou pelo **registro** com o qual o **fluxo** foi aberto originalmente.  
  
 **Loaddofile** substitui o conteúdo atual do objeto de **fluxo** por dados lidos do arquivo. Todos os bytes existentes no **fluxo** são substituídos pelo conteúdo do arquivo. Todos os bytes anteriores e restantes existentes após o [EOS](./eos-property.md) criado por **LoadFromFile**serão truncados.  
  
 Após uma chamada para **LoadFromFile**, a posição atual é definida como o início do **fluxo** (a[posição](./position-property-ado.md) é 0).  
  
 Como 2 bytes podem ser adicionados ao início do fluxo para codificação, o tamanho do fluxo pode não corresponder exatamente ao tamanho do arquivo do qual ele foi carregado.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](./stream-object-ado.md)