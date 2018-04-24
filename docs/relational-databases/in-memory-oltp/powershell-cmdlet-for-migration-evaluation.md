---
title: Cmdlet do PowerShell para avaliação de migração | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 117250d3-9982-47fe-94fd-6f29f6159940
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7e6f051e918e96e2d7e5c4db951b1b4ea9ed23c7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="powershell-cmdlet-for-migration-evaluation"></a>Cmdlet do PowerShell para Avaliação da Migração
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O cmdlet Save-SqlMigrationReport é uma ferramenta que avalia a adequação da migração de vários objetos em um banco de dados do SQL Server. Atualmente, ele é limitado pela avaliação da adequação da migração para o OLTP na Memória. O cmdlet pode ser executado em um ambiente do Windows PowerShell com privilégios elevados e no sqlps.  
  
## <a name="syntax"></a>Sintaxe  
  
```powershell  
Save-SqlMigrationReport [ -MigrationType OLTP ] [ -Server server -Database database [ -Object object_name ] ]  |  [ -InputObject smo_object ] -FolderPath path  
```  
  
#### <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros.  
  
|Parâmetros|Description|  
|----------------|-----------------|  
|MigrationType|O tipo de cenário de migração que o cmdlet tem como destino. Atualmente, o único valor é o OLTP padrão. Opcional.|  
|Servidor|O nome da instância do SQL Server de destino. Obrigatório no ambiente do Windows Powershell, se o parâmetro - InputObject não for fornecido. Opcional no SQLPS.|  
|banco de dados|O nome do banco de dados do SQL Server de destino. Obrigatório no ambiente do Windows Powershell, se o parâmetro -InputObject não for fornecido. Opcional no SQLPS.|  
|Object|O nome do objeto de banco de dados de destino. Pode ser uma tabela ou um procedimento armazenado.|  
|InputObject|O objeto SMO que o cmdlet deve ter como destino. Obrigatório no ambiente do Windows Powershell, se -Server e -Database não forem fornecidos. Opcional no SQLPS.|  
|FolderPath|A pasta em que o cmdlet deve colocar os relatórios gerados. Obrigatórios.|  
  
## <a name="results"></a>Resultados  
 Na pasta especificada no parâmetro - FolderPath, haverá dois nomes de pasta: Tables e Stored Procedures. Se o objeto de destino for uma tabela, o relatório estará na pasta Tables. Caso contrário, ele estará na pasta Stored Procedures.  
  
  
