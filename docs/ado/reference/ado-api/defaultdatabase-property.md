---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2cd93826e03f7767455ec4b656ed14d1c35c21d2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47757445"
---
# <a name="defaultdatabase-property"></a>Propriedade DefaultDatabase
Indica o banco de dados padrão para um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor que é avaliada como o nome de um banco de dados disponível do provedor.  
  
## <a name="remarks"></a>Comentários  
 Use o **DefaultDatabase** propriedade para definir ou retornar o nome do banco de dados padrão em uma determinada **Conexão** objeto.  
  
 Se houver um banco de dados padrão, cadeias de caracteres SQL podem usar uma sintaxe não qualificada para acessar objetos no banco de dados. Para acessar objetos em um banco de dados diferente daquele especificado em que o **DefaultDatabase** propriedade, você deve qualificar nomes de objeto com o nome do banco de dados desejado. Após a conexão, o provedor irá escrever informações de banco de dados padrão para o **DefaultDatabase** propriedade. Alguns provedores permitem que apenas um banco de dados por conexão, caso em que você não pode alterar o **DefaultDatabase** propriedade.  
  
 Algumas fontes de dados e provedores podem não dar suporte a esse recurso e podem retornar um erro ou uma cadeia de caracteres vazia.  
  
> [!NOTE]
>  **Uso do serviço de dados remotos** essa propriedade não está disponível em um lado do cliente **Conexão** objeto.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Provedor e o exemplo de propriedades de DefaultDatabase (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Exemplo das propriedades Provider e DefaultDatabase (VC++)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vc.md)   
