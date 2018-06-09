---
title: Guia de Introdução com o SSMA para o Console do DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: f245c017-023e-4880-8721-8908d339525e
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6990e771de81bbb3df4069f65104b8b41c308807
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774882"
---
# <a name="getting-started-with-ssma--for-db2-console-db2tosql"></a>Guia de Introdução com o SSMA para o Console do DB2 (DB2ToSQL)
Esta seção descreve o procedimento para iniciar e começar a trabalhar com o aplicativo de console do DB2. Também é listado, aqui, são as convenções usadas em uma janela de saída do Console SSMA típica.  
  
## <a name="launching-ssma-console"></a>Iniciar Console do SSMA  
Use as etapas a seguir para iniciar o aplicativo de console SSMA:  
  
1.  Vá para **iniciar** e aponte para **todos os programas**.  
  
2.  Clique o  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Assistente de migração para o Prompt de comando do DB2** atalho.  
  
    Exibe o menu de uso do Console SSMA e `(/? Help)`, para ajudá-lo a começar com o aplicativo de console.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimento para usar o Console do SSMA  
Depois que o console é iniciado com êxito em seu sistema Windows, você pode usar as etapas a seguir para trabalhar nela:  
  
1.  Configure o Console do SSMA através dos arquivos de script. Para obter mais informações sobre esta seção, consulte [criando arquivos de Script &#40;DB2ToSQL&#41; ](../../ssma/db2/creating-script-files-db2tosql.md) .  
  
2.  [Criando arquivos do valor da variável &#40;DB2ToSQL&#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
  
3.  [Criar os arquivos de Conexão de servidor &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
4.  [Executar o Console SSMA &#40;DB2ToSQL&#41; ](../../ssma/db2/executing-the-ssma-console-db2tosql.md) com base em suas necessidades de projeto  
  
Recursos adicionais:  
  
1.  [Gerenciamento de senhas](http://msdn.microsoft.com/en-us/56d546e3-8747-4169-aace-693302667e94) e exportar / importá-lo em outros computadores da janela  
  
2.  [Gerando relatórios](http://msdn.microsoft.com/en-us/69ef5fd9-190d-4c58-8199-b3f77d5e1883) para exibir o xml detalhado a saída de relatórios para avaliação /conversion e migração de dados. Relatórios de erro detalhadas também podem ser gerados para os comandos de atualização e sincronização.  
  
## <a name="ssma-console-output-conventions"></a>Convenções de saída do Console SSMA  
Depois de executar os comandos de script do SSMA e opções, o programa do console exibe os resultados e mensagens (informações de erro, etc.) para o usuário no console ou se necessário, redireciona para um arquivo de saída xml. Cada tipo de mensagem na saída é representado por uma cor exclusiva. Por exemplo, a mensagem de texto em branco indica comandos de script de arquivo; a cor verde representa um prompt de entrada do usuário e assim por diante.  
  
![O SSMA Console Output_Oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "Output_Oracle do Console SSMA")  
  
Interpretação de cor da saída do console na tabela a seguir:  
  
|Color|Description|  
|---------|---------------|  
|Vermelho|Erro fatal durante a execução|  
|Cinza|Carimbo de data e hora, a mensagem para o usuário|  
|Branco|Comandos do arquivo de script, o tipo de mensagem|  
|Amarelo|Aviso|  
|Verde|Solicitar entrada do usuário|  
|Ciano|Início, término e o resultado de uma operação|  
  
## <a name="see-also"></a>Consulte também  
[Instalando o SSMA para DB2](http://msdn.microsoft.com/en-us/79fbe8ea-471b-407a-be2a-4100d9b57c61)  
  
