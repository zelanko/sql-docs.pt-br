---
description: Exibições do aplicativo da camada de dados-dbo.sysdac_instances
title: dbo.sysdac_instances (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysdac_instances_TSQL
- sysdac_instances
- sysdac_instances_TSQL
- dbo.sysdac_instances
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.sysdac_instances
- sysdac_instances
ms.assetid: 28285f3d-3889-439f-8b24-3bdef08e46b4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 77aafe21c2aa67b55d7c2d9319ab2699585c697c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475493"
---
# <a name="data-tier-application-views---dbosysdac_instances"></a>Exibições do aplicativo da camada de dados-dbo.sysdac_instances
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe uma linha para cada instância do DAC (Aplicativo da Camada de Dados) implantada a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. sysdac_instances pertence ao esquema dbo no banco de dados msdb. A tabela a seguir descreve as colunas na exibição sysdac_instances.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|instance_id|**uniqueidentifier**|Identificador da instância do DAC.|  
|instance_name|**sysname**|Nome da instância do DAC especificada quando o DAC foi implantado.|  
|type_name|**sysname**|Nome do DAC especificado quando o pacote do DAC foi criado.|  
|type_version|**nvarchar (64)**|Versão do DAC especificado quando o pacote do DAC foi criado.|  
|descrição|**nvarchar(4000)**|Uma descrição do DAC escrita quando o pacote do DAC foi criado.|  
|type_stream|**varbinary(max)**|Fluxo que contém uma representação codificada dos objetos lógicos, como tabelas e exibições, contidos no DAC.|  
|date_created|**datetime**|Data e hora em que a instância do DAC foi criada.|  
|created_by|**sysname**|Logon que criou a instância do DAC.|  
|database_name|**sysname**|Nome do banco de dados criado para a instância do DAC.|  
  
## <a name="remarks"></a>Comentários  
 Um DAC inclui um tipo de DAC que é uma definição dos objetos da camada de dados lógicos usados por um aplicativo, como tabelas e exibições. Um pacote do DAC é um arquivo usado para implantar um DAC. O pacote do DAC contém uma representação de todos os objetos lógicos contidos no tipo do DAC. O pacote do DAC pode ser usado para implantar uma ou mais cópias, ou instâncias, do DAC em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Cada instância do DAC implantada a partir do mesmo pacote do DAC compartilha o mesmo tipo, mas é atribuída a um nome e identificador de instância exclusivos.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin para exibir todas as colunas. Os membros da função pública podem exibir as colunas instance_name, description e type_version.  
  
## <a name="see-also"></a>Consulte Também  
 [Aplicativos da Camada de Dados](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Exibições de aplicativo da camada de dados &#40;&#41;Transact-SQL ](https://msdn.microsoft.com/library/0de01328-d7a6-4677-b7a0-dcd3098c23d4)  
  
  
