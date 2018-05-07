---
title: Guia de Introdução com o SSMA para Sybase Console (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: d9b401ea1efdfcececbb35a16d7d10b29915e1fc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>Guia de Introdução com o SSMA para Sybase Console (SybaseToSQL)
Esta seção descreve o procedimento para iniciar e guia de Introdução do SSMA para Sybase aplicativo de console. Também são listados aqui são as convenções usadas em uma janela de saída do Console SSMA típica.  
  
## <a name="launching-the-ssma-console"></a>Iniciar o Console do SSMA  
Use as etapas a seguir para iniciar o aplicativo de console SSMA:  
  
1.  Vá para iniciar e, em seguida, aponte para todos os programas.  
  
2.  Clique o **SQL Server Migration Assistant para o Prompt de comando do Sybase** atalho.  
  
    Exibe o menu de uso do Console SSMA e `(/? Help)`, para ajudá-lo a começar com o aplicativo de console.  
  
## <a name="using-the-ssma-console"></a>Usando o Console do SSMA  
Depois que o console é iniciado com êxito em seu sistema Windows, você pode usar as etapas a seguir para trabalhar nela:  
  
1.  Configure o Console do SSMA através dos arquivos de script. Para obter mais informações sobre esta seção, consulte [criando arquivos de Script &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
2.  [Criando arquivos do valor da variável &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [Criar os arquivos de Conexão de servidor &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [Executar o Console SSMA &#40;SybaseToSQL&#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) com base em suas necessidades de projeto. 
  
Recursos adicionais:  
  
1.  [Especifique uma senha](http://msdn.microsoft.com/en-us/9b6a70f9-6840-4140-a059-bb7bd7ccc67c) e importação/exportação-lo para outros computadores com Windows.  
  
2.  [Gerar relatórios](http://msdn.microsoft.com/en-us/19278f6a-6d58-4867-9d71-c6228040466e) exibir o xml detalhado gerar relatórios de avaliação/conversão e migração de dados. Você também pode gerar relatórios de erro detalhadas para comandos de atualização e sincronização.  
  
## <a name="ssma-console-output-conventions"></a>Convenções de saída do Console SSMA  
Ao executar os comandos de script do SSMA e opções, o programa do console exibe os resultados e mensagens (informações de erro, etc.) para o usuário no console ou, se necessário, redireciona para um arquivo de saída xml. Cada tipo de mensagem na saída é representado por uma cor exclusiva. Por exemplo, a mensagem de texto em branco indica comandos de script de arquivo; a cor verde representa um prompt de entrada do usuário e assim por diante.  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
Interpretação de cor da saída do console é exibida na tabela a seguir:  
  
|Color|Description|  
|---------|---------------|  
|Vermelho|Erro fatal durante a execução|  
|Cinza|Carimbo de data e hora, a mensagem para o usuário|  
|Branco|Comandos do arquivo de script, o tipo de mensagem|  
|Amarelo|Aviso|  
|Verde|Solicitar entrada do usuário|  
|Ciano|Início, término e resultado de uma operação|  
  
## <a name="see-also"></a>Consulte também  
[Instalando o SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
