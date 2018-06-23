---
title: Opção de configuração de servidor clr enabled | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- assemblies [CLR integration], verifying can run
- clr enabled option
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1eb4bd97f6e008dbc84e7d7882b80cfff5c88f2c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117959"
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
>  Não há suporte para a execução de CLR (common language runtime) com lightweight pooling. Desabilite uma das duas opções: “clr enabled” ou “lightweight pooling”. Recursos que dependem de CLR e não funcionam corretamente no modo fibra incluem o `hierarchy` tipo de dados, replicação e gerenciamento baseado em políticas.  
  
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
  
  
