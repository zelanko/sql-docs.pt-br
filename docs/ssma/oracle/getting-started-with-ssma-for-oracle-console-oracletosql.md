---
title: Introdução com o console do SSMA para Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Oracle Console, Console Output Conventions
- Oracle Console, Launching Console
ms.assetid: 667a5e4a-6848-4973-a72d-1287f64718ac
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 25cd6eb9c811548e6300c944c65c5530185d46e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68264499"
---
# <a name="getting-started-with-ssma--for-oracle-console-oracletosql"></a>Introdução ao console do SSMA para Oracle (OracleToSQL)
Esta seção descreve o procedimento para iniciar e começar a usar o aplicativo de console do Oracle. Também listados aqui, estão as convenções usadas em uma janela de saída típica do console do SSMA.  
  
## <a name="launching-ssma-console"></a>Iniciando o console do SSMA  
Use as etapas a seguir para iniciar o aplicativo de console do SSMA:  
  
1.  Vá para **Iniciar** e aponte para **todos os programas**.  
  
2.  Clique no ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assistente de migração para o atalho do prompt de comando do Oracle** .  
  
    Ele exibe o menu uso do console do `(/? Help)`SSMA e, para ajudá-lo a começar a usar o aplicativo de console.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimento para usar o console do SSMA  
Depois que o console do for iniciado com êxito no seu sistema Windows, você poderá usar as seguintes etapas para trabalhar nele:  
  
1.  Configure o console do SSMA por meio dos arquivos de script. Para obter mais informações sobre esta seção, consulte [criando arquivos de Script &#40;OracleToSQL&#41;](../../ssma/oracle/creating-script-files-oracletosql.md) .  
  
2.  [Criando arquivos de valor de variável &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
  
3.  [Criando os arquivos de conexão do servidor &#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
4.  [Executando o console do SSMA &#40;OracleToSQL&#41;](../../ssma/oracle/executing-the-ssma-console-oracletosql.md) com base em suas necessidades de projeto  
  
Recursos adicionais:  
  
1.  [Especificar uma senha](managing-passwords-oracletosql.md) e exportá-la/importá-la para outros computadores da janela  
  
2.  [Gere relatórios](generating-reports-oracletosql.md) para exibir os relatórios de saída XML detalhados para avaliação/Conversion e migração de dados. Relatórios de erro detalhados também podem ser gerados para comandos de sincronização e atualização.  
  
## <a name="ssma-console-output-conventions"></a>Convenções de saída do console do SSMA  
Após a execução dos comandos e opções do script do SSMA, o programa de console exibe os resultados e as mensagens (informações, erro, etc.) para o usuário no console do ou, se necessário, redireciona para um arquivo de saída XML. Cada tipo de mensagem na saída é representado por uma cor exclusiva. Por exemplo, a mensagem de texto na cor branca denota comandos de arquivo de script; a cor verde representa um prompt para entrada do usuário e assim por diante.  
  
![SSMA Console Output_Oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "SSMA Console Output_Oracle")  
  
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
[Instalando o SSMA para Oracle](installing-ssma-for-oracle-oracletosql.md)  
  
