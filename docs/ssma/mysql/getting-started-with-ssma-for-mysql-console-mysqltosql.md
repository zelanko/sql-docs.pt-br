---
title: Introdução ao SSMA para o Console do MySQL (MySQLToSQL) | Microsoft Docs
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
ms.openlocfilehash: 8f33769bee5c8d6d9e134eb9dd5dcf8549d651cb
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983078"
---
# <a name="getting-started-with-ssma-for-mysql-console-mysqltosql"></a>Introdução ao SSMA para o Console do MySQL (MySQLToSQL)
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
  
1.  [Proteção de senha](http://msdn.microsoft.com/4ffbc587-ea3f-49ad-bc42-a654f672325e) e exportar / importá-los em outros computadores da janela  
  
2.  [Gerar relatórios](http://msdn.microsoft.com/1c0202e8-546d-4cb3-a37f-1d2e35d53839) exibir o xml detalhado relatórios para avaliação /conversion e migração de dados de saída. Relatórios de erro detalhadas também podem ser gerados para os comandos de atualização e a sincronização.  
  
## <a name="ssma-console-output-conventions"></a>Convenções de saída de Console do SSMA  
Após executar os comandos de script do SSMA e opções, o programa do console exibe os resultados e mensagens (informações de erro, etc.) para o usuário no console ou se for necessário, redireciona para um arquivo de saída xml. Cada tipo de mensagem na saída é representado por uma cor exclusiva. Por exemplo, a mensagem de texto cor branca indica comandos do arquivo de script; a cor verde representa um prompt para entrada do usuário e assim por diante.  
  
![SSMAConsoleOutput_MySQL](../../ssma/mysql/media/ssmaconsoleoutput_mysql.jpg "SSMAConsoleOutput_MySQL")  
  
Interpretação de cor da saída do console na tabela a seguir:  
  
|Color|Description|  
|---------|---------------|  
|Vermelho|Erro fatal durante a execução|  
|Cinza|Carimbo de data e hora da mensagem para o usuário|  
|Branco|Comandos do arquivo de script, o tipo de mensagem|  
|Amarelo|Aviso|  
|Verde|Prompt para entrada do usuário|  
|Ciano|Guia de início, término e o resultado de uma operação|  
  
## <a name="see-also"></a>Consulte também  
[Instalar o SSMA para MySQL](http://msdn.microsoft.com/e89b45bd-59c1-4d23-8bd7-3dafc1947448)  
  
