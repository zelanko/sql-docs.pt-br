---
title: Propriedade ConnectionTimeout (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionTimeout
helpviewer_keywords:
- ConnectionTimeout property [ADO]
ms.assetid: 8904a403-1383-4b4b-b53d-5c01d6f5deac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 03d3de2c4aabaf4ad8cbc45d9900b33883ff9a48
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933461"
---
# <a name="connectiontimeout-property-ado"></a>Propriedade ConnectionTimeout (ADO)
Indica por quanto tempo a esperar ao estabelecer uma conexão antes de encerrar a tentativa e gerar um erro.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **longo** valor que indica, em segundos, o tempo de espera para a conexão abrir. O padrão é 15.  
  
## <a name="remarks"></a>Comentários  
 Use o **ConnectionTimeout** propriedade em um [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) se os atrasos do uso de servidor de tráfego ou com uso intenso de rede Verifique necessário abandonar uma tentativa de conexão do objeto. Se o tempo desde o **ConnectionTimeout** decorre de configuração da propriedade antes da abertura da conexão, ocorrerá um erro e ADO cancela a tentativa. Se você definir a propriedade como zero, o ADO aguardará indefinidamente até que a conexão é aberta. Verifique se o provedor ao qual você está escrevendo código oferece suporte a **ConnectionTimeout** funcionalidade.  
  
 O **ConnectionTimeout** propriedade é leitura/gravação quando a conexão é fechada e somente leitura quando ele é aberto.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [ConnectionString, ConnectionTimeout e exemplo de propriedades de estado (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString, ConnectionTimeout e exemplo de propriedades de estado (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [Propriedade CommandTimeout (ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)
