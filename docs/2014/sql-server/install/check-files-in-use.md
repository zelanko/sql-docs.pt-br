---
title: Verificar arquivos em uso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ccd65867-d4c0-43b2-8361-7fd41c6f79ac
caps.latest.revision: 10
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 32e2152d93cc49309b6824462f5d413d59d30daf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37242306"
---
# <a name="check-files-in-use"></a>Verificar arquivos em uso
  Para evitar a necessidade de reiniciar o Windows após a instalação das atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use a página Verificar Arquivos em Uso para identificar processos que estão bloqueando arquivos necessários ao programa de Instalação de atualização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Pare todos os aplicativos e serviços que façam conexões com as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo atualizado. Isso inclui parar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Se a Instalação determinar que arquivos estão bloqueados durante a instalação, talvez seja necessário reiniciar o computador após a conclusão da instalação. Se necessário, a Instalação solicitará que você reinicie o computador. Se o programa de Instalação precisar parar um serviço durante a instalação, ele reiniciará o serviço após a conclusão da instalação.  
  
 Para eliminar a necessidade de reiniciar o computador após a instalação, a Instalação exibirá uma lista de processos que estão bloqueando arquivos. Pare ou termine os processos e os aplicativos na lista. Em seguida, clique em **Atualizar verificação** para executar a verificação novamente. Clique em **Parar verificação** para encerrar uma verificação que esteja em execução. Se arquivos bloqueados não forem encontrados, a tabela estará vazia. Quando todos os processos bloqueados tiverem sido fechados ou parados, clique em **Avançar** para continuar.  
  
 A Instalação registra as informações nos arquivos de log. Para obter mais informações sobre como exibir os arquivos de log, veja [Como exibir os arquivos de log da instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md) e [Como ler um arquivo de log da Instalação do SQL Server](http://go.microsoft.com/fwlink/?LinkID=134490).  
  
 As seguintes informações estão incluídas no arquivo de log:  
  
-   Nome do processo  
  
-   Nome do recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Tipo de processo  
  
-   Conta sob a qual o processo está sendo executado  
  
-   ID do Processo  
  
-   Nome do arquivo bloqueado  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
  
|Nome|Description|  
|----------|-----------------|  
|Processar|Exibe o nome completo do processo que está usando os arquivos a serem atualizados.|  
|Tipo|Exibe o tipo de processo.|  
|Conta|Exibe a conta sob a qual o processo está sendo executado.|  
|ID do Processo|Exibe a ID do processo.|  
  
  
