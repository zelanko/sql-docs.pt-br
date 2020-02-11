---
title: Gerenciando assemblies de integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- database objects [CLR integration], assemblies
- common language runtime [SQL Server], assemblies
- assemblies [CLR integration], managing
ms.assetid: bdbbf325-14f6-460e-a35a-d3861d3c961e
author: rothja
ms.author: jroth
ms.openlocfilehash: b3476ba45f7f563524cdfd9855e80f9c5dd96524
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054451"
---
# <a name="managing-clr-integration-assemblies"></a>Gerenciando assemblies de integração CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O código gerenciado é compilado e implantado em unidades chamadas de assembly. Um assembly é empacotado como uma DLL ou um arquivo executável (.exe). Um arquivo executável pode ser executado sozinho, mas uma DLL precisa ser hospedada em um aplicativo existente. Os assemblies DLL gerenciados podem ser carregados e hospedados pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exige que você registre o assembly em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a instrução CREATE ASSEMBLY, antes que ele seja carregado no processo e usado. Os assemblies também podem ser atualizados de uma versão mais recente usando a instrução ALTER ASSEMBLY ou removidos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a instrução DROP ASSEMBLY.  
  
 As informações do assembly são armazenadas na tabela **Sys. assembly_files** no banco de dados em que o assembly foi instalado. A tabela **Sys. assembly_files** contém as colunas a seguir.  
  
|Coluna|DESCRIÇÃO|  
|------------|-----------------|  
|assembly_id|O identificador definido para o assembly. Este número é atribuído a todos os objetos relacionados ao mesmo assembly.|  
|name|O nome do objeto.|  
|file_id|Um número que identifica cada objeto, com o primeiro objeto associado a um determinado **assembly_id** dado o valor de 1. Se vários objetos estiverem associados ao mesmo **assembly_id**, cada valor de **file_id** subsequente será incrementado em 1.|  
|conteúdo|A representação hexadecimal do assembly ou arquivo.|  
  
## <a name="in-this-section"></a>Nesta seção  
 [Criando um assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
 Discute a criação de assemblies SAFE, EXTERNAL_ACCESS e UNSAFE CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Alterando um assembly](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)  
 Descreve a atualização de assemblies CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Descartando um assembly](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)  
 Discute o descarte de assemblies CLR do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança de integração CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Segurança de acesso a código da integração CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
  
  
