---
title: "Introdução ao SSMA for Sybase Console (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Launching SSMA Console
- Sybase Console,Output Conventions
- Sybase Console,Procedure for Using Console
ms.assetid: 43219dbe-bcfa-427d-9242-f07b1455f15f
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 239b7a8f4dbc3069e67d680b319bf426a0f917e6
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="getting-started-with-ssma-for-sybase-console-sybasetosql"></a>Introdução ao SSMA for Sybase Console (SybaseToSQL)
Esta seção descreve o procedimento para iniciar e começar a trabalhar com o aplicativo de console do Sybase. Também é listado, aqui, são as convenções usadas em uma janela de saída do Console SSMA típica.  
  
## <a name="launching-ssma-console"></a>Iniciar Console do SSMA  
Use as etapas a seguir para iniciar o aplicativo de console SSMA:  
  
1.  Vá para iniciar e aponte para todos os programas.  
  
2.  Clique o **SQL Server Migration Assistant para o Prompt de comando do Sybase** atalho.  
  
    Exibe o menu de uso do Console SSMA e `(/? Help)`, para ajudá-lo a começar com o aplicativo de console.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimento para usar o Console do SSMA  
Depois que o console é iniciado com êxito em seu sistema Windows, você pode usar as etapas a seguir para trabalhar nela:  
  
1.  Configure o Console do SSMA através dos arquivos de script. Para obter mais informações sobre esta seção, consulte [criando arquivos de Script &#40; SybaseToSQL &#41; ](../../ssma/sybase/creating-script-files-sybasetosql.md) .  
  
2.  [Criando arquivos do valor da variável &#40; SybaseToSQL &#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [Criar os arquivos de Conexão do servidor &#40; SybaseToSQL &#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [Executar o Console SSMA &#40; SybaseToSQL &#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) com base em suas necessidades de projeto  
  
Recursos adicionais:  
  
1.  [Especifique uma senha](http://msdn.microsoft.com/en-us/9b6a70f9-6840-4140-a059-bb7bd7ccc67c) e exportar / importá-lo em outros computadores da janela  
  
2.  [Gerar relatórios](http://msdn.microsoft.com/en-us/19278f6a-6d58-4867-9d71-c6228040466e) para exibir o xml detalhado a saída de relatórios para avaliação /conversion e migração de dados. Relatórios de erro detalhadas também podem ser gerados para os comandos de atualização e sincronização.  
  
## <a name="ssma-console-output-conventions"></a>Convenções de saída do Console SSMA  
Depois de executar os comandos de script do SSMA e opções, o programa do console exibe os resultados e mensagens (informações de erro, etc.) para o usuário no console ou se necessário, redireciona para um arquivo de saída xml. Cada tipo de mensagem na saída é representado por uma cor exclusiva. Por exemplo, a mensagem de texto em branco indica comandos de script de arquivo; a cor verde representa um prompt de entrada do usuário e assim por diante.  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
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
[Instalando o SSMA para Sybase &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
  

