---
title: Guia de Introdução com o SSMA para o Console do Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Oracle Console, Console Output Conventions
- Oracle Console, Launching Console
ms.assetid: 667a5e4a-6848-4973-a72d-1287f64718ac
caps.latest.revision: 31
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 8fb5dc2f2bc16f531ffebef7a4e908fe6260b7a3
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="getting-started-with-ssma--for-oracle-console-oracletosql"></a>Guia de Introdução com o SSMA para o Console do Oracle (OracleToSQL)
Esta seção descreve o procedimento para iniciar e começar a trabalhar com o aplicativo de console do Oracle. Também é listado, aqui, são as convenções usadas em uma janela de saída do Console SSMA típica.  
  
## <a name="launching-ssma-console"></a>Iniciar Console do SSMA  
Use as etapas a seguir para iniciar o aplicativo de console SSMA:  
  
1.  Vá para **iniciar** e aponte para **todos os programas**.  
  
2.  Clique o  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Assistente de migração para o Prompt de comando do Oracle** atalho.  
  
    Exibe o menu de uso do Console SSMA e `(/? Help)`, para ajudá-lo a começar com o aplicativo de console.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimento para usar o Console do SSMA  
Depois que o console é iniciado com êxito em seu sistema Windows, você pode usar as etapas a seguir para trabalhar nela:  
  
1.  Configure o Console do SSMA através dos arquivos de script. Para obter mais informações sobre esta seção, consulte [criando arquivos de Script &#40;OracleToSQL&#41; ](../../ssma/oracle/creating-script-files-oracletosql.md) .  
  
2.  [Criando arquivos do valor da variável &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
  
3.  [Criar os arquivos de Conexão de servidor &#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
4.  [Executar o Console SSMA &#40;OracleToSQL&#41; ](../../ssma/oracle/executing-the-ssma-console-oracletosql.md) com base em suas necessidades de projeto  
  
Recursos adicionais:  
  
1.  [Especifique uma senha](http://msdn.microsoft.com/en-us/8c7d9f8e-06bb-476c-bbd2-15b61d5bba3c) e exportar / importá-lo em outros computadores da janela  
  
2.  [Gerar relatórios](http://msdn.microsoft.com/en-us/ccad6262-01e1-447a-bd2b-c105154c80ce) para exibir o xml detalhado a saída de relatórios para avaliação /conversion e migração de dados. Relatórios de erro detalhadas também podem ser gerados para os comandos de atualização e sincronização.  
  
## <a name="ssma-console-output-conventions"></a>Convenções de saída do Console SSMA  
Depois de executar os comandos de script do SSMA e opções, o programa do console exibe os resultados e mensagens (informações de erro, etc.) para o usuário no console ou se necessário, redireciona para um arquivo de saída xml. Cada tipo de mensagem na saída é representado por uma cor exclusiva. Por exemplo, a mensagem de texto em branco indica comandos de script de arquivo; a cor verde representa um prompt de entrada do usuário e assim por diante.  
  
![O SSMA Console Output_Oracle](../../ssma/db2/media/ssmaconsoleoutput_oracle.jpg "Output_Oracle do Console SSMA")  
  
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
[Instalando o SSMA para Oracle](http://msdn.microsoft.com/en-us/9211013a-ab24-4c52-9b26-87994b35e502)  
  
