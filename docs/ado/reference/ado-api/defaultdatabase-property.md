---
description: Propriedade DefaultDatabase
title: Propriedade DefaultDatabase | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::DefaultDatabase
helpviewer_keywords:
- DefaultDatabase property
ms.assetid: 41e8a8dd-e69c-4a09-8736-93502e01961c
author: rothja
ms.author: jroth
ms.openlocfilehash: d7e16a5a5bc3a711477cca1507c889bd15e0f37a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444188"
---
# <a name="defaultdatabase-property"></a>Propriedade DefaultDatabase
Indica o banco de dados padrão para um objeto de [conexão](../../../ado/reference/ado-api/connection-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **cadeia de caracteres** que é avaliado como o nome de um banco de dados disponível do provedor.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **DefaultDatabase** para definir ou retornar o nome do banco de dados padrão em um objeto de **conexão** específico.  
  
 Se houver um banco de dados padrão, as cadeias de caracteres SQL poderão usar uma sintaxe não qualificada para acessar objetos nesse banco de dados. Para acessar objetos em um banco de dados diferente daquele especificado na propriedade **DefaultDatabase** , você deve qualificar nomes de objeto com o nome de banco de dados desejado. Após a conexão, o provedor gravará informações padrão do banco de dados na propriedade **DefaultDatabase** . Alguns provedores permitem apenas um banco de dados por conexão; nesse caso, não é possível alterar a propriedade **DefaultDatabase** .  
  
 Algumas fontes de dados e provedores podem não dar suporte a esse recurso e podem retornar um erro ou uma cadeia de caracteres vazia.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** Essa propriedade não está disponível em um objeto de **conexão** do lado do cliente.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades Provider e DefaultDatabase (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Exemplo das propriedades Provider e DefaultDatabase (VC++)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vc.md)   
