---
title: Opção de pré-processamento (Ferramenta de administração do Distributed Replay) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: distributed-replay
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9b5012fd-233e-4a25-a2e1-585c63b70502
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9a4a0cfe264cc5f67c5fe2f21590ffcd6abf63d0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="preprocess-option-distributed-replay-administration-tool"></a>Opção de pré-processamento (ferramenta de administração Distributed Replay)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A ferramenta de administração [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay, **DReplay.exe**, é uma ferramenta de linha de comando que você pode usar para se comunicar com o controlador de reprodução distribuída. Este tópico descreve a opção de linha de comando **preprocess** e a sintaxe correspondente.  
  
 A opção **preprocess** inicia o estágio de pré-processamento. Durante esse estágio, o controlador prepara os dados de rastreamento de entrada para retomada contra o servidor de destino.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") Para obter mais informações sobre as convenções de sintaxe usadas com a sintaxe da ferramenta de administração, confira [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dreplay preprocess [-m controller] -i input_trace_file  
    -d controller_working_dir [-c config_file] [-f status_interval]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 **-m** *controller*  
 Especifica o nome do computador do controlador. Você pode usar "`localhost`" ou "`.`" para fazer referência ao computador local.  
  
 Se o parâmetro **-m** não for especificado, será usado o computador local.  
  
 **-i** *input_trace_file*  
 Especifica o caminho completo do arquivo de rastreamento de entrada no controlador, como `D:\Mytrace.trc`. O parâmetro **-i** é obrigatório.  
  
 Se houver arquivos de substituição no mesmo diretório, eles serão carregados e usados automaticamente. Os arquivos devem seguir a convenção de nomenclatura de substituição de arquivo, por exemplo: `Mytrace.trc`, `Mytrace_1.trc`, `Mytrace_2.trc`, `Mytrace_3.trc`, ... `Mytrace_n.trc`.  
  
> [!NOTE]  
>  Se você estiver usando a ferramenta de administração em um computador diferente do controlador, precisará copiar os arquivos de rastreamento de entrada no controlador de forma que um caminho local possa ser usado para este parâmetro.  
  
 **-d** *controller_working_dir*  
 Especifica o diretório no controlador onde o arquivo intermediário será armazenado. O parâmetro **-d** é obrigatório.  
  
 Os seguintes requisitos são aplicados:  
  
-   O diretório deve residir no controlador.  
  
-   Você deve especificar o caminho completo, iniciando com uma letra da unidade (por exemplo, `c:\WorkingDir`).  
  
-   O caminho não deve terminar com uma barra invertida "`\`".  
  
-   Não há suporte para caminhos UNC.  
  
 **-c** *config_file*  
 É o caminho completo do arquivo de configuração de pré-processamento; usado para especificar o local do arquivo de configuração de pré-processamento quando armazenado em um local diferente. Esse parâmetro pode ser um caminho UNC ou pode residir localmente no computador onde você executa a ferramenta de administração.  
  
 O parâmetro **-c** não será obrigatório se nenhuma filtragem for necessária, ou se você não desejar modificar o tempo ocioso máximo.  
  
 Sem o parâmetro **-c** , o arquivo de configuração de pré-processamento padrão, `DReplay.exe.preprocess.config`, será usado.  
  
 **-f** *status_interval*  
 Especifica a frequência (em segundos) na qual exibir mensagens de status.  
  
 Se **-f** não for especificado, o intervalo padrão será de 30 segundos.  
  
## <a name="examples"></a>Exemplos  
 Neste exemplo, o estágio de pré-processamento é iniciado com todas as configurações padrão. O valor `localhost` indica que o serviço do controlador está em execução no mesmo computador que a ferramenta de administração. O parâmetro *input_trace_file* especifica o local dos dados de rastreamento de entrada, `c:\mytrace.trc`. Como não há filtragem de arquivo de rastreamento envolvida, o parâmetro **-c** deve ser especificado.  
  
```  
dreplay preprocess –m localhost -i c:\mytrace.trc -d c:\WorkingDir  
```  
  
 Neste exemplo, o estágio de pré-processamento é iniciado e um arquivo de configuração de pré-processamento modificado é especificado. Ao contrário do exemplo anterior, o parâmetro **-c** é usado para apontar para o arquivo de configuração modificado, caso tenha armazenado esse arquivo em um local diferente. Por exemplo:  
  
```  
dreplay preprocess –m localhost -i c:\mytrace.trc -d c:\WorkingDir -c c:\DReplay.exe.preprocess.config  
```  
  
 No arquivo de configuração de pré-processamento modificado, é adicionada uma condição de filtro que filtra sessões de sistema durante reprodução distribuída. O filtro é adicionado modificando o elemento `<PreprocessModifiers>` no arquivo de configuração de pré-processamento, `DReplay.exe.preprocess.config`.  
  
 O exemplo a seguir mostra um arquivo de configuração modificado:  
  
```  
<?xml version='1.0'?>  
<Options>  
    <PreprocessModifiers>  
        <IncSystemSession>No</IncSystemSession>  
        <MaxIdleTime>-1</MaxIdleTime>  
    </PreprocessModifiers>  
</Options>  
```  
  
## <a name="permissions"></a>Permissões  
 Você deve executar a ferramenta de administração como um usuário interativo, um usuário local ou uma conta de usuário de domínio. Para usar uma conta de usuário local, a ferramenta de administração e o controlador devem estar em execução no mesmo computador.  
  
 Para saber mais, confira [Distributed Replay Security](../../tools/distributed-replay/distributed-replay-security.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Preparar os dados de rastreamento de entrada](../../tools/distributed-replay/prepare-the-input-trace-data.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)   
 [Configurar o Distributed Replay](../../tools/distributed-replay/configure-distributed-replay.md)  
  
  
