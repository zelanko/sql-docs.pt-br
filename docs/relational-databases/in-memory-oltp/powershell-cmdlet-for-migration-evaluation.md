---
title: Cmdlet do PowerShell para avaliação de migração | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 117250d3-9982-47fe-94fd-6f29f6159940
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1903907268847f2d8e84a338f8bc3cf2135aba17
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34327098"
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
  
|Parâmetros|Descrição|  
|----------------|-----------------|  
|MigrationType|O tipo de cenário de migração que o cmdlet tem como destino. Atualmente, o único valor é o OLTP padrão. Opcional.|  
|Servidor|O nome da instância do SQL Server de destino. Obrigatório no ambiente do Windows Powershell, se o parâmetro - InputObject não for fornecido. Opcional no SQLPS.|  
|banco de dados|O nome do banco de dados do SQL Server de destino. Obrigatório no ambiente do Windows Powershell, se o parâmetro -InputObject não for fornecido. Opcional no SQLPS.|  
|Object|O nome do objeto de banco de dados de destino. Pode ser uma tabela ou um procedimento armazenado.|  
|InputObject|O objeto SMO que o cmdlet deve ter como destino. Obrigatório no ambiente do Windows Powershell, se -Server e -Database não forem fornecidos. Opcional no SQLPS.|  
|FolderPath|A pasta em que o cmdlet deve colocar os relatórios gerados. Obrigatórios.|  
  
## <a name="results"></a>Resultados  
 Na pasta especificada no parâmetro - FolderPath, haverá dois nomes de pasta: Tables e Stored Procedures. Se o objeto de destino for uma tabela, o relatório estará na pasta Tables. Caso contrário, ele estará na pasta Stored Procedures.  
  
  
