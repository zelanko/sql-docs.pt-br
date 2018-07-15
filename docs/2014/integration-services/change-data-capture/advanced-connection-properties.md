---
title: Propriedades da Conexão Avançadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4edfab68-7e68-45e8-a3f3-a0049ff7eb9e
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ccc1337c845e3a9c30d6fcdb08c2c87ca1938b4e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37205686"
---
# <a name="advanced-connection-properties"></a>Propriedades Avançadas de Conexão
  Use a caixa de diálogo **Propriedades Avançadas de Conexão** para adicionar mais parâmetros de conexão à cadeia de conexão.  
  
 Os parâmetros de conexão adicionais podem ser qualquer parâmetro de conexão ODBC que tem suporte pela instância de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você está usando.  
  
 Os parâmetros adicionados através da caixa de diálogo **Propriedades Avançadas de Conexão** são adicionados aos parâmetros selecionados usando as opções da caixa de diálogo **Conecte-se ao SQL Server** .  
  
 A última instância fornecida de cada parâmetro anula qualquer instância anterior do parâmetro. Parâmetros adicionados usando a caixa de diálogo **Parâmetros Avançados de Conexão** seguem e substituem os parâmetros fornecidos na caixa de diálogo **Conexão do SQL Server** . Por exemplo, se a caixa de diálogo **Conexão do SQL Server** especificar SERVER1 como o Nome do servidor e a página **Parâmetros Adicionais de Conexão** tiver ;SERVER=SERVER2, a conexão será feita ao SERVER2.  
  
 Parâmetros adicionados usando a caixa de diálogo **Propriedades Avançadas de Conexão** sempre são passados como texto sem formatação.  
  
> [!IMPORTANT]  
>  Não inclua credenciais de logon na caixa de diálogo **Propriedades Avançadas de Conexão** . Eles não serão criptografados quando forem transmitidos pela rede.  
  
## <a name="see-also"></a>Consulte também  
 [Acessar o CDC Designer Console](access-the-cdc-designer-console.md)   
 [Conexão do SQL Server para a criação de instância](sql-server-connection-for-instance-creation.md)  
  
  
