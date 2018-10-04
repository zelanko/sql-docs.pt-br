---
title: Opção de configuração de servidor clr enabled | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- assemblies [CLR integration], verifying can run
- clr enabled option
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a796426f02c2ad9c0878c212c51eb0e90cfce8bf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219367"
---
# <a name="clr-enabled-server-configuration-option"></a>Opção clr enabled de configuração de servidor
  Use a opção clr habilitado para especificar se assemblies de usuário podem ser executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A opção clr enabled fornece os seguintes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|0|Execução de assembly não permitida no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|1|Execução de assembly permitida no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 Servidores WOW64 devem ser reiniciados antes das alterações nessa configuração entrarem em vigor. A reinicialização não é necessária para outros tipos de servidores.  
  
> [!NOTE]  
>  Quando RECONFIGURE é executado e o valor de execução da opção clr ativado é alterado de 1 para 0, todos os domínios de aplicativo que contêm assemblies de usuário são descarregados imediatamente.  
  
> [!NOTE]  
>  Não há suporte para a execução de CLR (common language runtime) com lightweight pooling. Desabilite uma das duas opções: “clr enabled” ou “lightweight pooling”. Os recursos que dependem de CLR e que não funcionam corretamente no modo fibra incluem o `hierarchy` tipo de dados, replicação e gerenciamento baseado em políticas.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir primeiro mostra a configuração atual da opção clr enabled e, em seguida, habilita a opção configurando o valor da opção como 1. Para desabilitar a opção, defina o valor para 0.  
  
```  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Opção lightweight pooling de configuração de Servidor](lightweight-pooling-server-configuration-option.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [Opção lightweight pooling de configuração de Servidor](lightweight-pooling-server-configuration-option.md)  
  
  
