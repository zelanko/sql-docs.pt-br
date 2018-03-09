---
title: Propriedade DefaultDatabase | Microsoft Docs
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
- Connection15::DefaultDatabase
helpviewer_keywords:
- DefaultDatabase property
ms.assetid: 41e8a8dd-e69c-4a09-8736-93502e01961c
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c4220d8551d7aa9d1bd37f0770474214bc14209
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="defaultdatabase-property"></a>Propriedade DefaultDatabase
Indica o banco de dados padrão para um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor que é avaliada como o nome de um banco de dados disponível do provedor.  
  
## <a name="remarks"></a>Remarks  
 Use o **DefaultDatabase** propriedade para definir ou retornar o nome do banco de dados padrão em um determinado **Conexão** objeto.  
  
 Se houver um banco de dados padrão, cadeias de caracteres SQL podem usar uma sintaxe não qualificada para acessar objetos no banco de dados. Para acessar objetos em um banco de dados diferente daquele especificado no **DefaultDatabase** propriedade, você deve qualificar nomes de objeto com o nome do banco de dados desejado. Após a conexão, o provedor irá escrever informações de banco de dados padrão para o **DefaultDatabase** propriedade. Alguns provedores de permitir que apenas um banco de dados por conexão, caso em que você não pode alterar o **DefaultDatabase** propriedade.  
  
 Alguns provedores e as fontes de dados podem não oferecer suporte a esse recurso e podem retornar um erro ou uma cadeia de caracteres vazia.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** essa propriedade não está disponível em um cliente **Conexão** objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de DefaultDatabase (VB) e o provedor](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Exemplo das propriedades Provider e DefaultDatabase (VC++)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vc.md)   
