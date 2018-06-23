---
title: Preparar os dados de rastreamento de entrada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c14fd3d2-5770-47c2-a851-cc13ddbc9bf5
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 30b9108a8586e56f7a96695be513e6e33fe39c85
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121816"
---
# <a name="prepare-the-input-trace-data"></a>Preparar os dados de rastreamento de entrada
  Antes de iniciar uma reprodução distribuída com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Distributed Replay, é necessário preparar os dados de rastreamento de entrada iniciando o estágio de pré-processamento da ferramenta de administração de reprodução distribuída. No estágio de pré-processamento, o controlador de reprodução distribuída processa os dados de rastreamento e gera um arquivo intermediário:  
  
 ![Estágio de pré-processamento de reprodução distribuída](../../database-engine/media/preprocess.gif "estágio de pré-processamento de reprodução distribuída")  
  
 Para obter mais informações sobre o estágio de pré-processamento, consulte [SQL Server Distributed Replay](sql-server-distributed-replay.md).  
  
> [!NOTE]  
>  Os dados de rastreamento de entrada devem ser capturados em uma versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que seja compatível com o Distributed Replay. Os dados de rastreamento de entrada também devem ser compatíveis com o servidor de destino no qual você deseja reproduzir os dados de rastreamento. Para obter mais informações sobre os requisitos da versão, consulte [Distributed Replay Requirements](distributed-replay-requirements.md).  
  
### <a name="to-prepare-the-input-trace-data"></a>Para preparar os dados de rastreamento de entrada  
  
1.  **(Opcional) Modifique as definições de configuração de pré-processamento**: se desejar modificar as definições de configuração de pré-processamento, como a opção de filtrar sessões do sistema ou configurar o tempo ocioso máximo, modifique o elemento `<PreprocessModifiers>` do arquivo de configuração de pré-processamento baseado em XML, `DReplay.exe.preprocess.config`. Se você modificar o arquivo de configuração de pré-processamento, é recomendável modificar uma cópia em vez do original. Para modificar as configurações, siga estas etapas:  
  
    1.  Faça uma cópia do arquivo de configuração de pré-processamento padrão, `DReplay.exe.preprocess.config`, e renomeie o novo arquivo. O arquivo de configuração de pré-processamento padrão está localizado na pasta de instalação da ferramenta de administração.  
  
    2.  Modifique os parâmetros de configuração de pré-processamento no novo arquivo de configuração.  
  
    3.  Ao iniciar o estágio de pré-processamento (a próxima etapa), use o parâmetro *config_file* da opção **preprocess** para especificar o local do arquivo de configuração modificado.  
  
     Para obter mais informações sobre o arquivo de configuração de pré-processo, veja [Configurar o Distributed Replay](configure-distributed-replay.md).  
  
2.  **Inicie o estágio de pré-processamento**: para preparar os dados de rastreamento de entrada, execute a ferramenta de administração com a opção **preprocess** . Para obter mais informações, veja [Opção de Pré-processamento &#40;Ferramenta de administração do Distributed Replay&#41;](preprocess-option-distributed-replay-administration-tool.md).  
  
    1.  Abra o utilitário de Prompt de comando do Windows (`CMD.exe`) e navegue até o local de instalação da ferramenta de administração Distributed Replay (`DReplay.exe`).  
  
    2.  (Opcional) Use o parâmetro *controller* , **-m**, para especificar o controlador, se o serviço de controlador estiver em execução em um computador diferente da ferramenta de administração.  
  
    3.  Use o parâmetro *input_trace_file* , **-i**, para especificar o local e o nome dos arquivos de rastreamento de entrada.  
  
    4.  Use o parâmetro *controller_working_directory* , **-d**, para especificar o local em que o arquivo intermediário deve ser salvo no controlador.  
  
    5.  (Opcional) Use o parâmetro *config_file* , **-c**, para especificar o local do arquivo de configuração de pré-processamento. Use esse parâmetro para apontar para o novo arquivo de configuração, caso você tenha modificado uma cópia do arquivo de configuração de pré-processamento padrão.  
  
    6.  (Opcional) Use o parâmetro *status_interval* , **-f**, para especificar se deseja que a ferramenta de administração exiba mensagens de status em uma frequência diferente de 30 segundos.  
  
     Por exemplo, ao iniciar o estágio de pré-processamento no mesmo computador que o serviço de controlador para um arquivo de rastreamento localizado em `c:\trace1.trc`, um diretório de trabalho de controlador localizado em `c:\WorkingDir` , e uma mensagem de status exibida no valor padrão de 30 segundos, a seguinte sintaxe é necessária: `dreplay preprocess -i c:\trace1.trc -d c:\WorkingDir`  
  
3.  Depois que o estágio de pré-processamento for concluído, o arquivo intermediário é armazenado no diretório de trabalho do controlador. Para iniciar o estágio de reprodução do evento, execute a ferramenta de administração com a opção **replay** . Para obter mais informações, veja [Reproduzir dados de rastreamento](replay-trace-data.md).  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)   
 [Requisitos do Distributed Replay](distributed-replay-requirements.md)   
 [Opções de linha de comando da ferramenta de administração &#40;Distributed Replay Utility&#41;](administration-tool-command-line-options-distributed-replay-utility.md)   
 [Configurar o Distributed Replay](configure-distributed-replay.md)  
  
  