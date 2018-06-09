---
title: Guia de Introdução com o SSMA para MySQL Console (MySQLToSQL) | Microsoft Docs
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
helpviewer_keywords:
- MySQL Console, launching console
- MySQL Console, output conventions
ms.assetid: 218d502c-059f-4d48-9aea-61e553d74303
caps.latest.revision: 23
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 75e189d89c9a1bbc7207521b8156d0f4b56ca759
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34776232"
---
# <a name="getting-started-with-ssma-for-mysql-console-mysqltosql"></a>Guia de Introdução com o SSMA para MySQL Console (MySQLToSQL)
Esta seção descreve o procedimento para iniciar e começar a trabalhar com o aplicativo de console do MySQL. Também é listado, aqui, são as convenções usadas em uma janela de saída do Console SSMA típica.  
  
## <a name="launching-ssma-console"></a>Iniciar Console do SSMA  
Use as etapas a seguir para iniciar o aplicativo de console SSMA:  
  
1.  Vá para **iniciar** e aponte para **todos os programas**.  
  
2.  Clique o **SQL Server Migration Assistant para o Prompt de comando do MySQL** atalho.  
  
    Exibe o menu de uso do Console SSMA e `(/? Help)`, para ajudá-lo a começar com o aplicativo de console.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimento para usar o Console do SSMA  
Depois que o console é iniciado com êxito em seu sistema Windows, você pode usar as etapas a seguir para trabalhar nela:  
  
1.  Configure o Console do SSMA através dos arquivos de script. Para obter mais informações sobre esta seção, consulte [criando arquivos de Script &#40;MySQLToSQL&#41; ](../../ssma/mysql/creating-script-files-mysqltosql.md) .  
  
2.  [Criando arquivos do valor da variável &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
  
3.  [Criar os arquivos de Conexão de servidor &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
4.  [Executar o Console SSMA &#40;MySQLToSQL&#41; ](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md) com base em suas necessidades de projeto  
  
Recursos adicionais:  
  
1.  [Proteção de senha](http://msdn.microsoft.com/en-us/4ffbc587-ea3f-49ad-bc42-a654f672325e) e exportar / importá-lo em outros computadores da janela  
  
2.  [Gerar relatórios](http://msdn.microsoft.com/en-us/1c0202e8-546d-4cb3-a37f-1d2e35d53839) para exibir o xml detalhado a saída de relatórios para avaliação /conversion e migração de dados. Relatórios de erro detalhadas também podem ser gerados para os comandos de atualização e sincronização.  
  
## <a name="ssma-console-output-conventions"></a>Convenções de saída do Console SSMA  
Depois de executar os comandos de script do SSMA e opções, o programa do console exibe os resultados e mensagens (informações de erro, etc.) para o usuário no console ou se necessário, redireciona para um arquivo de saída xml. Cada tipo de mensagem na saída é representado por uma cor exclusiva. Por exemplo, a mensagem de texto em branco indica comandos de script de arquivo; a cor verde representa um prompt de entrada do usuário e assim por diante.  
  
![SSMAConsoleOutput_MySQL](../../ssma/mysql/media/ssmaconsoleoutput_mysql.jpg "SSMAConsoleOutput_MySQL")  
  
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
[Instalando o SSMA para MySQL](http://msdn.microsoft.com/en-us/e89b45bd-59c1-4d23-8bd7-3dafc1947448)  
  
