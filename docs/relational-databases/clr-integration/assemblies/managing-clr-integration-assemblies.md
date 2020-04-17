---
title: Gerenciando as Assembléias de Integração da CLR | Microsoft Docs
description: Você pode hospedar conjuntos DLL gerenciados no SQL Server.  Você pode registrar, alterar e soltar conjuntos e também gerenciar arquivos e permissões associados.
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
ms.openlocfilehash: 19b90d7994aa4b75a294f24345d43333d13a22df
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484615"
---
# <a name="managing-clr-integration-assemblies"></a>Gerenciando assemblies de integração CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O código gerenciado é compilado e implantado em unidades chamadas de assembly. Um assembly é empacotado como uma DLL ou um arquivo executável (.exe). Um arquivo executável pode ser executado sozinho, mas uma DLL precisa ser hospedada em um aplicativo existente. Os conjuntos dll gerenciados podem ser [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]carregados e hospedados por . O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exige que você registre o assembly em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a instrução CREATE ASSEMBLY, antes que ele seja carregado no processo e usado. Os assemblies também podem ser atualizados de uma versão mais recente usando a instrução ALTER ASSEMBLY ou removidos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a instrução DROP ASSEMBLY.  
  
 As informações de montagem são armazenadas na tabela **sys.assembly_files** no banco de dados onde o conjunto foi instalado. A tabela **sys.assembly_files** contém as seguintes colunas.  
  
|Coluna|Descrição|  
|------------|-----------------|  
|assembly_id|O identificador definido para o assembly. Este número é atribuído a todos os objetos relacionados ao mesmo assembly.|  
|name|O nome do objeto.|  
|file_id|Um número que identifica cada objeto, com o primeiro objeto associado a um dado **assembly_id** sendo dado o valor de 1. Se vários objetos estiverem associados com o mesmo **assembly_id,** cada valor **de file_id** subseqüente será incrementado por 1.|  
|content|A representação hexadecimal do assembly ou arquivo.|  
  
## <a name="in-this-section"></a>Nesta seção  
 [Criando um assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
 Discute a criação de assemblies SAFE, EXTERNAL_ACCESS e UNSAFE CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Alterando um assembly](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)  
 Descreve a atualização de assemblies CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Descartando um assembly](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)  
 Discute o descarte de assemblies CLR do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança de Integração CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Segurança de acesso a código da integração CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
  
  
