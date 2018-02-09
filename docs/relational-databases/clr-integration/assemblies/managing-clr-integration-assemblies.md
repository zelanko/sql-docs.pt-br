---
title: "Gerenciando Assemblies de integração CLR | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- database objects [CLR integration], assemblies
- common language runtime [SQL Server], assemblies
- assemblies [CLR integration], managing
ms.assetid: bdbbf325-14f6-460e-a35a-d3861d3c961e
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 97aaba3b56cce6bceafa02a1ef3bfca93d05a5c4
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="managing-clr-integration-assemblies"></a>Gerenciando assemblies de integração CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
O código gerenciado é compilado e implantado em unidades chamadas de assembly. Um assembly é empacotado como uma DLL ou um arquivo executável (.exe). Um arquivo executável pode ser executado sozinho, mas uma DLL precisa ser hospedada em um aplicativo existente. Os assemblies DLL gerenciados podem ser carregados no e hospedados por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exige que você registre o assembly em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a instrução CREATE ASSEMBLY, antes que ele seja carregado no processo e usado. Os assemblies também podem ser atualizados de uma versão mais recente usando a instrução ALTER ASSEMBLY ou removidos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a instrução DROP ASSEMBLY.  
  
 Informações de assembly são armazenadas no **assembly_files** tabela no banco de dados onde o assembly foi instalado. O **assembly_files** tabela contém as seguintes colunas.  
  
|Coluna|Description|  
|------------|-----------------|  
|assembly_id|O identificador definido para o assembly. Este número é atribuído a todos os objetos relacionados ao mesmo assembly.|  
|name|O nome do objeto.|  
|file_id|Um número que identifica cada objeto, com o primeiro objeto associado com um determinado **assembly_id** recebendo o valor de 1. Se vários objetos estão associados com o mesmo **assembly_id**, em seguida, cada subsequentes **file_id** valor é incrementado em 1.|  
|content|A representação hexadecimal do assembly ou arquivo.|  
  
## <a name="in-this-section"></a>Nesta seção  
 [Criando um Assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
 Discute a criação de assemblies SAFE, EXTERNAL_ACCESS e UNSAFE CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Alterando um assembly](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)  
 Descreve a atualização de assemblies CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Descarte de um assembly](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)  
 Discute o descarte de assemblies CLR do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Segurança da integração CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Segurança de acesso do código da integração CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
  
  
