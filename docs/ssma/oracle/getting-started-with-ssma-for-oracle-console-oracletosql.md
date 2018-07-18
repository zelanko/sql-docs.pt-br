---
title: Introdução ao SSMA para o Console do Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Oracle Console, Console Output Conventions
- Oracle Console, Launching Console
ms.assetid: 667a5e4a-6848-4973-a72d-1287f64718ac
caps.latest.revision: 31
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 86b8adc8841e06d91d164c2c35e2329511ac0e28
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38985748"
---
# <a name="getting-started-with-ssma--for-oracle-console-oracletosql"></a>Introdução ao SSMA para o Console do Oracle (OracleToSQL)
Esta seção descreve o procedimento para iniciar e começar a trabalhar com o aplicativo de console do Oracle. Também é listado, aqui, são as convenções usadas em uma janela de saída do Console do SSMA típica.  
  
## <a name="launching-ssma-console"></a>Iniciando o Console do SSMA  
Use as etapas a seguir para iniciar o aplicativo de console do SSMA:  
  
1.  Vá para **inicie** e aponte para **todos os programas**.  
  
2.  Clique o  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Assistente de migração para o Prompt de comando do Oracle** atalho.  
  
    Ele exibe o menu de uso do Console do SSMA e `(/? Help)`, para ajudá-lo a começar com o aplicativo de console.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimento para usar o Console do SSMA  
Depois que o console é iniciado com êxito em seu sistema Windows, você pode usar as etapas a seguir para trabalhar nele:  
  
1.  Configure o Console do SSMA através dos arquivos de script. Para obter mais informações sobre essa seção, consulte [criando arquivos de Script &#40;OracleToSQL&#41; ](../../ssma/oracle/creating-script-files-oracletosql.md) .  
  
2.  [Criando arquivos de valor da variável &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
  
3.  [Criar os arquivos de Conexão de servidor &#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
4.  [Executar o Console do SSMA &#40;OracleToSQL&#41; ](../../ssma/oracle/executing-the-ssma-console-oracletosql.md) com base em suas necessidades de projeto  
  
Recursos adicionais:  
  
1.  [Especifique uma senha](http://msdn.microsoft.com/8c7d9f8e-06bb-476c-bbd2-15b61d5bba3c) e exportar / importá-los em outros computadores da janela  
  
2.  [Gerar relatórios](http://msdn.microsoft.com/ccad6262-01e1-447a-bd2b-c105154c80ce) exibir o xml detalhado relatórios para avaliação /conversion e migração de dados de saída. Relatórios de erro detalhadas também podem ser gerados para os comandos de atualização e a sincronização.  
  
## <a name="ssma-console-output-conventions"></a>Convenções de saída de Console do SSMA  
Após executar os comandos de script do SSMA e opções, o programa do console exibe os resultados e mensagens (informações de erro, etc.) para o usuário no console ou se for necessário, redireciona para um arquivo de saída xml. Cada tipo de mensagem na saída é representado por uma cor exclusiva. Por exemplo, a mensagem de texto cor branca indica comandos do arquivo de script; a cor verde representa um prompt para entrada do usuário e assim por diante.  
  
![O SSMA Console Output_Oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "Output_Oracle de Console do SSMA")  
  
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
[Instalar o SSMA para Oracle](http://msdn.microsoft.com/9211013a-ab24-4c52-9b26-87994b35e502)  
  
