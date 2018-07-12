---
title: MSSQLSERVER_26014 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 26014 (Database Engine error)
ms.assetid: e2b0dfc7-0681-4e5d-8875-1d5f63534086
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b018c28ec8f718d74d00aec1cdb6fa74b9140118
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411035"
---
# <a name="mssqlserver26014"></a>MSSQLSERVER_26014
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|26014|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SNI_SSL_USER_CERT_FAILURE|  
|Texto da mensagem|Não foi possível carregar o certificado especificado pelo usuário [Cert Hash (sha1) "% hs"]. O servidor não aceitará uma conexão. Verifique se o certificado está instalado corretamente. Consulte "Configuring Certificate for Use by SSL" nos Manuais Online (em inglês).|  
  
## <a name="explanation"></a>Explicação  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tentou carregar o certificado indicado na mensagem, mas a operação não foi bem-sucedida. Esse problema deve ser resolvido para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possa usar o certificado.  
  
 As possíveis causas do erro incluem as seguintes:  
  
-   O certificado pode ter sido movido ou excluído.  
  
-   Se o logon usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mudou, talvez o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tenha permissão para acessar o certificado.  
  
-   O certificado pode ter expirado.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique se o certificado indicado na mensagem existe no sistema, se pode ser acessado e se é válido para uso.  
  
  
