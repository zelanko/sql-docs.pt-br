---
title: Propriedades do SQL Server (Página FILESTREAM) | Microsoft Docs
description: Familiarize-se com as configurações de FILESTREAM no SQL Server. Saiba como ativar FILESTREAM e veja como configurar o acesso de cliente remoto e outras propriedades.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.filestream.f1
helpviewer_keywords:
- FILESTREAM [SQL Server], properties page
ms.assetid: 8a8d38d3-e97a-4b09-a40b-659b2e3a5c47
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 81edbd9bfc913f9d339625a993f866d44e1a313b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730933"
---
# <a name="server-properties---filestream-page"></a>Propriedades do servidor – página FILESTREAM
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use esta página para habilitar FILESTREAM para esta instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 **Habilitar FILESTREAM para acesso Transact-SQL**  
 Selecione para habilitar FILESTREAM para acesso [!INCLUDE[tsql](../../includes/tsql-md.md)] . Este controle deve ser verificado antes que as demais opções de controle fiquem disponíveis.  
  
 **Habilitar FILESTREAM para acesso de fluxo de E/S de arquivo**  
 Selecione para habilitar o acesso de fluxo Win32 para FILESTREAM.  
  
 **Nome de compartilhamento do Windows**  
 Use este controle para digitar o nome do compartilhamento do Windows no qual os dados FILESTREAM serão armazenados.  
  
 **Permitir que clientes remotos tenham acesso de fluxo a dados FILESTREAM**  
 Selecione este controle para permitir que clientes remotos acessem dados FILESTREAM neste servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
