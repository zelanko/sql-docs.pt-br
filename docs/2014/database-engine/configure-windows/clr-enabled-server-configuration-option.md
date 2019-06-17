---
title: Opção de configuração de servidor clr enabled | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- assemblies [CLR integration], verifying can run
- clr enabled option
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 45c72bc5b811fec8e5532d5d03d4552cc2e0d319
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62786675"
---
# <a name="clr-enabled-server-configuration-option"></a>Opção clr enabled de configuração de servidor
  Use a opção clr habilitado para especificar se assemblies de usuário podem ser executados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A opção clr enabled fornece os seguintes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0|Execução de assembly não permitida no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|1|Execução de assembly permitida no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 Servidores WOW64 devem ser reiniciados antes das alterações nessa configuração entrarem em vigor. A reinicialização não é necessária para outros tipos de servidores.  
  
> [!NOTE]  
>  Quando RECONFIGURE é executado e o valor de execução da opção clr ativado é alterado de 1 para 0, todos os domínios de aplicativo que contêm assemblies de usuário são descarregados imediatamente.  
  
> [!NOTE]  
>  Não há suporte para a execução de CLR (common language runtime) com lightweight pooling. Desabilite uma das duas opções: “clr enabled” ou “lightweight pooling”. Os recursos que dependem de CLR e que não funcionam corretamente no modo fibra incluem o tipo de dados `hierarchy`, replicação e Gerenciamento Baseado em Políticas.  
  
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
  
  
