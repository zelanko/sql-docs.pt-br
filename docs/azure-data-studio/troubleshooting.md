---
title: Solução de problemas do Azure Data Studio
description: Saiba como obter logs e solucionar problemas do Azure Data Studio, o que é útil para elaborar relatórios de bugs.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: hanqin, maghan
ms.custom: seodec18
ms.date: 11/24/2020
ms.openlocfilehash: 1d2483532589cd840f1120cfb0ac3273b41e0bb5
ms.sourcegitcommit: 2e7154475ba1f31d1aeebc8f48ac05846f793736
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "95920203"
---
# <a name="azure-data-studio-troubleshooting"></a>Solução de problemas do Azure Data Studio
O Azure Data Studio rastreia problemas e solicitações de recursos usando um [rastreador de problemas do repositório do GitHub](https://github.com/Microsoft/azuredatastudio/issues) para o repositório `azuredatastudio`. 

## <a name="if-youve-experienced-any-issue"></a>Se você teve algum problema

Relate problemas no [Rastreador de Problemas do GitHub](https://github.com/Microsoft/azuredatastudio/issues) e informe-nos detalhes que ajudarão a reproduzir o erro. Inclua qualquer [informação de log](#how-to-set-the-logging-level) do arquivo de log.

## <a name="writing-good-bug-reports-and-feature-requests"></a>Escrever bons relatórios de bugs e solicitações de recursos

Faça um único registro por problema e solicitação de recurso.

* Não enumere vários bugs ou solicitações de recursos no mesmo problema.
* Não adicione seu problema como um comentário a um problema existente, a menos que seja para uma entrada idêntica. Muitos problemas parecem semelhantes, mas têm causas diferentes.

Quanto mais informações você fornecer, maior será a probabilidade de alguém conseguir reproduzir o problema e encontrar uma correção. 

Inclua as seguintes informações com cada problema:

* Versão do Azure Data Studio
* Etapas reproduzíveis (1... 2... 3...) e o que você esperava versus o que realmente ocorreu. 
* Imagens, animações ou um link para um vídeo. Imagens e animações ilustram as etapas de reprodução, mas não as substituem.
* Um snippet de código que demonstre o problema ou um link para um repositório de código que possamos obter facilmente em nosso computador para recriar o problema. 

> [!NOTE]
>  Como precisamos copiar e colar o snippet de código, a inclusão dele como um arquivo de mídia (ou seja, .gif) não é suficiente. 

* Erros no Console de Ferramentas para Desenvolvedores (Ajuda | Ativar/desativar Ferramentas para Desenvolvedores)

Lembre-se de fazer o seguinte:

* Pesquise no repositório de problemas para ver se existe uma duplicata. 
* Simplifique seu código em relação ao problema para que possamos isolá-lo de uma forma melhor. 

Não se preocupe se não conseguirmos reproduzir o problema e solicitarmos mais informações.

## <a name="how-to-set-the-logging-level"></a>Como definir o nível de registros em log

### <a name="azure-data-studio"></a>Azure Data Studio
Execute o comando `Developer: Set Log Level...` para selecionar o nível de log da sessão atual. Esse valor NÃO se mantém em várias sessões. Portanto, se você reiniciar o Azure Data Studio, ele será revertido para o nível `Info` padrão. 

Se você quiser habilitar o log de depuração para inicialização, defina o nível de log como `Debug` e execute o comando `Developer: Reload Window`

### <a name="mssql-built-in-extension"></a>MSSQL (Extensão interna)

Se a configuração de usuário `Mssql: Log Debug Info` for definida como true, as informações de log de depuração serão enviadas para o canal de saída `MSSQL`.

A configuração de usuário `Mssql: Tracing Level` é usada para controlar o detalhamento do registro em log.

## <a name="debug-log-location"></a>Local de log de depuração
No Azure Data Studio, execute o comando `Developer: Open Logs Folder` a fim de abrir o caminho para os logs. Há muitos tipos diferentes de arquivos de log que gravam nesse local, alguns dos mais usados são:

1. `renderer#.log` (por exemplo, renderer1.log) – esse é o arquivo de log para o processo principal.
1. `telemetry.log` – quando o nível de log é definido como `Trace`, esse arquivo contém os eventos de telemetria enviados pelo Azure Data Studio
1. `exthost#/exthost.log` – arquivo de log para o processo de host de extensão (esse é apenas o próprio processo, não as extensões em execução dentro dele)
1. `exthost#/Microsoft.mssql` – logs para a extensão MSSQL, que contém grande parte da lógica principal para recursos relacionados a MSSQL
   * sqltools.log é o log do Serviço de Ferramentas SQL
1. `exthost#/output_logging_#######` – essas pastas contêm as mensagens exibidas no painel `Output` no Azure Data Studio. Cada arquivo é nomeado `#-<Channel Name>`, portanto, por exemplo, o canal de saída `Notebooks` pode gerar uma saída em um arquivo chamado `3-Notebooks.log`.

Se for solicitado que você forneça logs, compacte a pasta inteira para garantir que os logs corretos sejam incluídos. 

## <a name="next-steps"></a>Próximas etapas
- [Relatar um problema](https://github.com/Microsoft/azuredatastudio/issues)
- [O que é o Azure Data Studio](what-is-azure-data-studio.md)