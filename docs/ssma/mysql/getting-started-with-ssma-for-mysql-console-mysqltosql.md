---
title: Introdução ao SSMA para o Console do MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- MySQL Console, launching console
- MySQL Console, output conventions
ms.assetid: 218d502c-059f-4d48-9aea-61e553d74303
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 88cf4716ea02b8c5dbcbd73e9839c6bacfbed10b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075425"
---
# <a name="getting-started-with-ssma-for-mysql-console-mysqltosql"></a>Introdução ao Console de SSMA para MySQL (MySQLToSQL)
Esta seção descreve o procedimento para iniciar e começar a trabalhar com o aplicativo de console do MySQL. Também é listado, aqui, são as convenções usadas em uma janela de saída do Console do SSMA típica.  
  
## <a name="launching-ssma-console"></a>Iniciando o Console do SSMA  
Use as etapas a seguir para iniciar o aplicativo de console do SSMA:  
  
1.  Vá para **inicie** e aponte para **todos os programas**.  
  
2.  Clique o **SQL Server Migration Assistant para o Prompt de comando do MySQL** atalho.  
  
    Ele exibe o menu de uso do Console do SSMA e `(/? Help)`, para ajudá-lo a começar com o aplicativo de console.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimento para usar o Console do SSMA  
Depois que o console é iniciado com êxito em seu sistema Windows, você pode usar as etapas a seguir para trabalhar nele:  
  
1.  Configure o Console do SSMA através dos arquivos de script. Para obter mais informações sobre essa seção, consulte [criando arquivos de Script &#40;MySQLToSQL&#41; ](../../ssma/mysql/creating-script-files-mysqltosql.md) .  
  
2.  [Criando arquivos de valor da variável &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
  
3.  [Criar os arquivos de Conexão de servidor &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
4.  [Executar o Console do SSMA &#40;MySQLToSQL&#41; ](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md) com base em suas necessidades de projeto  
  
Recursos adicionais:  
  
1.  [Proteção de senha](managing-passwords-mysqltosql.md) e exportar / importá-los em outros computadores da janela  
  
2.  [Gerar relatórios](generating-reports-mysqltosql.md) exibir o xml detalhado relatórios para avaliação /conversion e migração de dados de saída. Relatórios de erro detalhadas também podem ser gerados para os comandos de atualização e a sincronização.  
  
## <a name="ssma-console-output-conventions"></a>Convenções de saída de Console do SSMA  
Após executar os comandos de script do SSMA e opções, o programa do console exibe os resultados e mensagens (informações de erro, etc.) para o usuário no console ou se for necessário, redireciona para um arquivo de saída xml. Cada tipo de mensagem na saída é representado por uma cor exclusiva. Por exemplo, a mensagem de texto cor branca indica comandos do arquivo de script; a cor verde representa um prompt para entrada do usuário e assim por diante.  
  
![SSMAConsoleOutput_MySQL](../../ssma/mysql/media/ssmaconsoleoutput_mysql.jpg "SSMAConsoleOutput_MySQL")  
  
Interpretação de cor da saída do console na tabela a seguir:  
  
|Cor|Descrição|  
|---------|---------------|  
|Vermelho|Erro fatal durante a execução|  
|Cinza|Carimbo de data e hora da mensagem para o usuário|  
|Branco|Comandos do arquivo de script, o tipo de mensagem|  
|Amarelo|Aviso|  
|Verde|Prompt para entrada do usuário|  
|Ciano|Guia de início, término e o resultado de uma operação|  
  
## <a name="see-also"></a>Consulte também  
[Instalar o SSMA para MySQL](installing-ssma-for-mysql-mysqltosql.md)  
  
