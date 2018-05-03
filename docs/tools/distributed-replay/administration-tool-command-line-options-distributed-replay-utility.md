---
title: Opções de linha de comando da ferramenta de administração (utilitário Distributed Replay) | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: distributed-replay
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c01b0ed3-67e4-4561-92d2-a8fbb086aca8
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 225724b8c1e3132344a4769be9f3b6195337e5ca
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="administration-tool-command-line-options-distributed-replay-utility"></a>Opções de linha de comando da ferramenta de administração (Distributed Replay Utility)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A ferramenta de administração [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay, **DReplay.exe**, é uma ferramenta de linha de comando para se comunicar com o controlador de reprodução distribuída. Use a ferramenta de administração para iniciar, monitorar e cancelar operações no controlador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") Para obter mais informações sobre as convenções de sintaxe usadas com a sintaxe da ferramenta de administração, confira [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dreplay {preprocess|replay|status|cancel} [options] [-?]}  
  
Usage:  
  
  dreplay preprocess [-m controller] -i input_trace_file  
    -d controller_working_dir [-c config_file] [-f status_interval]  
  
  dreplay replay [-m controller] -d controller_working_dir [-o]  
    [-s target_server] -w clients [-c config_file]  
    [-f status_interval]  
  
  dreplay status [-m controller] [-f status_interval]  
  
  dreplay cancel [-m controller] [-q]   
```  
  
## <a name="remarks"></a>Remarks  
 É possível emitir as seguintes opções de linha de comando com **DReplay.exe**:  
  
 **preprocess**  
 Inicia o estágio de pré-processamento. O controlador prepara os dados de rastreamento de entrada que você capturou do ambiente de produção para a reprodução contra o servidor de destino.  
  
 **reproduzir**  
 Inicia o estágio de reprodução do evento. O controlador despacha dados de reprodução aos clientes especificados, inicia a reprodução distribuída e sincroniza os clientes. Opcionalmente, cada cliente selecionado registra a atividade de reprodução e salva arquivos de rastreamento de resultado localmente.  
  
 **status**  
 Consulta o controlador e exibe o status atual.  
  
 **cancel**  
 Cancela a operação atual em execução no controlador.  
  
 Para obter informações detalhadas de sintaxe, incluindo argumentos e exemplos de comandos, consulte os seguintes tópicos:  
  
-   [Opção Pré-processamento &#40;Ferramenta de administração de reprodução distribuída&#41;](../../tools/distributed-replay/preprocess-option-distributed-replay-administration-tool.md)  
  
-   [Opção Reprodução &#40;Ferramenta de administração de reprodução distribuída&#41;](../../tools/distributed-replay/replay-option-distributed-replay-administration-tool.md)  
  
-   [Opção Status &#40;Ferramenta de administração de reprodução distribuída&#41;](../../tools/distributed-replay/status-option-distributed-replay-administration-tool.md)  
  
-   [Opção Cancelamento &#40;Ferramenta de administração de reprodução distribuída&#41;](../../tools/distributed-replay/cancel-option-distributed-replay-administration-tool.md)  
  
 Os RPCs são executados novamente como RPCs e não como eventos de idioma.  
  
## <a name="permissions"></a>Permissões  
 Você deve executar a ferramenta de administração como um usuário interativo, um usuário local ou uma conta de usuário de domínio. Para usar uma conta de usuário local, a ferramenta de administração e o controlador devem estar em execução no mesmo computador.  
  
 Para saber mais, confira [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>Confira também  
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
