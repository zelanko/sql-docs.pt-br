---
title: "Método LoadFromFile (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::raw_LoadFromFile
helpviewer_keywords:
- LoadFromFile method [ADO]
ms.assetid: b18d8d38-7354-4a94-b637-6ac035faa433
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 071ba2d6a2aa5af96af07274455a7495a9650dea
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="loadfromfile-method-ado"></a>Método LoadFromFile (ADO)
Carrega o conteúdo de um arquivo existente em um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *FileName*  
 Um **cadeia de caracteres** valor que contém o nome de um arquivo a ser carregado para o **fluxo**. *Nome de arquivo* pode conter qualquer caminho válido e um nome no formato UNC. Se o arquivo especificado não existir, ocorrerá um erro de tempo de execução.  
  
## <a name="remarks"></a>Remarks  
 Esse método pode ser usado para carregar o conteúdo de um arquivo local em um **fluxo** objeto. Isso pode ser usado para carregar o conteúdo de um arquivo local para um servidor.  
  
 O **fluxo** objeto já deve estar aberto antes de chamar **LoadFromFile**. Este método não altera a associação do **fluxo** objeto; ainda será associado ao objeto especificado pela URL ou **registro** com a qual o **fluxo** originalmente aberto.  
  
 **LoadFromFile** substitui o conteúdo atual do **fluxo** objeto com a leitura do arquivo de dados. Qualquer bytes existentes no **fluxo** são substituídos pelo conteúdo do arquivo. Qualquer bytes restantes e anteriormente existentes após a [EOS](../../../ado/reference/ado-api/eos-property.md) criado por **LoadFromFile**, são truncados.  
  
 Após uma chamada para **LoadFromFile**, a posição atual está definida para o início do **fluxo** ([posição](../../../ado/reference/ado-api/position-property-ado.md) é 0).  
  
 Como 2 bytes podem ser adicionados para o início do fluxo de codificação, o tamanho do fluxo pode não corresponder exatamente ao tamanho do arquivo do qual ele foi carregado.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
