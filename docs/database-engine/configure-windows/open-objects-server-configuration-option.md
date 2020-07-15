---
title: Opção de configuração de servidor open objects | Microsoft Docs
description: Saiba mais sobre a opção de configuração desabilitada "objetos abertos". Veja como o SQL Server agora gerencia o número de objetos de banco de dados abertos.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- open objects option
ms.assetid: c8424d3c-86ba-4cc5-bf0c-be4ce44bdd04
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0bbcb11a80f06eae10e5481c965e9216cc84695e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773625"
---
# <a name="open-objects-server-configuration-option"></a>Opção de configuração de servidor open objects
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta opção ainda está presente em **sp_configure**, embora a funcionalidade dela tenha sido desabilitada no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. (A configuração não tem nenhum efeito.) Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o número de objetos de banco de dados abertos é gerenciado dinamicamente e é limitado somente pela memória disponível. A opção **open objects** disponível em **sp_configure** para compatibilidade com versões anteriores com scripts existentes.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
