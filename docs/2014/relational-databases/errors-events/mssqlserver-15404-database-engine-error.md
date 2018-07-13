---
title: MSSQLSERVER_15404 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 15404 (Database Engine error)
ms.assetid: 69677f02-bc81-4e4a-99b8-5c1bd1de36df
caps.latest.revision: 6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f3aa429a44d38977295cb3e4a51cc1ede283ab0f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37411006"
---
# <a name="mssqlserver15404"></a>MSSQLSERVER_15404
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|15404|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_NTGRP_ERROR|  
|Texto da mensagem|Não foi possível obter informações sobre o grupo/usuário '*user*' do Windows NT, código de erro *code*.|  
  
## <a name="explanation"></a>Explicação  
 15404 é usado na autenticação quando uma entidade de segurança inválida é especificada. A representação de uma conta do Windows falha porque não há uma relação de confiança total entre a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o domínio da conta do Windows.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique se a entidade de segurança do Windows existe e não está digitada de forma incorreta.  
  
 Se esse erro for resultante da falta de uma relação de confiança total entre a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o domínio da conta do Windows, uma destas ações poderá corrigir o erro:  
  
-   Use uma conta do mesmo domínio que o usuário do Windows para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver usando uma conta de computador como Serviço de Rede ou Sistema Local, o computador deverá ser confiável no domínio que contém o usuário do Windows.  
  
-   Usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
