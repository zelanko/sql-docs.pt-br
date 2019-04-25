---
title: Introdução ao SSMA para Sybase Console (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Launching SSMA Console
- Sybase Console,Output Conventions
- Sybase Console,Procedure for Using Console
ms.assetid: 43219dbe-bcfa-427d-9242-f07b1455f15f
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 608457b1732d2c1cc188b4b419903d20faa642c8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62631945"
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>Introdução ao SSMA para Sybase Console (SybaseToSQL)
Esta seção descreve o procedimento para iniciar e guia de Introdução o SSMA para Sybase aplicativo de console. Também são listados aqui são as convenções usadas em uma janela de saída do Console do SSMA típica.  
  
## <a name="launching-the-ssma-console"></a>Iniciando o Console do SSMA  
Use as etapas a seguir para iniciar o aplicativo de console do SSMA:  
  
1.  Vá para iniciar e, em seguida, aponte para todos os programas.  
  
2.  Clique o **SQL Server Migration Assistant para o Prompt de comando do Sybase** atalho.  
  
    Ele exibe o menu de uso do Console do SSMA e `(/? Help)`, para ajudá-lo a começar com o aplicativo de console.  
  
## <a name="using-the-ssma-console"></a>Usando o Console do SSMA  
Depois que o console é iniciado com êxito em seu sistema Windows, você pode usar as etapas a seguir para trabalhar nele:  
  
1.  Configure o Console do SSMA através dos arquivos de script. Para obter mais informações sobre essa seção, consulte [criando arquivos de Script &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
2.  [Criando arquivos de valor da variável &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [Criar os arquivos de Conexão de servidor &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [Executar o Console do SSMA &#40;SybaseToSQL&#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) com base em suas necessidades de projeto. 
  
Recursos adicionais:  
  
1.  [Especifique uma senha](managing-passwords-sybasetosql.md) e importação/exportação-lo para outros computadores da janela.  
  
2.  [Gerar relatórios](generating-reports-sybasetosql.md) exibir o xml detalhado relatórios para conversão/avaliação e migração de dados de saída. Você também pode gerar relatórios de erro detalhada para comandos de atualização e a sincronização.  
  
## <a name="ssma-console-output-conventions"></a>Convenções de saída do Console do SSMA  
Após executar os comandos de script do SSMA e opções, o programa de console exibe os resultados e mensagens (informações de erro, etc.) para o usuário no console ou, se necessário, redireciona para um arquivo de saída xml. Cada tipo de mensagem na saída é representado por uma cor exclusiva. Por exemplo, a mensagem de texto cor branca indica comandos do arquivo de script; a cor verde representa um prompt para entrada do usuário e assim por diante.  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
Interpretação de cor da saída do console aparece na tabela a seguir:  
  
|Cor|Descrição|  
|---------|---------------|  
|Vermelho|Erro fatal durante a execução|  
|Cinza|Carimbo de data e hora da mensagem para o usuário|  
|Branco|Comandos do arquivo de script, o tipo de mensagem|  
|Amarelo|Aviso|  
|Verde|Prompt para entrada do usuário|  
|Ciano|Início, término e o resultado de uma operação|  
  
## <a name="see-also"></a>Confira também  
[Instalar o SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
