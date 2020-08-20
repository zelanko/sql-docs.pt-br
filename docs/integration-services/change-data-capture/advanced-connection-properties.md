---
description: Propriedades Avançadas de Conexão
title: Propriedades da Conexão Avançadas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4edfab68-7e68-45e8-a3f3-a0049ff7eb9e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fd7ed8863356ff3e6b67d456628bd3dbc1ab6a5b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484733"
---
# <a name="advanced-connection-properties"></a>Propriedades Avançadas de Conexão

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use a caixa de diálogo **Propriedades Avançadas de Conexão** para adicionar mais parâmetros de conexão à cadeia de conexão.  
  
 Os parâmetros de conexão adicionais podem ser qualquer parâmetro de conexão ODBC que tem suporte pela instância de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você está usando.  
  
 Os parâmetros adicionados através da caixa de diálogo **Propriedades Avançadas de Conexão** são adicionados aos parâmetros selecionados usando as opções da caixa de diálogo **Conecte-se ao SQL Server** .  
  
 A última instância fornecida de cada parâmetro anula qualquer instância anterior do parâmetro. Parâmetros adicionados usando a caixa de diálogo **Parâmetros Avançados de Conexão** seguem e substituem os parâmetros fornecidos na caixa de diálogo **Conexão do SQL Server** . Por exemplo, se a caixa de diálogo **Conexão do SQL Server** especificar SERVER1 como o Nome do servidor e a página **Parâmetros Adicionais de Conexão** tiver ;SERVER=SERVER2, a conexão será feita ao SERVER2.  
  
 Parâmetros adicionados usando a caixa de diálogo **Propriedades Avançadas de Conexão** sempre são passados como texto sem formatação.  
  
> [!IMPORTANT]  
>  Não inclua credenciais de logon na caixa de diálogo **Propriedades Avançadas de Conexão** . Eles não serão criptografados quando forem transmitidos pela rede.  
  
## <a name="see-also"></a>Consulte Também  
 [Acessar o CDC Designer Console](../../integration-services/change-data-capture/access-the-cdc-designer-console.md)   
 [Conexão de SQL Server para a criação de instância](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md)  
  
  
