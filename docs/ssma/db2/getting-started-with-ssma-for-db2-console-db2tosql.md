---
title: Introdução ao SSMA para DB2 Console (DB2ToSQL) | Microsoft Docs
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
ms.assetid: f245c017-023e-4880-8721-8908d339525e
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c74c3f21508ce08e6e540dd5c4cc84531b7c744d
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40393970"
---
# <a name="getting-started-with-ssma--for-db2-console-db2tosql"></a>Introdução ao SSMA para DB2 Console (DB2ToSQL)
Esta seção descreve o procedimento para iniciar e começar a trabalhar com o aplicativo de console do DB2. Também é listado, aqui, são as convenções usadas em uma janela de saída do Console do SSMA típica.  
  
## <a name="launching-ssma-console"></a>Iniciando o Console do SSMA  
Use as etapas a seguir para iniciar o aplicativo de console do SSMA:  
  
1.  Vá para **inicie** e aponte para **todos os programas**.  
  
2.  Clique o  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de migração para o Prompt de comando do DB2** atalho.  
  
    Ele exibe o menu de uso do Console do SSMA e `(/? Help)`, para ajudá-lo a começar com o aplicativo de console.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimento para usar o Console do SSMA  
Depois que o console é iniciado com êxito em seu sistema Windows, você pode usar as etapas a seguir para trabalhar nele:  
  
1.  Configure o Console do SSMA através dos arquivos de script. Para obter mais informações sobre essa seção, consulte [criando arquivos de Script &#40;DB2ToSQL&#41; ](../../ssma/db2/creating-script-files-db2tosql.md) .  
  
2.  [Criando arquivos de valor da variável &#40;DB2ToSQL&#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
  
3.  [Criar os arquivos de Conexão de servidor &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
  
4.  [Executar o Console do SSMA &#40;DB2ToSQL&#41; ](../../ssma/db2/executing-the-ssma-console-db2tosql.md) com base em suas necessidades de projeto  
  
Recursos adicionais:  
  
1.  [Gerenciamento de senhas](http://msdn.microsoft.com/56d546e3-8747-4169-aace-693302667e94) e exportar / importá-los em outros computadores da janela  
  
2.  [Geração de relatórios](http://msdn.microsoft.com/69ef5fd9-190d-4c58-8199-b3f77d5e1883) exibir o xml detalhado relatórios para avaliação /conversion e migração de dados de saída. Relatórios de erro detalhadas também podem ser gerados para os comandos de atualização e a sincronização.  
  
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
[Instalar o SSMA para DB2](http://msdn.microsoft.com/79fbe8ea-471b-407a-be2a-4100d9b57c61)  
  
