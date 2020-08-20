---
description: Introdução ao Console de SSMA para MySQL (MySQLToSQL)
title: Introdução com o console do SSMA para MySQL (MySQLToSQL) | Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 9eba640bc529487772510e06a7c66210be3e43a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463435"
---
# <a name="getting-started-with-ssma-for-mysql-console-mysqltosql"></a>Introdução ao Console de SSMA para MySQL (MySQLToSQL)
Esta seção descreve o procedimento para iniciar e começar a usar o aplicativo de console do MySQL. Também listados aqui, estão as convenções usadas em uma janela de saída típica do console do SSMA.  
  
## <a name="launching-ssma-console"></a>Iniciando o console do SSMA  
Use as etapas a seguir para iniciar o aplicativo de console do SSMA:  
  
1.  Vá para **Iniciar** e aponte para **todos os programas**.  
  
2.  Clique no **Assistente de migração do SQL Server para o atalho do prompt de comando do MySQL** .  
  
    Ele exibe o menu uso do console do SSMA e `(/? Help)` , para ajudá-lo a começar a usar o aplicativo de console.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimento para usar o console do SSMA  
Depois que o console do for iniciado com êxito no seu sistema Windows, você poderá usar as seguintes etapas para trabalhar nele:  
  
1.  Configure o console do SSMA por meio dos arquivos de script. Para obter mais informações sobre esta seção, consulte [criando arquivos de Script &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-script-files-mysqltosql.md) .  
  
2.  [Criando arquivos de valor de variável &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
  
3.  [Criando os arquivos de conexão do servidor &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
4.  [Executando o console do SSMA &#40;MySQLToSQL&#41;](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md) com base em suas necessidades de projeto  
  
Recursos adicionais:  
  
1.  [Protegendo a senha](managing-passwords-mysqltosql.md) e exporte/importe-a para outras máquinas de janela  
  
2.  [Gere relatórios](generating-reports-mysqltosql.md) para exibir os relatórios de saída XML detalhados para avaliação/Conversion e migração de dados. Relatórios de erro detalhados também podem ser gerados para comandos de sincronização e atualização.  
  
## <a name="ssma-console-output-conventions"></a>Convenções de saída do console do SSMA  
Após a execução dos comandos e opções do script do SSMA, o programa de console exibe os resultados e as mensagens (informações, erro, etc.) para o usuário no console do ou, se necessário, redireciona para um arquivo de saída XML. Cada tipo de mensagem na saída é representado por uma cor exclusiva. Por exemplo, a mensagem de texto na cor branca denota comandos de arquivo de script; a cor verde representa um prompt para entrada do usuário e assim por diante.  
  
![SSMAConsoleOutput_MySQL](../../ssma/mysql/media/ssmaconsoleoutput_mysql.jpg "SSMAConsoleOutput_MySQL")  
  
Interpretação de cores da saída do console na tabela a seguir:  
  
|Color|DESCRIÇÃO|  
|---------|---------------|  
|Vermelho|Erro fatal durante a execução|  
|Cinza|Carimbo de data e hora, mensagem para o usuário|  
|Branco|Comandos de arquivo de script, tipo de mensagem|  
|Amarelo|Aviso|  
|Verde|Solicitar entrada do usuário|  
|Cores|Início, término e resultado de uma operação|  
  
## <a name="see-also"></a>Consulte Também  
[Instalando o SSMA para MySQL](installing-ssma-for-mysql-mysqltosql.md)  
  
