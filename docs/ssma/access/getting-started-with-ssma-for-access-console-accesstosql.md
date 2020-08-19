---
description: Introdução com o console do SSMA para Access (AccessToSQL)
title: Introdução com o console do SSMA para Access (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8585ec16-7e0a-483a-b250-adab9b9232a3
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1923323699282e40fcca8afa1a8079edd8163c09
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426978"
---
# <a name="getting-started-with-ssma-for-access-console-accesstosql"></a>Introdução com o console do SSMA para Access (AccessToSQL)
Esta seção descreve o procedimento para iniciar e começar a usar o aplicativo de console do Access. Também listados aqui, estão as convenções usadas em uma janela de saída típica do console do SSMA.  
  
## <a name="launching-ssma-console"></a>Iniciando o console do SSMA  
Use as etapas a seguir para iniciar o aplicativo de console do SSMA:  
  
1.  Vá para **Iniciar** e aponte para **todos os programas**.  
  
2.  Clique no atalho **Assistente de migração do SQL Server para acessar o prompt de comando** .  
  
    Ele exibe o menu uso do console do SSMA e `(/? Help)` , para ajudá-lo a começar a usar o aplicativo de console.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedimento para usar o console do SSMA  
Depois que o console do for iniciado com êxito no seu sistema Windows, você poderá usar as seguintes etapas para trabalhar nele:  
  
1.  Configure o console do SSMA por meio dos arquivos de script. Para obter mais informações sobre esta seção, consulte [criando arquivos de Script &#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md).  
  
2.  [Criando arquivos de valor de variável &#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
3.  [Criando os arquivos de conexão do servidor &#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
4.  [Executando o console do SSMA &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md) com base em suas necessidades de projeto  
  
Recursos adicionais:  
  
1.  [Especificar uma senha](managing-passwords-accesstosql.md) e exportá-la/importá-la para outros computadores da janela  
  
2.  [Gere relatórios](generating-reports-accesstosql.md) para exibir os relatórios de saída XML detalhados para avaliação/Conversion e migração de dados. Relatórios de erro detalhados também podem ser gerados para comandos de sincronização e atualização.  
  
## <a name="ssma-console-output-conventions"></a>Convenções de saída do console do SSMA  
Após a execução dos comandos e opções do script do SSMA, o programa de console exibe os resultados e as mensagens (informações, erro, etc.) para o usuário no console do ou, se necessário, redireciona para um arquivo de saída XML. Cada tipo de mensagem na saída é representado por uma cor exclusiva. Por exemplo, a mensagem de texto na cor branca denota comandos de arquivo de script; a cor verde representa um prompt para entrada do usuário e assim por diante.  
  
![Saída do Console SSMA](../../ssma/access/media/ssmaconsoleoutput.jpg "Saída do Console SSMA")  
  
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
[Instalando o Assistente de Migração do SQL Server para acesso](installing-sql-server-migration-assistant-for-access-accesstosql.md)  
  
