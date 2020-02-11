---
title: Introdução com o console do SSMA para Sybase (SybaseToSQL) | Microsoft Docs
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
ms.openlocfilehash: bad08c06028a64a0423135b15641ebf6fa4e895e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029114"
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>Introdução com o console do SSMA para Sybase (SybaseToSQL)
Esta seção descreve o procedimento para iniciar e começar a usar o aplicativo de console do SSMA para Sybase. Também estão listados aqui as convenções usadas em uma janela de saída típica do console do SSMA.  
  
## <a name="launching-the-ssma-console"></a>Iniciando o console do SSMA  
Use as etapas a seguir para iniciar o aplicativo de console do SSMA:  
  
1.  Vá até iniciar e aponte para todos os programas.  
  
2.  Clique no **Assistente de migração do SQL Server para o atalho do prompt de comando Sybase** .  
  
    Ele exibe o menu uso do console do `(/? Help)`SSMA e, para ajudá-lo a começar a usar o aplicativo de console.  
  
## <a name="using-the-ssma-console"></a>Usando o console do SSMA  
Depois que o console do for iniciado com êxito no seu sistema Windows, você poderá usar as seguintes etapas para trabalhar nele:  
  
1.  Configure o console do SSMA por meio dos arquivos de script. Para obter mais informações sobre esta seção, consulte [criando arquivos de Script &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
2.  [Criando arquivos de valor de variável &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [Criando os arquivos de conexão do servidor &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [Executar o console do SSMA &#40;o SybaseToSQL&#41;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) com base em suas necessidades de projeto. 
  
Recursos adicionais:  
  
1.  [Especifique uma senha](managing-passwords-sybasetosql.md) e exporte/importe-a para outros computadores Windows.  
  
2.  [Gere relatórios](generating-reports-sybasetosql.md) para exibir os relatórios de saída XML detalhados para avaliação/conversão e migração de dados. Você também pode gerar relatórios de erros detalhados para comandos de sincronização e atualização.  
  
## <a name="ssma-console-output-conventions"></a>Convenções de saída do console do SSMA  
Após a execução dos comandos e opções do script do SSMA, o programa de console exibe os resultados e as mensagens (informações, erro, etc.) para o usuário no console do ou, se necessário, redireciona para um arquivo de saída XML. Cada tipo de mensagem na saída é representado por uma cor exclusiva. Por exemplo, a mensagem de texto na cor branca denota comandos de arquivo de script; a cor verde representa um prompt para entrada do usuário e assim por diante.  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
A interpretação de cores da saída do console aparece na tabela a seguir:  
  
|Color|DESCRIÇÃO|  
|---------|---------------|  
|Vermelho|Erro fatal durante a execução|  
|Cinza|Carimbo de data e hora, mensagem para o usuário|  
|Branco|Comandos de arquivo de script, tipo de mensagem|  
|Amarelo|Aviso|  
|Verde|Solicitar entrada do usuário|  
|Cores|Início, término e resultado de uma operação|  
  
## <a name="see-also"></a>Confira também  
[Instalando o SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
